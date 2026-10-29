# Formuláře a vložený obsah

**Týká se:** webu nebo aplikace s formulářem či vloženým obsahem, například mapou, videem, kalendářem, rezervacemi nebo jiným widgetem.

## Pole a instrukce

- [ ] Každé pole má srozumitelný popisek propojený s ovládacím prvkem. U běžných formulářových polí je popisek viditelný i po vyplnění; placeholder ho nenahrazuje. [Popisky WAI] [MDN placeholder] *Ověření:* zkontroluj vazbu `label` a pole nebo odpovídající přístupné pojmenování; pomocí axe vyhledej chybějící popisky a neplatné vazby.

- [ ] Když jednotlivé volby dávají smysl až se společnou otázkou: skupina má programově dostupný název. Samostatné popisky „Ano“ a „Ne“ bez otázky nestačí. [Skupiny WAI] *Ověření:* zkontroluj například `fieldset` s `legend` nebo odpovídající pojmenovanou skupinu v accessibility tree.

- [ ] Povinná pole jsou rozpoznatelná před odesláním vizuálně i programově. Samotná barva povinnost nesděluje. [Instrukce WAI] *Ověření:* porovnej viditelné označení s `required` nebo odpovídajícím stavem přístupnosti a s pravidly backendu.

- [ ] Když pole vyžaduje konkrétní formát nebo má omezující limit: instrukce jsou dostupné před zadáním hodnoty. U příloh uveď povolené typy a maximální velikost. [Instrukce WAI] *Ověření:* porovnej instrukce s implementovanou validací a zkontroluj jejich propojení s polem, například přes `aria-describedby`.

- [ ] Vstupní typ odpovídá zadávaným údajům. Telefon, PSČ a jiné identifikátory nejsou množství určená k aritmetice. [MDN number] [Validace WAI] *Ověření:* projdi `type` a `inputmode`; u telefonu ověř odpovídající telefonní vstup, u číselného identifikátoru zachování počátečních nul.

- [ ] Když formulář sbírá běžné osobní údaje o vyplňujícím: účel polí je označen platnými hodnotami `autocomplete`. Samotné `type="email"` neurčuje, čí e-mail formulář požaduje. [WCAG 1.3.5] *Ověření:* porovnej pole s účely podle WCAG 1.3.5 a zkontroluj například `name`, `email`, `tel` nebo `postal-code`; rozliš i opakující se adresní skupiny.

## Ovládání formulářů a widgetů

- [ ] Když proces znovu vyžaduje údaj, který už uživatel zadal nebo dostal v rámci téhož procesu: nabídne ho předvyplněný nebo k výběru. Výjimkou je nezbytné opakování, bezpečnost nebo údaj, který už není platný. [WCAG 3.3.7] *Ověření (prohlížeč):* projdi všechny kroky včetně návratu zpět a ověř, že stejné platné údaje nemusíš znovu ručně opisovat; zahrň i údaje poskytnuté systémem.

- [ ] Když formulář omezuje dobu vyplňování: splňuje některou možnost WCAG 2.2.1. Limit jde předem vypnout, předem nastavit alespoň na desetinásobek výchozí doby, nebo prodloužit jednoduchou akcí s nejméně 20 sekundami na reakci a alespoň deseti prodlouženími; výjimkou je nezbytný limit, neoddělitelná událost v reálném čase nebo limit delší než 20 hodin. [WCAG 2.2.1] *Ověření:* zkontroluj časovače a expiraci na klientu i serveru a testem s řízeným časem ověř vybranou možnost; případnou výjimku dolož.

## Validace a oprava chyb

Serverová validace vstupů viz [Bezpečnost](08-bezpecnost.md).

- [ ] Validace přijímá platné údaje očekávané cílové skupiny. Neodmítá jméno kvůli diakritice či apostrofu ani podporovaný telefonní formát kvůli mezerám. [OWASP validace] [Validace WAI] *Ověření:* projdi validační pravidla a otestuj reprezentativní platné varianty; omezení na konkrétní zemi nebo formát musí odpovídat skutečnému účelu formuláře.

- [ ] Každá validační chyba je textově popsaná u příslušného pole a programově s ním propojená. Nabízí známý způsob opravy, pokud tím neohrozí bezpečnost nebo účel formuláře; samotný červený rámeček nestačí. [Notifikace WAI] [WCAG 3.3.3] *Ověření (prohlížeč):* vyvolej chyby a zkontroluj text, umístění, přístupný popis a stav neplatného pole; případné vynechání návodu na opravu odůvodni.

- [ ] Po neúspěšném odeslání je cesta k chybám dostupná klávesnicí. Použij například fokus na první chybné pole nebo souhrn chyb s odkazy na pole. [Souhrn chyb GOV.UK] *Ověření (prohlížeč):* odešli neplatný formulář, zjisti polohu fokusu a oprav všechny chyby bez myši.

- [ ] Po validační nebo přenosové chybě zůstávají běžné vyplněné údaje zachované. Výjimky pro citlivé údaje nebo znovuvýběr souboru musí být odůvodněné a vysvětlené. [Chybová hláška GOV.UK] *Ověření (prohlížeč):* vyplň formulář, vyvolej validační chybu a následně chybu přenosu a porovnej hodnoty před a po chybě.

- [ ] Když podání vytváří právní závazek, provádí finanční transakci, mění či maže uložená data ovládaná uživatelem nebo odesílá odpovědi testu: existuje ochrana před chybným potvrzením podle WCAG 3.3.4. Stačí jedna možnost: podání lze vrátit; zadané údaje se kontrolují na vstupní chyby a chyby lze opravit; nebo lze údaje před dokončením zkontrolovat, upravit a potvrdit. [WCAG 3.3.4] *Ověření (prohlížeč):* na testovacích datech zadej chybný údaj a ověř dostupnou cestu opravy nebo vrácení operace; u mazání ověř možnost obnovy nebo potvrzení rozsahu před smazáním.

## Odeslání a potvrzení

- [ ] Během odesílání je zřejmé, že požadavek probíhá, a po jeho skončení je zřejmý výsledek. Samotná animace bez sdělení stavu nestačí; dynamické stavové hlášky, které nepřebírají fokus, jsou programově dostupné asistivním technologiím podle WCAG 4.1.3. [WCAG 4.1.3] *Ověření (prohlížeč):* zpomal odpověď endpointu a projdi čekání, úspěch i chybu; u dynamických hlášek zkontroluj odpovídající role nebo vlastnosti v accessibility tree.

- [ ] Hláška o úspěchu odpovídá skutečně potvrzenému výsledku backendu. Přijetí požadavku ke zpracování není potvrzení doručeného e-mailu ani dokončené rezervace. [RFC 9110 202] *Ověření:* sleduj podmínku zobrazení hlášky a u testovacího podání ji porovnej s odpovědí API a výsledným záznamem nebo přijatou úlohou; HTTP 202 posuzuj jako přijetí ke zpracování.

- [ ] Selhání komunikace nebo backendu nevede k falešnému úspěchu ani nekonečnému čekání. Při neznámém výsledku po přerušení spojení hláška netvrdí, že podání určitě nevzniklo. [MDN fetch] *Ověření (prohlížeč):* otestuj offline stav před odesláním, přerušení během přenosu, HTTP 4xx, HTTP 5xx a neodpovídající endpoint; porovnej chování s nastaveným timeoutem.

- [ ] Při neúspěšném podání je uveden konkrétní další postup. Může to být oprava údaje, pozdější opakování, kontrola stavu podání nebo alternativní kontakt. [Problém se službou GOV.UK] [Potvrzení GOV.UK] *Ověření (prohlížeč):* vyvolej jednotlivé chybové větve a ověř, že jejich instrukce odpovídají příčině a nabízená cesta funguje.

- [ ] Když opakované podání může vytvořit duplicitní rezervaci, objednávku nebo jinou škodlivou operaci: backend umí stejné podání bezpečně rozpoznat. Vypnutí tlačítka v prohlížeči samo nestačí. [RFC 9110 idempotence] *Ověření:* integračním testem zopakuj stejné podání i po simulované ztrátě odpovědi a ověř jediný obchodní výsledek.

- [ ] Když formulář nebo vložený widget posílá e-mail: doručení je ověřené z nasazeného webu až do cílové schránky. Potvrzení od odesílacího systému samo nedokazuje přítomnost zprávy ve schránce. [RFC 5321] *Ověření (člověk):* bez přihlášení provozovatele odešli označené testovací podání a v cílové schránce dohledáš stejný obsah; když proces slibuje potvrzení návštěvníkovi, ověř i jeho doručení.

## Ochrana proti spamu

Serverový limit četnosti podání viz [Bezpečnost](08-bezpecnost.md).

- [ ] Když odeslání vyžaduje anti-bot token: jeho platnost kontroluje backend. Pouhá přítomnost widgetu nebo tokenu v požadavku není důkaz úspěšné kontroly. [OWASP boti] *Ověření:* testem endpointu ověř odmítnutí chybějícího, neplatného a podle použitého protokolu expirovaného či opakovaně použitého tokenu.

- [ ] Když používáš interaktivní CAPTCHA: existuje přístupná cesta dokončení bez stejné smyslové nebo kognitivní překážky. Alternativní varianta stejného obrázkového úkolu tuto podmínku neřeší. [CAPTCHA W3C] *Ověření (člověk):* se čtečkou a bez myši dokonči podání přes dostupnou alternativu; ověř i praktickou použitelnost případného náhradního kontaktu.

- [ ] Když používáš honeypot nebo kontrolu rychlosti vyplnění: neblokují běžné vyplnění ani asistivní technologie. Rychlé doplnění uložených údajů samo neprokazuje bota. [CAPTCHA W3C] [OWASP boti] *Ověření (prohlížeč):* zkontroluj nepřítomnost honeypotu v běžném pořadí fokusu a accessibility tree a odešli formulář po automatickém doplnění údajů.

## Vložené mapy, kalendáře a další widgety

Rezervace prostoru a odložené načítání viz [Rychlost](03-rychlost.md), souhlas před načtením viz [Právo a analytika](07-pravo-a-analytika.md).

- [ ] Když je obsah vložený přes iframe: rám má výstižný přístupný název. Název rozlišuje například mapu provozovny od rezervačního kalendáře. [MDN iframe] *Ověření:* projdi `iframe` v DOM a jejich `title` nebo jiné přístupné pojmenování; zkontroluj i rámy vložené dodatečně skriptem.

- [ ] Podstatná informace nebo akce zůstává dostupná i při nenačtení embedu. U mapy to může být textová adresa, u rezervace funkční samostatná stránka nebo náhradní kontakt. [MDN iframe] [Embedy] *Ověření (prohlížeč):* zablokuj načtení widgetu v rámci stránky a ověř alternativu mimo jeho rám; samostatně simuluj výpadek jeho služby a ověř dostupnost podstatné informace nebo náhradního postupu, který na této službě nezávisí; samotnou událost `load` iframe nepovažuj za důkaz funkčnosti.

- [ ] Když widget závisí na cookies nebo úložišti třetí strany: při jejich blokování funguje nebo nabídne použitelnou alternativní cestu. Návštěvník nesmí zůstat v neřešitelné přihlašovací či potvrzovací smyčce. [Storage Access API] [WebKit ITP] *Ověření (prohlížeč):* v čisté relaci se zapnutým blokováním cookies třetích stran projdi celý proces včetně přesměrování; zaznamenej prohlížeč, verzi a nastavení.

- [ ] Když kalendář nebo rezervace pracuje s konkrétním časem: widget a potvrzení označují stejný okamžik. Převod mezi časovými zónami nesmí změnit skutečný termín. [RFC 5545] *Ověření (prohlížeč):* porovnej vybraný termín s potvrzením při nastavení různých časových zón a pro letní i zimní období; u exportu iCalendar zkontroluj UTC nebo odpovídající časovou zónu.

## Vložená videa

- [ ] Když předtočené video se zvukem předává informace: má synchronizované titulky zachycující řeč i významové zvuky. Výjimku podle WCAG 1.2.2 posuzuj jen u jasně označené mediální alternativy existujícího textu. [WCAG 1.2.2] [Titulky WAI] *Ověření (člověk):* přehraj video bez zvuku a porovnej titulky s původní zvukovou stopou; samotná existence automatických titulků nedokazuje jejich správnost.

## Zdroje

- [W3C WAI: Forms Tutorial](https://www.w3.org/WAI/tutorials/forms/) - omezení požadovaných údajů a základní zásady formulářů.
- [W3C WAI: Labeling Controls](https://www.w3.org/WAI/tutorials/forms/labels/) a [MDN: placeholder](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/placeholder) - popisky, jejich propojení a omezení placeholderu.
- [W3C WAI: Grouping Controls](https://www.w3.org/WAI/tutorials/forms/grouping/) - společné otázky a skupiny ovládacích prvků.
- [W3C WAI: Form Instructions](https://www.w3.org/WAI/tutorials/forms/instructions/) - povinnost, formáty a dostupnost instrukcí.
- [W3C WAI: Validating Input](https://www.w3.org/WAI/tutorials/forms/validation/) - typy vstupů, tolerantní formáty a validace.
- [MDN: input type="number"](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/number) - PSČ a jiné číselné identifikátory nejsou čísla k aritmetice; ověřeno 29. 10. 2026.
- [WCAG 1.3.5: Identify Input Purpose](https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose.html) - programové označení účelu osobních údajů.
- [WCAG 2.1.1: Keyboard](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html), [2.1.2: No Keyboard Trap](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html) a [4.1.2: Name, Role, Value](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html) - ovládání a sémantika widgetů.
- [WCAG 3.3.7: Redundant Entry](https://www.w3.org/WAI/WCAG22/Understanding/redundant-entry) - opakované zadávání údajů a výjimky.
- [WCAG 2.2.1: Timing Adjustable](https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable.html) - časové limity a přesné podmínky prodloužení.
- [OWASP: Input Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html) - serverová validace a přijímání legitimních vstupů.
- [W3C WAI: User Notifications](https://www.w3.org/WAI/tutorials/forms/notifications/) - zpětná vazba a propojení chyb s poli.
- [WCAG 3.3.3: Error Suggestion](https://www.w3.org/WAI/WCAG22/Understanding/error-suggestion.html) - známé způsoby opravy a výjimky kvůli bezpečnosti nebo účelu obsahu.
- [GOV.UK: Error summary](https://design-system.service.gov.uk/components/error-summary/) a [Error message](https://design-system.service.gov.uk/components/error-message/) - navigace k chybám a zachování odpovědí.
- [WCAG 3.3.4: Error Prevention](https://www.w3.org/WAI/WCAG22/Understanding/error-prevention-legal-financial-data.html) - prevence závažných chyb.
- [WCAG 4.1.3: Status Messages](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html) - oznamování dynamických stavů.
- [RFC 9110, oddíl 15.3.3](https://www.rfc-editor.org/rfc/rfc9110.html#section-15.3.3) a [oddíl 9.2.2](https://www.rfc-editor.org/rfc/rfc9110.html#section-9.2.2) - přijetí ke zpracování a bezpečnost opakovaných požadavků.
- [MDN: fetch](https://developer.mozilla.org/en-US/docs/Web/API/Window/fetch) - rozdíl mezi síťovou chybou a HTTP chybovou odpovědí.
- [GOV.UK: Confirmation pages](https://design-system.service.gov.uk/patterns/confirmation-pages/) - potvrzení a další postup.
- [GOV.UK: There is a problem with the service pages](https://design-system.service.gov.uk/patterns/problem-with-the-service-pages/) - další postup a alternativní kontakt při selhání služby.
- [RFC 5321, oddíly 4.2.5 a 6.1](https://www.rfc-editor.org/rfc/rfc5321.html) - přijetí e-mailu a následná selhání doručení.
- [OWASP: Bot Management and Anti-Automation](https://cheatsheetseries.owasp.org/cheatsheets/Bot_Management_and_Anti-Automation_Cheat_Sheet.html) - vrstvená ochrana, rate limiting a kontrola anti-bot tokenů.
- [W3C: Inaccessibility of CAPTCHA](https://www.w3.org/TR/turingtest/) - bariéry CAPTCHA a alternativy; jde o informativní Group Draft Note, nikoli normativní standard.
- [MDN: iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/iframe) - pojmenování rámů, rozměry a omezení událostí `load` a `error`.
- [WCAG 1.4.10: Reflow](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html) - 320 CSS px a výjimky pro dvourozměrný obsah.
- [web.dev: Best practices for using third-party embeds](https://web.dev/articles/embed-best-practices) - rezervace prostoru a odložené načítání.
- [MDN: Storage Access API](https://developer.mozilla.org/en-US/docs/Web/API/Storage_Access_API) a [WebKit: Tracking Prevention](https://webkit.org/tracking-prevention/) - omezení úložišť a cookies třetích stran; chování ověřeno ke stavu 10/2026.
- [ÚOOÚ: Cookies, otázky a odpovědi](https://uoou.gov.cz/verejnost/qa-otazky-a-odpovedi/cookies) - předchozí souhlas, technické výjimky a podobné technologie; stav 10/2026.
- [RFC 5545, oddíl 3.3.5](https://www.rfc-editor.org/rfc/rfc5545.html#section-3.3.5) - časové zóny a rozdíl mezi pevným a „floating“ časem.
- [WCAG 1.2.2: Captions (Prerecorded)](https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html) - titulky předtočeného videa a výjimka pro mediální alternativu textu; ověřeno 29. 10. 2026.
- [W3C WAI: Captions/Subtitles](https://www.w3.org/WAI/media/av/captions/) a [Description of Visual Information](https://www.w3.org/WAI/media/av/description/) - titulky a zvukový popis.
- [WCAG 1.2.1: Audio-only and Video-only](https://www.w3.org/TR/WCAG22/#audio-only-and-video-only-prerecorded) - video zcela bez zvuku.
- [WCAG 1.4.2: Audio Control](https://www.w3.org/WAI/WCAG22/Understanding/audio-control.html) - automatický zvuk delší než 3 sekundy.

[Popisky WAI]: https://www.w3.org/WAI/tutorials/forms/labels/
[MDN placeholder]: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/placeholder
[Skupiny WAI]: https://www.w3.org/WAI/tutorials/forms/grouping/
[Instrukce WAI]: https://www.w3.org/WAI/tutorials/forms/instructions/
[MDN number]: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/number
[Validace WAI]: https://www.w3.org/WAI/tutorials/forms/validation/
[WCAG 1.3.5]: https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose.html
[WCAG 3.3.7]: https://www.w3.org/WAI/WCAG22/Understanding/redundant-entry
[WCAG 2.2.1]: https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable.html
[OWASP validace]: https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html
[Notifikace WAI]: https://www.w3.org/WAI/tutorials/forms/notifications/
[WCAG 3.3.3]: https://www.w3.org/WAI/WCAG22/Understanding/error-suggestion.html
[Souhrn chyb GOV.UK]: https://design-system.service.gov.uk/components/error-summary/
[Chybová hláška GOV.UK]: https://design-system.service.gov.uk/components/error-message/
[WCAG 3.3.4]: https://www.w3.org/WAI/WCAG22/Understanding/error-prevention-legal-financial-data.html
[WCAG 4.1.3]: https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html
[RFC 9110 202]: https://www.rfc-editor.org/rfc/rfc9110.html#section-15.3.3
[RFC 9110 idempotence]: https://www.rfc-editor.org/rfc/rfc9110.html#section-9.2.2
[MDN fetch]: https://developer.mozilla.org/en-US/docs/Web/API/Window/fetch
[Problém se službou GOV.UK]: https://design-system.service.gov.uk/patterns/problem-with-the-service-pages/
[Potvrzení GOV.UK]: https://design-system.service.gov.uk/patterns/confirmation-pages/
[RFC 5321]: https://www.rfc-editor.org/rfc/rfc5321.html
[OWASP boti]: https://cheatsheetseries.owasp.org/cheatsheets/Bot_Management_and_Anti-Automation_Cheat_Sheet.html
[CAPTCHA W3C]: https://www.w3.org/TR/turingtest/
[MDN iframe]: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/iframe
[Embedy]: https://web.dev/articles/embed-best-practices
[Storage Access API]: https://developer.mozilla.org/en-US/docs/Web/API/Storage_Access_API
[WebKit ITP]: https://webkit.org/tracking-prevention/
[RFC 5545]: https://www.rfc-editor.org/rfc/rfc5545.html#section-3.3.5
[WCAG 1.2.2]: https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html
[Titulky WAI]: https://www.w3.org/WAI/media/av/captions/
