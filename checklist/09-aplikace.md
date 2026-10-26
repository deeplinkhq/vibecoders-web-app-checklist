# Aplikace

**Týká se:** aplikace s přihlášením, uživatelskými rolemi, transakčními e-maily, platbami nebo nahráváním souborů. Jednotlivé části přeskoč, když danou funkci aplikace nemá.

Aktivní kontroly prováděj s testovacími účty a daty v odděleném prostředí. Platby zkoušej v testovacím režimu. Čtení kódu neprokazuje doručení e-mailu ani skutečné zneplatnění relace. Bez potřebného přístupu napiš „Ověř ručně“ a uveď konkrétní chybějící kontrolu.

## Přihlášení a obnova účtu

Kontroly vycházejí z doporučení OWASP pro [přihlašování](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), [obnovu hesla](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) a [ověřování e-mailové adresy](https://cheatsheetseries.owasp.org/cheatsheets/Email_Validation_and_Verification_Cheat_Sheet.html).

- [ ] Když aplikace umožňuje registraci: nový uživatel dokončí registraci až k přístupu do svého účtu. Samotná úspěšná odpověď registračního API nestačí. *Ověření (prohlížeč):* založ testovací účet, dokonči požadované ověření a otevři jeho soukromou část.

- [ ] Když aplikace používá e-mail jako ověřenou identitu: neověřená adresa nezíská oprávnění vázaná na její vlastnictví. Týká se například přijetí pozvánky pro konkrétní adresu. *Ověření:* s neověřeným testovacím účtem zavolej přímo příslušné API; server musí akci odmítnout.

- [ ] Když aplikace umožňuje reset hesla: uživatel dokončí obnovu přes doručený e-mail a přihlásí se novým heslem. *Ověření (prohlížeč):* proveď obnovu testovacího účtu od žádosti přes odkaz ve schránce až po nové přihlášení; původní heslo musí přestat fungovat.

- [ ] Když aplikace používá ověřovací nebo obnovovací tokeny: server přijme jen nepředvídatelný, neprošlý token určený pro daný účet a účel; jednorázový token nepřijme podruhé. *Ověření:* projdi generování a validaci tokenů; otestuj změněný, prošlý, již použitý token a záměnu jeho účelu.

- [ ] Když aplikace nabízí přihlášení nebo obnovu účtu: veřejná odpověď neprozrazuje existenci účtu. Rozdíl nesmí být jen přesunutý do HTTP statusu nebo zjevně odlišné doby odpovědi. *Ověření:* porovnej odpovědi pro existující a neexistující účet včetně statusu, těla a opakovaných měření času.

- [ ] Když uživatel mění přihlašovací údaje nebo maže účet: aplikace znovu ověří jeho identitu. Samotná dlouhodobě otevřená relace nestačí. *Ověření:* v existující relaci vyvolej změnu hesla, e-mailu nebo smazání účtu; zkontroluj serverové vynucení nového ověření.

- [ ] Když uživatel mění přihlašovací e-mail: nová adresa se aktivuje až po ověření jejího vlastnictví. *Ověření:* před potvrzením nové adresy zkus její použití pro přihlášení nebo obnovu účtu; ověř, že server změnu drží jako nepotvrzenou.

- [ ] Když uživatel mění přihlašovací e-mail: na původní adresu přijde upozornění na změnu. Pomůže odhalit převzetí účtu. *Ověření (prohlížeč):* změň adresu testovacího účtu a zkontroluj zprávu v původní schránce.

- [ ] Když aplikace má administrátory s přístupem k cizím datům nebo penězům: jejich přihlášení vyžaduje vícefaktorové ověření. *Ověření:* projdi pravidla přihlášení a testovacím administrátorem zkus vstup bez druhého faktoru. Podklad: [OWASP MFA](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html).

- [ ] Když aplikace používá přihlášení přes externí identitu: callback přijme jen odpověď navázanou na zahájený přihlašovací pokus. *Ověření:* zkontroluj validaci podle použitého protokolu, včetně `state`, `nonce` nebo PKCE; opakovaný callback a odpověď z jiného pokusu musí být odmítnuty. Podklad: [OWASP OAuth2](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html).

## Správa relací

Pravidla vycházejí z [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html).

- [ ] Když aplikace udržuje přihlášení: server vynucuje stanovenou dobu nečinnosti a nejdelší dobu relace do nového ověření. Hodnoty odpovídají citlivosti aplikace a zahrnují i obnovování tokenů. *Ověření:* najdi obě hodnoty a testem překroč jejich hranice; samotný časovač v prohlížeči nestačí.

- [ ] Když se uživatel přihlásí nebo získá vyšší oprávnění: původní anonymní či méně privilegovanou relaci nelze převzít jako novou privilegovanou relaci. *Ověření:* porovnej identifikátory relací před změnou a po ní; zkus původní identifikátor podvrhnout jinému klientovi.

- [ ] Když se uživatel odhlásí: původní přihlašovací údaje relace přestanou fungovat na serveru. Smazání cookie v prohlížeči nestačí. *Ověření:* před odhlášením zachyť testovací cookie nebo token; po odhlášení jimi zopakuj chráněný požadavek včetně pokusu o obnovení přihlášení.

- [ ] Když uživatel obnoví heslo: existující relace lze zneplatnit; při obnově po podezření na převzetí účtu se zneplatní všechny. *Ověření:* otevři účet ve dvou klientech, proveď příslušnou obnovu a zopakuj požadavky se starými relacemi i obnovovacími tokeny. Podklad také: [OWASP Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html).

## Role a oprávnění

Podkladem jsou [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) a ochrana před [mass assignment](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html).

- [ ] Když aplikace omezuje přístup: server ověřuje oprávnění při každé chráněné operaci a bez výslovného povolení přístup zamítne. Skryté tlačítko není kontrola oprávnění. *Ověření:* sestav přehled chráněných operací a povolených rolí; každou operaci zavolej přímo bez oprávnění, včetně alternativních endpointů.

- [ ] Když aplikace odděluje uživatele nebo organizace: oprávnění se kontroluje ke konkrétnímu objektu i organizaci. *Ověření:* dvěma testovacími účty zkus cizí identifikátor při čtení, změně, mazání a exportu; zahrň hromadné operace.

- [ ] Když uživatel upravuje svůj profil nebo jiné záznamy: vstupem nemůže změnit chráněná pole, například roli, vlastníka nebo organizaci. *Ověření:* přidej tato pole do registračních a aktualizačních požadavků; ověř nezměněný uložený stav.

- [ ] Když administrátor odebere roli, členství nebo zablokuje účet: odebrané oprávnění přestane platit i pro již přihlášeného uživatele. *Ověření:* po odebrání zopakuj chráněnou operaci se starou relací; nespoléhej na nové přihlášení nebo obnovení stránky.

## Transakční e-maily

Ověření odesílatele vychází z [doporučení pro doručování do Gmailu](https://support.google.com/mail/answer/81126?hl=en), opakování doručení z [RFC 5321](https://www.rfc-editor.org/rfc/rfc5321.html). Zde požadované SPF, DKIM a DMARC jsou doporučený základ, nikoli tvrzení, že každá schránka vyžaduje všechny tři mechanismy.

- [ ] Když aplikace posílá e-maily: používá doménu pod kontrolou provozovatele s funkčním SPF, DKIM a DMARC alignment. Samotná existence DNS záznamů nestačí. *Ověření:* přes `dig` zkontroluj záznamy a v důvěryhodných hlavičkách skutečně doručené zprávy výsledky SPF, DKIM a DMARC. Stav doporučení: 10/2026.

- [ ] Když aplikace posílá odkazy pro práci s účtem: cílová adresa odpovídá prostředí a vzniká z důvěryhodné konfigurace. Nesmí ji podvrhnout hlavička požadavku. *Ověření:* zkontroluj generování URL a zprávy v testovací schránce; požadavek s cizí hlavičkou `Host` nesmí vytvořit odkaz na cizí doménu. Podklad: [OWASP Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html).

- [ ] Když běží vývojové nebo testovací prostředí: e-maily mohou odejít pouze na určené testovací adresy nebo do zachytávací schránky. *Ověření:* projdi omezení příjemců a úlohy na pozadí; pokus o jiného příjemce musí být bezpečně zachycen.

- [ ] Když aplikace posílá transakční e-maily: každý používaný typ zprávy je ověřený skutečným doručením do testovací schránky. Přijetí požadavku odesílací službou není doručení. *Ověření (prohlížeč):* vyvolej používané typy zpráv a zkontroluj příjemce, obsah a funkčnost odkazů v doručených zprávách.

- [ ] Když odeslání e-mailu dočasně selže: zpráva nezmizí a existuje řízený způsob opakování. Trvalé odmítnutí se neopakuje bez omezení. *Ověření:* simuluj dočasnou a trvalou chybu odesílání; zkontroluj uložený stav, opakování a dohledatelný konečný výsledek.

- [ ] Když na e-mailech závisí registrace nebo obnova účtu: dostupná odesílací kapacita pokrývá očekávanou špičku. *Ověření:* porovnej odhad špičky s aktuální kvótou a chováním při jejím vyčerpání; u údajů poskytovatele zaznamenej datum ověření. Bez odhadu nebo přístupu ke kvótě napiš „Otázka“ nebo „Ověř ručně“.

## Platby

Základ tvoří [OWASP Payment Gateway Integration](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Payment_Gateway_Integration_Cheat_Sheet.html), [Webhook Security](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html) a [Business Logic Security](https://cheatsheetseries.owasp.org/cheatsheets/Business_Logic_Security_Cheat_Sheet.html).

- [ ] Když aplikace přijímá platby: vývojové a testovací prostředí nemůže vytvořit skutečné účtování. *Ověření:* zkontroluj použitý režim a konfiguraci všech platebních cest včetně úloh na pozadí; proveď testovací platbu.

- [ ] Když aplikace přijímá platby: výslednou částku počítá server z důvěryhodných údajů. *Ověření:* v požadavku změň cenu, množství nebo slevu; ověř, že se účtovaná částka řídí serverovými pravidly.

- [ ] Když aplikace označí objednávku jako zaplacenou: rozhodne podle ověřeného serverového potvrzení odpovídající objednávky, částky, měny a konečného stavu platby. *Ověření:* podvrhni návratovou URL a zkus potvrzení jiné objednávky, jiné částky a nedokončené platby; nesmí vzniknout zaplacená objednávka.

- [ ] Když aplikace přijímá platební webhooky: před zpracováním ověří jejich autenticitu podle dokumentace odesílatele. *Ověření:* odešli událost bez ověření, s chybným ověřením a se změněným tělem; žádná nesmí změnit objednávku.

- [ ] Když se opakuje požadavek na vytvoření téže platby: nevznikne další účtování. *Ověření:* zopakuj požadavek po simulovaném timeoutu i souběžně; porovnej vzniklé platební operace. Podklad pro bezpečné opakování: [dokumentace idempotentních požadavků](https://docs.stripe.com/api/errors#idempotent_requests).

- [ ] Když stejné potvrzení platby přijde opakovaně nebo souběžně: plnění se provede pouze jednou. *Ověření:* doruč stejnou událost opakovaně i souběžně; zkontroluj objednávky, připsané kredity, zpřístupnění produktu a další vedlejší účinky.

- [ ] Když zpracování platební události selže: potvrzení úspěšného přijetí se odešle až po trvalém uložení události nebo dokončení jejího zpracování. *Ověření:* simuluj chybu úložiště; událost musí zůstat dostupná k opakování u odesílatele nebo v trvalé frontě.

- [ ] Když se platební událost opozdí nebo nedorazí: stav objednávky lze opravit podle ověřeného aktuálního stavu platby. Starší událost nesmí přepsat novější stav. *Ověření:* změň pořadí událostí, jednu vynech a spusť dohledání nebo opakované doručení.

- [ ] Když aplikace poskytuje předplatné: přístup odpovídá ověřenému stavu a zaplacenému období podle pravidel produktu. *Ověření:* v testovacím režimu projdi obnovení, neúspěšnou platbu a ukončení; porovnej účtování s oprávněním používat službu.

- [ ] Když aplikace umožňuje zrušení předplatného: potvrzené zrušení skutečně zastaví další obnovování u platebního systému. *Ověření:* zruš testovací předplatné a ověř jeho stav přes API; samotná změna příznaku v aplikaci nestačí.

- [ ] Když aplikace přijímá platby kartou: po autorizaci neuchovává CVV/CVC ani v logu. Zákaz platí i pro šifrovanou hodnotu a opakované platby. *Ověření:* projdi platební formulář, serverové zpracování, logování a datový model; hledej případné ukládání těchto polí. Podklad: [PCI SSC FAQ 1280](https://www.pcisecuritystandards.org/faqs/1280/), stav 10/2026.

## Nahrávání souborů

Kontroly vycházejí z [OWASP File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

- [ ] Když aplikace přijímá soubory: server povolí jen potřebné typy ověřené podle jejich obsahu. Přípona ani klientský `Content-Type` nestačí. *Ověření:* odešli přejmenovaný nepovolený soubor a podvržený MIME typ; musí být odmítnuty.

- [ ] Když aplikace přijímá soubory: server vynucuje stanovený limit jejich velikosti. *Ověření:* najdi limit a otestuj soubor pod ním i nad ním; kontrola pouze ve formuláři nestačí.

- [ ] Když aplikace přijímá soubory: uživatelský název neurčuje cestu k uložení ani nepřepíše jiný soubor. *Ověření:* otestuj shodné názvy a cestu obsahující `../`; zkontroluj výsledné uložení.

- [ ] Když nahrané soubory nejsou veřejné: stažení respektuje oprávnění i při přímém přístupu do úložiště. *Ověření:* vyzkoušej URL bez přihlášení, pod cizím účtem a po expiraci případného podepsaného odkazu.

- [ ] Když aplikace zpřístupňuje nahrané soubory: jejich obsah se nemůže spustit s oprávněními aplikace. *Ověření:* zkontroluj způsob servírování aktivních formátů; neškodným testem ověř, že soubor nezíská přístup k relaci aplikace.

## Zpracování chyb

Podkladem jsou [OWASP Error Handling](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html) a [REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html).

- [ ] Když hlavní akce selže: uživatel dostane srozumitelnou informaci o výsledku a dalším kroku. *Ověření (prohlížeč):* simuluj odmítnutí požadavku, výpadek spojení a chybu serveru; zkontroluj výsledný stav obrazovky.

- [ ] Když načtení dat selže: aplikace chybu nezamění za prázdný výsledek ani za odhlášení. *Ověření:* simuluj chybu datového API při platné relaci; ověř odlišný chybový stav a zachování identity uživatele.

- [ ] Když kontrola identity nebo oprávnění selže kvůli chybě závislosti: chráněná operace se nepovolí. *Ověření:* simuluj nedostupnost potřebné závislosti; ověř zamítnutí operace a nezměněná chráněná data.

## Mazání účtu a osobních údajů

Právní základ tvoří [GDPR, zejména články 12, 17 a 19](https://eur-lex.europa.eu/eli/reg/2016/679/oj?locale=cs). Praktické problémy výmazu a záloh popisuje [EDPB ve zprávě z roku 2026](https://www.edpb.europa.eu/system/files/2026-02/edpb_cef-report_2025_right-to-erasure_en.pdf).

- [ ] Když aplikace spravuje osobní účty: existuje funkční cesta ke zrušení účtu nebo podání žádosti o výmaz. Automatické tlačítko není jediná přípustná možnost. *Ověření (prohlížeč):* testovacím účtem projdi uvedený postup až k přijetí žádosti nebo dokončení zrušení.

- [ ] Když se účet zruší: jeho přístup k aplikaci přestane fungovat i v existujících relacích. *Ověření:* po zrušení testovacího účtu zopakuj chráněné požadavky se starými přihlašovacími a obnovovacími tokeny.

- [ ] Když aplikace provádí výmaz: odstraní osobní údaje bez dalšího právního důvodu i z navázaných aktivních systémů. Nestačí smazat řádek uživatele nebo nastavit příznak „smazáno“. *Ověření:* podle mapy dat dohledávej testovací identitu v databázi, souborech a u zpracovatelů; ověř dokončení jednotlivých kroků.

- [ ] Když po výmazu zůstávají některé osobní údaje: u každé skupiny je doložený důvod a konec uchování. Účetní povinnost neospravedlňuje ponechání celého profilu. *Ověření:* porovnej ponechaná pole a pravidla jejich odstranění s evidovanými účely a lhůtami.

- [ ] Když jsou osobní údaje v zálohách: existuje stanovený postup jejich zániku a ochrana před návratem vymazaných údajů do aktivního provozu. *Ověření:* zkontroluj životnost záloh a postup obnovy; při zkušební obnově ověř opětovné uplatnění výmazů.

- [ ] Když přijde žádost o výmaz: proces sleduje její přijetí a odpověď bez zbytečného odkladu, nejpozději do jednoho měsíce. Případné prodloužení o další dva měsíce vyžaduje důvod a oznámení během prvního měsíce. *Ověření:* projdi evidenci a eskalaci testovací žádosti. Podklad: [EDPB FAQ](https://www.edpb.europa.eu/contact/frequently-asked-questions_en), stav 10/2026.

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
