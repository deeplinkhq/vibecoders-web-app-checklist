# Aplikace

**Týká se:** aplikace s přihlášením, uživatelskými rolemi, transakčními e-maily, platbami nebo nahráváním souborů. Jednotlivé části přeskoč, když danou funkci aplikace nemá.

Aktivní kontroly prováděj s testovacími účty a daty v odděleném prostředí. Platby zkoušej v testovacím režimu. Čtení kódu neprokazuje doručení e-mailu ani skutečné zneplatnění relace. Bez potřebného přístupu napiš „Ověř ručně“ a uveď konkrétní chybějící kontrolu.

Bezpečnost přihlášení, tokenů, relací, oprávnění a nahraných souborů viz [Bezpečnost](08-bezpecnost.md), testovací režim plateb a e-mailů viz [Doména a nasazení](11-domena-a-nasazeni.md), výmaz u zpracovatelů a v zálohách a lhůty žádostí viz [Právo a analytika](07-pravo-a-analytika.md).

## Přihlášení a obnova účtu

Kontroly vycházejí z doporučení OWASP pro [přihlašování](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), [obnovu hesla](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) a [ověřování e-mailové adresy](https://cheatsheetseries.owasp.org/cheatsheets/Email_Validation_and_Verification_Cheat_Sheet.html).

- [ ] Když aplikace umožňuje registraci: nový uživatel dokončí registraci až k přístupu do svého účtu. Samotná úspěšná odpověď registračního API nestačí. *Ověření (prohlížeč):* založ testovací účet, dokonči požadované ověření a otevři jeho soukromou část.

- [ ] Když aplikace používá e-mail jako ověřenou identitu: neověřená adresa nezíská oprávnění vázaná na její vlastnictví. Týká se například přijetí pozvánky pro konkrétní adresu. [OWASP Email Verification] *Ověření:* s neověřeným testovacím účtem zavolej přímo příslušné API; server musí akci odmítnout.

- [ ] Když aplikace umožňuje reset hesla e-mailem: uživatel dokončí obnovu přes doručený e-mail a přihlásí se novým heslem. [OWASP Forgot Password] *Ověření (prohlížeč):* proveď obnovu testovacího účtu od žádosti přes odkaz ve schránce až po nové přihlášení; původní heslo musí přestat fungovat.

- [ ] Když uživatel mění přihlašovací e-mail: nová adresa se aktivuje až po ověření jejího vlastnictví. [OWASP Authentication] *Ověření:* před potvrzením nové adresy zkus její použití pro přihlášení nebo obnovu účtu; ověř, že server změnu drží jako nepotvrzenou.

- [ ] Když projekt drží osobní údaje cizích lidí a uživatel mění přihlašovací e-mail: na původní adresu přijde upozornění na změnu. Pomůže odhalit převzetí účtu. [OWASP Authentication] *Ověření (prohlížeč):* změň adresu testovacího účtu a zkontroluj zprávu v původní schránce.

## Správa relací

Pravidla vycházejí z [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html).

- [ ] Když uživatel obnoví heslo: aplikace mu nabídne zneplatnění všech dosavadních relací, nebo je zneplatní automaticky. Po úspěšné obnově účtu při podezření na jeho převzetí se zneplatní všechny dosavadní relace. *Ověření:* otevři účet ve dvou klientech, při běžné obnově zvol zneplatnění relací a zopakuj požadavky se starými relacemi i obnovovacími tokeny; u obnovy napadeného účtu ověř automatické zneplatnění. Podklad také: [OWASP Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html).

- [ ] Když uživatel v aplikaci píše delší text nebo vyplňuje formulář: vypršení přihlášení nezahodí rozepsaná data. Po novém přihlášení může pokračovat, nebo aplikace data předem uloží jako koncept. *Ověření (prohlížeč):* rozepiš testovací záznam, v jiné záložce se odhlas nebo smaž cookie relace a zkus záznam uložit; po přihlášení ověř, že text nezmizel. Podklad: [WCAG 2.2.5 AAA](https://www.w3.org/WAI/WCAG22/Understanding/re-authenticating.html).

## Role a oprávnění

Podkladem jsou [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) a ochrana před [mass assignment](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html).

- [ ] Když administrátor odebere roli, členství nebo zablokuje účet: odebrané oprávnění přestane platit i pro již přihlášeného uživatele. [OWASP Authorization] *Ověření:* po odebrání zopakuj chráněnou operaci se starou relací; nespoléhej na nové přihlášení nebo obnovení stránky.

## Transakční e-maily

Opakování doručení vychází z [RFC 5321](https://www.rfc-editor.org/rfc/rfc5321.html). SPF, DKIM a DMARC odesílací domény viz [Doména a nasazení](11-domena-a-nasazeni.md).

- [ ] Když aplikace posílá odkazy pro práci s účtem: cílová adresa odpovídá prostředí a vzniká z důvěryhodné konfigurace. Nesmí ji podvrhnout hlavička požadavku. *Ověření:* zkontroluj generování URL a zprávy v testovací schránce; požadavek s cizí hlavičkou `Host` nesmí vytvořit odkaz na cizí doménu. Podklad: [OWASP Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html).

- [ ] Když aplikace posílá transakční e-maily: každý používaný typ zprávy je ověřený skutečným doručením do testovací schránky. Přijetí požadavku odesílací službou není doručení. *Ověření (prohlížeč):* vyvolej používané typy zpráv a zkontroluj příjemce, obsah a funkčnost odkazů v doručených zprávách.

- [ ] Když odeslání e-mailu dočasně selže: zpráva nezmizí a existuje řízený způsob opakování v aplikaci nebo odesílací službě. Trvalé odmítnutí se automaticky neopakuje beze změny požadavku nebo odstranění příčiny. [RFC 5321] [Amazon SES: chyby kvót] *Ověření:* simuluj dočasnou a trvalou chybu odesílání; zkontroluj uložený stav, odpovědnost za opakování a dohledatelný konečný výsledek.

- [ ] Když projekt drží osobní údaje cizích lidí a na e-mailech závisí registrace nebo obnova účtu: dostupná odesílací kapacita pokrývá očekávaný objem zpráv i rychlost odesílání ve špičce. [Amazon SES: kvóty] *Ověření:* porovnej odhad s aktuálními kvótami použité služby a chováním při jejich vyčerpání; u údajů poskytovatele zaznamenej datum ověření. Bez odhadu nebo přístupu ke kvótám napiš „Otázka“ nebo „Ověř ručně“.

## Platby

Základ tvoří [OWASP Payment Gateway Integration](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Payment_Gateway_Integration_Cheat_Sheet.html), [Webhook Security](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html) a [Business Logic Security](https://cheatsheetseries.owasp.org/cheatsheets/Business_Logic_Security_Cheat_Sheet.html).

- [ ] Když aplikace přijímá platby: výslednou částku počítá server z důvěryhodných údajů. [OWASP Payment Gateway] *Ověření:* v požadavku změň cenu, množství nebo slevu; ověř, že se účtovaná částka řídí serverovými pravidly.

- [ ] Když aplikace označí objednávku jako zaplacenou: rozhodne podle ověřeného serverového potvrzení odpovídající objednávky, částky, měny a konečného stavu platby. [OWASP Payment Gateway] *Ověření:* podvrhni návratovou URL a zkus potvrzení jiné objednávky, jiné částky a nedokončené platby; nesmí vzniknout zaplacená objednávka.

- [ ] Když se opakuje požadavek na vytvoření téže platby: nevznikne další účtování. *Ověření:* zopakuj požadavek po simulovaném timeoutu i souběžně; porovnej vzniklé platební operace. Podklad pro bezpečné opakování: [dokumentace idempotentních požadavků](https://docs.stripe.com/api/errors#idempotent_requests).

- [ ] Když stejné potvrzení platby přijde opakovaně nebo souběžně: plnění se provede pouze jednou. [OWASP Webhook Security] *Ověření:* doruč stejnou událost opakovaně i souběžně; zkontroluj objednávky, připsané kredity, zpřístupnění produktu a další vedlejší účinky.

- [ ] Když zpracování platební události selže: potvrzení úspěšného přijetí se odešle až po trvalém uložení události nebo dokončení jejího zpracování. [OWASP Webhook Security] *Ověření:* simuluj chybu úložiště; událost musí zůstat dostupná k opakování u odesílatele nebo v trvalé frontě.

- [ ] Když se platební událost opozdí nebo nedorazí: stav objednávky lze opravit podle ověřeného aktuálního stavu platby. Starší událost nesmí přepsat novější stav. [OWASP Webhook Security] *Ověření:* změň pořadí událostí, jednu vynech a spusť dohledání nebo opakované doručení.

- [ ] Když aplikace poskytuje předplatné: přístup odpovídá ověřenému stavu předplatného a pravidlům produktu pro zaplacené období, zkušební dobu a prodlení. [Stripe: předplatné] *Ověření:* v testovacím režimu projdi používané stavy včetně obnovení, neúspěšné platby a ukončení; porovnej účtování a stav předplatného s oprávněním používat službu.

- [ ] Když aplikace umožňuje zrušení předplatného: potvrzené zrušení skutečně zastaví další obnovování u platebního systému podle potvrzeného data ukončení. [Stripe: zrušení] *Ověření:* zruš testovací předplatné a přes API ověř okamžité ukončení nebo naplánované ukončení bez dalšího obnovení; samotná změna příznaku v aplikaci nestačí.

- [ ] Když aplikace přijímá platby kartou: po autorizaci neuchovává CVV/CVC ani v logu. Zákaz platí i pro šifrovanou hodnotu a opakované platby. *Ověření:* projdi platební formulář, serverové zpracování, logování a datový model; hledej případné ukládání těchto polí. Podklad: [PCI SSC FAQ 1280](https://www.pcisecuritystandards.org/faqs/1280/), stav 10/2026.

## Nahrávání souborů

Kontroly vycházejí z [OWASP File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

- [ ] Když nahrané soubory nejsou veřejné: stažení respektuje oprávnění i při přímém přístupu do úložiště. Podepsaný odkaz může po omezenou dobu sám opravňovat ke stažení, proto ho aplikace vydává jen oprávněnému žadateli. [OWASP File Upload] [Amazon S3: podepsané odkazy] *Ověření:* zkus přímou URL úložiště bez oprávnění a získání odkazu pod cizím účtem; u podepsaného odkazu ověř omezení na určený soubor a odmítnutí nového požadavku po expiraci.

## Zpracování chyb

Podkladem jsou [OWASP Error Handling](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html) a [REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html).

- [ ] Když načtení dat selže kvůli chybě serveru nebo síťovému výpadku: aplikace chybu nezamění za prázdný výsledek ani za odhlášení při jinak platné relaci. [RFC 9110] *Ověření (prohlížeč):* simuluj odpověď datového API se stavem `500` a samostatně síťový timeout; ověř odlišný chybový stav a zachování přihlášení.

## Texty v rozhraní

- [ ] Když rozhraní zobrazuje počet: tvar slova odpovídá českému skloňování. Čeština má pro celá čísla tři tvary, „1 položka“, „2 položky“, „5 položek“, a nula má tvar jako pět. Text skládaný jako „{n} položek“ je chybně u 1 až 4. [CLDR Plural Rules] *Ověření:* v kódu najdi texty skládané s číslem a ověř, že tvar vybírají pravidla množného čísla pro češtinu podle CLDR; vyzkoušej hodnoty 0, 1, 2, 5 a desetinné číslo.

## Mazání účtu a osobních údajů

Právní základ tvoří [GDPR, zejména články 12, 17 a 19](https://eur-lex.europa.eu/eli/reg/2016/679/oj?locale=cs), stav 10/2026. Praktické problémy výmazu a záloh popisuje [EDPB ve zprávě z roku 2026](https://www.edpb.europa.eu/system/files/2026-02/edpb_cef-report_2025_right-to-erasure_en.pdf).

- [ ] Když projekt má uživatelské účty a na zpracování se vztahuje GDPR: existuje funkční cesta k podání žádosti o výmaz osobních údajů. Samotné zrušení účtu nemusí znamenat výmaz dat a automatické tlačítko není jediná přípustná možnost podání žádosti. [GDPR] [EDPB: práva] *Ověření (prohlížeč):* testovacím účtem najdi uvedený kontakt nebo formulář, podej testovací žádost a ověř její přijetí k vyřízení.

- [ ] Když projekt drží osobní údaje cizích lidí a účet se zruší: jeho přístup k aplikaci přestane fungovat i v existujících relacích. [OWASP Session Management] *Ověření:* po zrušení testovacího účtu zopakuj chráněné požadavky se starými přihlašovacími a obnovovacími tokeny.

- [ ] Když po výmazu zůstávají některé osobní údaje a na zpracování se vztahuje GDPR: u každé ponechané skupiny je doložený důvod a lhůta uchování nebo kritéria jejího určení. Účetní povinnost neospravedlňuje ponechání celého profilu. [GDPR] [EDPB: výmaz 2026] *Ověření:* porovnej ponechaná pole a pravidla jejich odstranění s evidovanými účely, právními důvody a lhůtami nebo kritérii uchování.

## Zdroje

- [OWASP Authentication Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html) - přihlášení a nové ověření identity.
- [OWASP Forgot Password Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) - tokeny, obnova a relace.
- [OWASP Email Validation and Verification](https://cheatsheetseries.owasp.org/cheatsheets/Email_Validation_and_Verification_Cheat_Sheet.html) - ověření a změna adresy.
- [OWASP Multifactor Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html) - ochrana citlivých účtů.
- [OWASP OAuth2](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html) - navázání odpovědi na přihlašovací pokus.
- [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html) - vznik, expirace a rušení relací.
- [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) - serverové kontroly oprávnění.
- [OWASP Mass Assignment](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html) - ochrana uživatelem neměnitelných polí.
- [Google: Email sender guidelines](https://support.google.com/mail/answer/81126?hl=en) - autentizace odesílatele a doručování, stav 10/2026.
- [RFC 5321](https://www.rfc-editor.org/rfc/rfc5321.html) - dočasné a trvalé chyby doručení, odpovědnost za opakování.
- [OWASP Third Party Payment Gateway Integration](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Payment_Gateway_Integration_Cheat_Sheet.html) - potvrzení platby a kontrola objednávky.
- [OWASP Webhook Security](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html) - autenticita, duplicity, pořadí a spolehlivé přijetí událostí.
- [OWASP Business Logic Security](https://cheatsheetseries.owasp.org/cheatsheets/Business_Logic_Security_Cheat_Sheet.html) - stavové přechody, souběh a obchodní pravidla.
- [Stripe: Idempotent requests](https://docs.stripe.com/api/errors#idempotent_requests) - konkrétní dokumentovaný mechanismus bezpečného opakování; nenahrazuje dokumentaci použitého platebního systému.
- [PCI SSC FAQ 1280](https://www.pcisecuritystandards.org/faqs/1280/) - zákaz uchování CVV/CVC po autorizaci, stav 10/2026.
- [OWASP File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html) - validace, ukládání a zpřístupnění souborů.
- [OWASP Error Handling](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html) a [REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html) - chybové odpovědi a bezpečné selhání.
- [GDPR, české znění](https://eur-lex.europa.eu/eli/reg/2016/679/oj?locale=cs) - články 12, 17 a 19, stav 10/2026.
- [EDPB FAQ](https://www.edpb.europa.eu/contact/frequently-asked-questions_en) - lhůty a výjimky práva na výmaz.
- [EDPB: Coordinated Enforcement Action 2025, Right to Erasure, zpráva 2026](https://www.edpb.europa.eu/system/files/2026-02/edpb_cef-report_2025_right-to-erasure_en.pdf) - praktické provedení výmazu včetně záloh.
- [Amazon SES: Sending quota errors](https://docs.aws.amazon.com/ses/latest/dg/manage-sending-quotas-errors.html) - příklad odmítnutí před přijetím zprávy a nutnosti opakování na straně aplikace.
- [Amazon SES: Sending quotas](https://docs.aws.amazon.com/ses/latest/dg/manage-sending-quotas.html) - rozlišení objemové kvóty a rychlosti odesílání; konkrétní limity ověř u použité služby.
- [Stripe: Subscription webhooks](https://docs.stripe.com/billing/subscriptions/webhooks) - vazba přístupu na stav předplatného včetně zkušební doby a selhání platby.
- [Stripe: Cancel subscriptions](https://docs.stripe.com/billing/subscriptions/cancel) - okamžité a naplánované ukončení předplatného.
- [Amazon S3: Presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html) - příklad časově omezeného oprávnění samotným držením podepsaného odkazu.
- [WCAG 2.2.5: Re-authenticating](https://www.w3.org/WAI/WCAG22/Understanding/re-authenticating.html) - zachování dat po vypršení relace.
- [Unicode CLDR: Language Plural Rules](https://www.unicode.org/cldr/charts/latest/supplemental/language_plural_rules.html) - kategorie množného čísla pro češtinu; v JavaScriptu je zpřístupňuje [`Intl.PluralRules`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/PluralRules).
- [RFC 9110, kapitola 15](https://www.rfc-editor.org/rfc/rfc9110.html#section-15) - rozlišení chyb autentizace a serverových chyb.
- [EDPB: Respect individuals’ rights](https://www.edpb.europa.eu/sme/be-compliant/respect-individuals-rights_en) - usnadnění podání žádosti o výmaz a podmínky jejího vyřízení.

[OWASP Email Verification]: https://cheatsheetseries.owasp.org/cheatsheets/Email_Validation_and_Verification_Cheat_Sheet.html
[OWASP Forgot Password]: https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html
[OWASP Authentication]: https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
[OWASP Authorization]: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
[OWASP Session Management]: https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html
[RFC 5321]: https://www.rfc-editor.org/rfc/rfc5321.html
[Amazon SES: chyby kvót]: https://docs.aws.amazon.com/ses/latest/dg/manage-sending-quotas-errors.html
[Amazon SES: kvóty]: https://docs.aws.amazon.com/ses/latest/dg/manage-sending-quotas.html
[OWASP Payment Gateway]: https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Payment_Gateway_Integration_Cheat_Sheet.html
[OWASP Webhook Security]: https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html
[Stripe: předplatné]: https://docs.stripe.com/billing/subscriptions/webhooks
[Stripe: zrušení]: https://docs.stripe.com/billing/subscriptions/cancel
[OWASP File Upload]: https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html
[Amazon S3: podepsané odkazy]: https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html
[RFC 9110]: https://www.rfc-editor.org/rfc/rfc9110.html#section-15
[CLDR Plural Rules]: https://www.unicode.org/cldr/charts/latest/supplemental/language_plural_rules.html
[GDPR]: https://eur-lex.europa.eu/eli/reg/2016/679/oj?locale=cs
[EDPB: práva]: https://www.edpb.europa.eu/sme/be-compliant/respect-individuals-rights_en
[EDPB: výmaz 2026]: https://www.edpb.europa.eu/system/files/2026-02/edpb_cef-report_2025_right-to-erasure_en.pdf
