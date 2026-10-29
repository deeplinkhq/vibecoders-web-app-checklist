# Obsah webu nebo landing page

**Týká se:** každého webu. U aplikace hlavně veřejných stránek (úvodní stránka, registrace).

## Obsah

- [ ] Stránka má jeden cíl, jednu hlavní konverzi. Ne tři soupeřící.
- [ ] Je jasné, komu je web určený a kde ti lidé jsou.
- [ ] Hlavní akce je vidět z každého místa stránky, v navigaci nebo jako tlačítko, které jede s obsahem. [Sticky hlavičky NN/g]

## Struktura

- [ ] Landing page má 7 až 9 sekcí, ne víc. Každá sekce si musí zasloužit další scroll.
- [ ] Pořadí, které funguje: úvod, problém, jak to funguje, co nabízíš, důvěra, kdo za tím stojí, otázky a námitky, závěrečná výzva k akci.
- [ ] Když jde o službu, kterou lidé neznají: sekce „Jak to funguje" v několika krocích je vysoko. Hlavní bariéra je nepochopení, ne cena.

## Úvodní sekce (hero)

- [ ] Do 5 sekund odpovídá na tři otázky: co to je, je to pro mě, co mám udělat. Tímhle testem projde zhruba 14 % landing pages. [Úvodní stránka NN/g]
- [ ] Nad zlomem je nadpis, jedna až dvě věty pod ním, jeden vizuál a jedno tlačítko. Nic víc.
- [ ] Žádný slider, žádné video, které se samo spouští, žádná stock fotka lidí u notebooku. [Karusely NN/g], [Pohyb WCAG], [Fotky NN/g]
- [ ] Na mobilu se do prvního okna vejde nadpis, věta a tlačítko. Vizuál klidně až pod ně. [Pozornost a scrollování NN/g]
- [ ] Žádné vyskakovací okno nezakryje hlavní obsah hned po příchodu nebo během čtení, hlavně na mobilu. Google takové stránky může ve výsledcích znevýhodnit (stav 10/2026). Výjimkou je cookie lišta, ověření věku a přihlášení k neveřejnému obsahu. [Vyskakovací okna Google] *Ověření (prohlížeč):* otevři hlavní vstupní stránky v čisté relaci na mobilním viewportu, chvíli roluj a zaznamenej každé okno nebo banner, který zakryje většinu obsahu; u každého zjisti, jestli spadá pod výjimku.

## Nadpis

- [ ] 6 až 12 slov. Kratší nesdělí hodnotu, delší se nepřečte za dvě sekundy.
- [ ] Konkrétní, ne aspirativní. Test: řekl by tuhle větu člověk nahlas? [Psaní pro web NN/g]
- [ ] Žádné „inovativní", „revoluční", „měníme způsob, jakým…". [Psaní pro web NN/g]

## Výzva k akci (CTA)

- [ ] Jeden cíl, ale 3 až 5 opakování téhož tlačítka: v úvodu, po „jak to funguje", po sekci důvěry, na konci, na mobilu přilepené dole.
- [ ] Text tlačítka dokončuje větu „Chci…", není to povel. „Chci se přidat", ne „Odeslat".
- [ ] Pod tlačítkem stojí, co se stane potom. „Zdarma a nezávazně, ozveme se do dvou dnů." [Get Started NN/g]
- [ ] Nejvýš jedno vedlejší tlačítko a vizuálně slabší než hlavní. [Stavy tlačítek NN/g]
- [ ] Po provedení akce vizuální konfirmace a co se stane ("Kdy odpovíme") [Stav systému NN/g]

## Důvěra

- [ ] Aspoň tři různé typy důkazu. Jeden citát nestačí.
- [ ] Reálné číslo, i malé. Malé pravdivé číslo je věrohodnější než žádné.
- [ ] Je vidět, kdo za tím stojí, s fotkou a jménem. [Fotky NN/g]
- [ ] Fotky reálných věcí, lidí a míst, ne fotobanka. [Fotky NN/g]
- [ ] Žádné vymyšlené reference, recenze ani „1000+ spokojených zákazníků". Smyšlené recenze jsou v ČR klamavá reklama. Vždy vycházet z pravdivých dat která mohu podložit [Recenze ČOI], [Zákon o ochraně spotřebitele]
- [ ] U referencí a recenzí uvádět autora, odkaz na web/LinkedIn - pouze s jeho souhlasem

## Námitky

- [ ] FAQ - Otázky a odpovědi: 5 až 8 otázek formulovaných jazykem návštěvníka odpovídající na nejčastější otázky, které by zákazník mohl mít [FAQ NN/g]
- [ ] Cena je veřejná nebo je uvedeno, jak ji zákazník získá. Chybějící cena je nejčastější důvod odchodu. Chybějící cena při nabízení koncovému zákazníkovi (ne firmě) je protiprávní [Důvěryhodnost NN/g], [Informace prodejce ČOI]
- [ ] Je napsané i to, co neděláš. Vymezení zvyšuje důvěryhodnost.
- [ ] Když jde o službu vázanou na místo: lokalita je uvedená konkrétně, čtvrtí nebo ulicemi, ne jen „Praha".

## Kontakty a údaje

- [ ] Telefon a e-mail na webu jsou klikací odkazy `tel:` a `mailto:`. Na mobilu je zavolání jedním klepnutím často hlavní konverze. Číslo v odkazu je v mezinárodním tvaru bez mezer, `tel:+420` a devět číslic. [RFC 3966], [MDN a] *Ověření:* najdi v HTML telefonní čísla a e-mailové adresy zobrazené jako text a ověř, že každé má odkaz se stejnou hodnotou.
- [ ] Když je web česky: ceny, čísla a data jsou v českém formátu. Desetinná čárka, tisíce oddělené mezerou, měna za číslem (`1 234,50 Kč`) a datum jako `29. 10. 2026`. Formáty z anglických šablon (`$`, `1,234.50`, `10/29/2026`) působí cize a datum jde přečíst špatně. [MDN NumberFormat], [MDN DateTimeFormat] *Ověření:* prohledej šablony a vykreslené stránky na měnové symboly, oddělovače a pevně zapsané formáty data; u dynamických hodnot zkontroluj, že formátování používá české národní prostředí `cs-CZ`, ne výchozí anglické.

## Zdroje

Zdroje byly kontrolovány 29. 10. 2026.

- [Sticky hlavičky NN/g] - hlavička, která jede s obsahem, drží hlavní prvky dostupné z celé stránky.
- [Úvodní stránka NN/g] - úvodní stránka má hned říct, kdo jsi, co děláš a co má návštěvník udělat dál.
- [Karusely NN/g] - automaticky se střídající panely snižují viditelnost obsahu a působí jako reklama.
- [Pohyb WCAG] - samo se spouštějící pohyblivý obsah delší než 5 sekund musí jít zastavit.
- [Fotky NN/g] - lidé přehlížejí fotobankové fotky generických lidí, fotky skutečných lidí a věcí si prohlížejí.
- [Pozornost a scrollování NN/g] - obsah v prvním okně dostává 57 % času prohlížení (studie 2018).
- [Vyskakovací okna Google] - překryvná okna a výjimky, stav 10/2026.
- [Psaní pro web NN/g] - objektivní text bez reklamních frází byl o 27 % použitelnější než propagační.
- [Get Started NN/g] - tlačítko má říct, co přesně se po kliknutí stane.
- [Stavy tlačítek NN/g] - hlavní tlačítko má největší vizuální důraz, vedlejší menší.
- [Stav systému NN/g] - systém má uživateli vždy dát zpětnou vazbu, co se stalo.
- [Recenze ČOI], [Zákon o ochraně spotřebitele] - falešné spotřebitelské recenze jsou podle přílohy č. 1 písm. y) a z) zákona č. 634/1992 Sb. vždy klamavou obchodní praktikou.
- [FAQ NN/g] - otázky ve FAQ mají používat slova a formulace návštěvníků.
- [Důvěryhodnost NN/g] - skryté nebo chybějící ceny snižují důvěru, lidé kvůli nim odcházejí.
- [Informace prodejce ČOI] - prodávající musí spotřebitele informovat o ceně před nákupem, případně aspoň odhadem ceny (§ 12 zákona č. 634/1992 Sb., § 13 zákona č. 526/1990 Sb.).
- [RFC 3966] a [MDN a] - odkazy `tel:` a `mailto:`.
- [MDN NumberFormat] a [MDN DateTimeFormat] - formátování čísel, měn a dat podle národního prostředí.

[Sticky hlavičky NN/g]: https://www.nngroup.com/articles/sticky-headers/
[Úvodní stránka NN/g]: https://www.nngroup.com/articles/homepage-design-principles/
[Karusely NN/g]: https://www.nngroup.com/articles/auto-forwarding/
[Pohyb WCAG]: https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html
[Fotky NN/g]: https://www.nngroup.com/articles/photos-as-web-content/
[Pozornost a scrollování NN/g]: https://www.nngroup.com/articles/scrolling-and-attention/
[Vyskakovací okna Google]: https://developers.google.com/search/docs/appearance/avoid-intrusive-interstitials
[Psaní pro web NN/g]: https://www.nngroup.com/articles/concise-scannable-and-objective-how-to-write-for-the-web/
[Get Started NN/g]: https://www.nngroup.com/articles/get-started/
[Stavy tlačítek NN/g]: https://www.nngroup.com/articles/button-states-communicate-interaction/
[Stav systému NN/g]: https://www.nngroup.com/articles/visibility-system-status/
[Recenze ČOI]: https://coi.gov.cz/recenze/
[Zákon o ochraně spotřebitele]: https://e-sbirka.gov.cz/sb/1992/634
[FAQ NN/g]: https://www.nngroup.com/articles/faqs-deliver-value/
[Důvěryhodnost NN/g]: https://www.nngroup.com/articles/trustworthy-design/
[Informace prodejce ČOI]: https://coi.gov.cz/pro-podnikatele/informace-pro-prodejce-zbozi-a-sluzeb/informacni-povinnosti-prodejce-2/
[RFC 3966]: https://www.rfc-editor.org/rfc/rfc3966.html
[MDN a]: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a
[MDN NumberFormat]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat
[MDN DateTimeFormat]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat
