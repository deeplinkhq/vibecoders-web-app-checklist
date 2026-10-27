# Rychlost, obrázky a fonty

**Týká se:** každého webu a webové aplikace.

## Jak vyhodnocovat výsledky

Hranice metrik a diagnostická doporučení jsou ověřené k 26. 10. 2026. U Core Web Vitals vyhodnocuj 75. percentil reálných návštěv zvlášť pro mobil a desktop. Zapiš období měření a rozliš data konkrétní URL od dat celého originu. CrUX používá klouzavé období 28 dnů. [Hranice Core Web Vitals](https://web.dev/articles/defining-core-web-vitals-thresholds), [CrUX API](https://developer.chrome.com/docs/crux/api).

Když chybí reprezentativní terénní data, neoznačuj Core Web Vitals jako „OK“ ani automaticky jako „Chybí“. Použij „Ověř ručně“ s poznámkou „nepotvrzeno - chybí terénní data“ a uveď dostupné laboratorní výsledky. Data celého originu nepotvrzují výsledek konkrétní stránky. [PageSpeed Insights: dostupnost a rozsah dat](https://developers.google.com/speed/docs/insights/v5/about).

Orientační práh je podnět k prověření. Překročení dolož konkrétním souborem, požadavkem nebo měřením. Výjimku zdůvodni potřebnou funkcí a výsledkem na cílovém zařízení. Rozliš přenesenou velikost po kompresi od rozbalené velikosti kódu. [Výkonnostní rozpočty](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Performance_budgets).

## Měření a Core Web Vitals

- [ ] [web] Každý odlišný typ stránky má měření produkčního sestavení také v mobilním profilu se zpomaleným připojením a procesorem. Rychlá úvodní stránka nepotvrzuje rychlost detailu, seznamu nebo aplikace. *Ověření:* spusť Lighthouse CLI nebo PageSpeed Insights API pro reprezentativní URL; ulož JSON, datum, verzi nástroje, profil a nastavení zpomalení, měření opakuj a uveď rozptyl výsledků.

- [ ] [web] LCP je nejvýš 2,5 s na 75. percentilu reálných návštěv. Jde o vykreslení největšího způsobilého obsahu ve viewportu, například obrázku, textového bloku nebo videa, ne o dokončení všech požadavků. *Ověření:* načti `record.metrics.largest_contentful_paint.percentiles.p75` z CrUX API v milisekundách nebo odpovídající údaj z dostupného měření návštěv; laboratorní LCP vykazuj odděleně.

- [ ] [web] Když stránka zaznamenává uživatelské interakce: INP je nejvýš 200 ms na 75. percentilu reálných návštěv. Metrika sleduje odezvu na kliknutí, klepnutí a klávesnici během návštěvy. *Ověření:* načti `record.metrics.interaction_to_next_paint.percentiles.p75` z CrUX API v milisekundách nebo odpovídající údaj z dostupného měření návštěv; TBT ani samotné načtení stránky tento bod nepotvrzují.

- [ ] [web] CLS je nejvýš 0,1 na 75. percentilu reálných návštěv. Posuny mohou vznikat také po načtení, například při zobrazení dalších bloků nebo výměně fontu. *Ověření:* načti `record.metrics.cumulative_layout_shift.percentiles.p75` z CrUX API jako bezrozměrné číslo nebo odpovídající údaj z dostupného měření návštěv; výsledek běžného Lighthouse auditu označ jen jako laboratorní CLS při načítání.

- [ ] [web] Laboratorní TBT je orientačně nejvýš 200 ms v mobilním profilu Lighthouse. Je to diagnostická hranice blokování hlavního vlákna při načítání, nikoli náhrada INP. *Ověření:* načti `total-blocking-time.numericValue` z JSON reportu; při překročení přiřaď největší blokování ke konkrétním skriptům, případnou výjimku dolož měřením skutečných interakcí.

## Obrázky a stabilita obsahu

- [ ] [web] Bitmapové obrázky se doručují v rozměrech odpovídajících velikosti zobrazení a hustotě displeje. Zmenšení pomocí CSS nesníží počet stažených bajtů. *Ověření (prohlížeč):* na mobilním a desktopovém viewportu zjisti `currentSrc`, rozměry zobrazení a DPR; porovnej je se skutečnými rozměry staženého souboru, u responzivních obrázků prověř `srcset` a `sizes`.

- [ ] [web] Obrázky nemají zbytečně velký přenos kvůli nevhodnému formátu nebo nedostatečné kompresi. U fotek prověř WebP nebo AVIF, u jednoduché vektorové grafiky SVG; samotná přípona úspornost nepotvrzuje. *Ověření:* projdi „Improve image delivery“ v Lighthouse a skutečné formáty souborů; odhad úspory alespoň 4 KiB na obrázek ber jako orientační diagnostický nález, výjimku dolož například potřebou bezeztrátového obsahu nebo výsledkem porovnání variant.

- [ ] [web] Obrázky, videa a vložené bloky mají před načtením rezervovaný prostor odpovídající výslednému rozložení. Dodatečné zvětšení bloku může posunout okolní obsah. *Ověření:* zkontroluj `width` a `height`, CSS `aspect-ratio` nebo jinou rezervaci místa, u vícekrokového widgetu i změnu jeho výšky; nálezy porovnej s diagnostikou příčin layout shiftů v Lighthouse.

- [ ] [web] Když LCP tvoří obrázek: jeho načítání není odložené pomocí lazy loadingu. Odklad zdržuje zobrazení hlavního obsahu. *Ověření:* identifikuj LCP prvek v reportu a zkontroluj, že nepoužívá `loading="lazy"` ani ekvivalentní odklad v JavaScriptu.

- [ ] [web] Když LCP tvoří obrázek: jeho URL je zjistitelná už z počátečního HTML nebo preloadu v HTTP hlavičce. Prohlížeč nemusí čekat na spuštění JavaScriptu nebo stažení CSS, aby obrázek objevil. *Ověření:* porovnej LCP zdroj s HTML a hlavičkami získanými přes `curl`; hledej odpovídající `src`, `srcset` nebo preload skutečně použité varianty v HTML či hlavičce `Link`.

- [ ] [web] Když LCP tvoří obrázek: má odpovídající prioritu načítání. Vysoká priorita všech obrázků její účinek ruší. *Ověření:* prověř `fetchpriority="high"` na LCP obrázku nebo jeho preloadu; vysokou prioritu u více než jednoho až dvou obrázků ber jako orientační podnět k prověření podle síťového záznamu. Samotná absence atributu není chyba, pokud prohlížeč obrázek načítá včas s odpovídající prioritou.

- [ ] [web] Když jsou obrázky daleko pod počátečním viewportem: jejich načtení je odložené. Nesoutěží tak při otevření stránky s hlavním obsahem. *Ověření:* zkontroluj `loading="lazy"` nebo odpovídající mechanismus; obrázky v počátečním viewportu do této kontroly nezahrnuj a respektuj, že prohlížeč může přednačítat obrázky poblíž viewportu.

## Fonty

- [ ] [web] Když používáš webfonty: podporovaným moderním prohlížečům doručuješ WOFF2. Další formáty potřebují doložený požadavek na kompatibilitu. *Ověření:* projdi `@font-face`, formáty skutečně stahovaných fontů a požadavky projektu na podporované prohlížeče.

- [ ] [web] Když používáš webfonty: nestahují se nepoužité rodiny, řezy ani znakové subsety. Nepotřebný preload může obejít běžný výběr fontů a stáhnout soubor zbytečně. *Ověření:* porovnej fontové požadavky z měření s použitými styly a texty; zvlášť prověř preloady a fonty vložené přímo do CSS.

- [ ] [web] Když používáš webfonty: jejich znakové subsety pokrývají jazyky webu, na českých stránkách včetně české diakritiky. Chybějící znaky mohou přepínat část textu do jiného fontu. *Ověření:* pomocí FontTools nebo jiného dostupného nástroje porovnej znakovou mapu souborů a `unicode-range` s potřebnými znaky; u uživatelského obsahu vycházej z podporovaných jazyků, ne pouze z aktuálního vzorku textů.

- [ ] [web] Když používáš webfonty: běžný text se při čekání na font vykreslí záložním fontem bez dlouhé blokovací fáze. Typicky tomu odpovídá `font-display: swap` nebo `optional`. *Ověření:* projdi `font-display`, dostupný fallback a diagnostiku „Font display“; samotná existence záložního fontu bez kontroly načítacího chování nestačí.

- [ ] [web] Když se záložní font mění za webfont: celkové laboratorní CLS při výměně zůstává orientačně nejvýš 0,1 v ověřovaném scénáři. Podobný vzhled fontů nezaručuje stejné metriky a zalomení textu. *Ověření (prohlížeč):* s prázdnou cache a zpomaleným načítáním fontů zaznamenej layout shifty; urči příspěvek výměny fontu a porovnej celkové CLS se scénářem bez výměny. Tento test nepotvrzuje 75. percentil reálných návštěv.

## Komprese a cache

- [ ] [web] Textové odpovědi, u kterých komprese snižuje přenos, se doručují komprimované. Týká se hlavně HTML, CSS, JavaScriptu, SVG a textových dat. *Ověření:* pro skutečné produkční URL spusť `curl --compressed -sS -D - -o /dev/null -w '%{size_download}\n' 'URL'`, zkontroluj `Content-Encoding` a porovnej přenesené bajty těla s opakováním stejného požadavku bez `--compressed` a s `-H 'Accept-Encoding: identity'`; malé odpovědi bez čisté úspory nepovažuj automaticky za chybu.

- [ ] [web] Když má veřejný statický soubor neměnný obsah a verzi v URL: používá dlouhou cache. Orientační vzor je `Cache-Control: max-age=31536000, immutable`, tedy jeden rok; kratší dobu zdůvodni potřebou projektu. *Ověření:* přes GET zkontroluj skutečné hlavičky reprezentativních skriptů, stylů, obrázků a fontů; tento vzor nepřenášej na personalizované odpovědi.

- [ ] [web] Když používáš dlouhou cache statických souborů: změna obsahu mění jejich URL. Vyprázdnění serverové cache neodstraní čerstvou kopii uloženou v prohlížeči návštěvníka. *Ověření:* projdi manifest a pravidla verzování; z dostupných sestavení nebo implementace ověř, že změněný soubor dostane novou URL a odkazující dokument ji použije.

- [ ] [web] HTML má explicitní pravidlo obnovy odpovídající požadované aktuálnosti obsahu. Běžný vzor je revalidace pomocí `no-cache`, ne dlouhá neměnná cache převzatá ze statických souborů. *Ověření:* porovnej hlavičky GET odpovědi s konfigurací; při použití `ETag` nebo `Last-Modified` ověř podmíněný GET, jinou strategii posuď podle doložené doby přijatelného zastarání a všech zapojených cache včetně service workeru.

## Velikost a spouštění kódu

- [ ] [web] Když projekt rozlišuje vývojové a produkční sestavení: veřejný web doručuje produkční sestavení. Vývojový klient, ladicí panely nebo kompilace určená jen pro vývoj přidávají zbytečný přenos a práci. *Ověření:* porovnej konfiguraci sestavení a nasazení se skutečně doručovanými soubory; hledej vývojové runtime moduly a připojení pro aktualizace vývojového serveru.

- [ ] [web] Produkční JavaScript a CSS jsou minifikované. Minifikace a přenosová komprese řeší odlišné části velikosti souborů. *Ověření:* zkontroluj nastavení sestavení a skutečné produkční soubory; komentáře nutné kvůli licenci nepovažuj za chybu.

- [ ] [web] Produkční JavaScript nepřenáší významné množství prokazatelně nepotřebného kódu. Orientační podnět k prověření je více než 20 KiB nepoužitého kódu v jednom souboru podle diagnostiky Lighthouse. *Ověření:* nález porovnej s importy a analýzou balíků včetně duplicitních knihoven; kód označ za nepotřebný až po prověření relevantních interakcí a stavů stránky.

- [ ] [web] Produkční CSS nepřenáší významné množství prokazatelně nepotřebných pravidel. Orientační podnět k prověření je odhad úspory alespoň 2 KiB v jednom stylesheetu podle diagnostiky Lighthouse. *Ověření:* porovnej nález s použitím stylů v projektu; zahrň responzivní varianty, otevřená menu, dialogy a chybové stavy, samotné nepoužití při prvním načtení nestačí.

- [ ] [web] Když je rozsáhlá funkce potřeba až později: její kód nezatěžuje nezbytné počáteční načtení bez doloženého důvodu. Typicky jde o editor, graf nebo jinou obrazovku aplikace. *Ověření:* porovnej strukturu produkčních balíků a síťové požadavky při načtení s požadavky při aktivaci funkce; případné přednačítání posuď podle jeho dopadu na LCP a odezvu.

- [ ] [web] Stahování skriptů nepotřebných pro počáteční zobrazení nezastavuje parsování HTML. Jejich spuštění může dál blokovat hlavní vlákno; `async` při spuštění přeruší také parsování. *Ověření:* projdi skutečné HTML a iniciátory požadavků; u externích klasických skriptů prověř vhodné `defer`, `async` nebo pozdější načtení, modulové skripty posuzuj podle jejich výchozího odloženého chování.

- [ ] [velká] Počáteční přenos stránky se vejde do stanoveného výkonnostního rozpočtu. Rozpočet stanov podle cílových zařízení, připojení a potřebného obsahu; historických 1 600 KiB z doporučení Lighthouse není univerzální limit ani důkaz splnění Core Web Vitals. *Ověření:* porovnej stanovený rozpočet s přenesenými bajty při načtení s prázdnou cache bez scrollování a dalších akcí; uveď měřicí interval, rozpad podle typů zdrojů a zvlášť velikost JavaScriptu po přenosové kompresi a po rozbalení.

## Skripty třetích stran

- [ ] [web] Když web načítá integrace třetích stran: každá má doložený aktuální účel. Opuštěná analytika, widget nebo experiment mohou dál načítat další kód. *Ověření:* sestav inventář z kódu a síťového záznamu včetně skriptů přidaných nepřímo; zahrň stav s aktivními integracemi po udělení souhlasu, nejasný účel označ jako „Otázka“.

- [ ] [web] Když vložený přehrávač, mapa nebo widget nejsou potřeba při otevření stránky: jejich plné načtení je odložené do přiblížení k viewportu nebo aktivace. Lehký náhled může zabránit předčasnému stažení celé integrace; odložení nesmí zablokovat obsah potřebný k první hlavní akci. *Ověření:* zkontroluj mechanismus odložení a síťový záznam; samotný vizuální placeholder bez odložení požadavků nestačí.

- [ ] [web] Když třetí strana zajišťuje pouze doplňkovou funkci: její nedostupnost neblokuje zobrazení hlavního obsahu. Čekání na analytiku nebo chat nemá zadržet celou stránku. *Ověření (prohlížeč):* zablokuj požadavky integrace, znovu načti stránku a ověř zobrazení hlavního obsahu; porovnej také LCP a blokování hlavního vlákna s běžným načtením.

## Zdroje

Zdroje ověřené 26. 10. 2026. Diagnostické prahy nástrojů se mohou měnit; do reportu zapisuj použitou verzi.

- **Core Web Vitals:** [hranice a 75. percentil](https://web.dev/articles/defining-core-web-vitals-thresholds), [CrUX API a období sběru](https://developer.chrome.com/docs/crux/api), [dotazy podle URL a zařízení](https://developer.chrome.com/docs/crux/guides/crux-api).
- **Laboratorní měření:** [Lighthouse CLI a další způsoby spuštění](https://developer.chrome.com/docs/lighthouse/overview), [PageSpeed Insights API](https://developers.google.com/speed/docs/insights/v5/get-started), [rozdíl laboratorních a reálných dat](https://developers.google.com/speed/docs/insights/v5/about).
- **TBT:** [hranice 200 ms v mobilním profilu Lighthouse](https://developer.chrome.com/docs/lighthouse/performance/lighthouse-total-blocking-time).
- **Obrázky:** [rozměry, DPR, `srcset`, `sizes` a formáty](https://web.dev/learn/performance/image-performance), [diagnostika doručování obrázků a práh úspory 4 KiB](https://developer.chrome.com/docs/performance/insights/image-delivery).
- **LCP obrázek:** [objevení zdroje, lazy loading a priorita](https://web.dev/articles/optimize-lcp).
- **Stabilita rozložení:** [rezervace prostoru, posuny po načtení a fonty](https://web.dev/articles/optimize-cls).
- **Fonty:** [WOFF2, subsety, preload a doručování](https://web.dev/learn/performance/optimize-web-fonts), [načítání, fallback a výměna fontů](https://web.dev/articles/font-best-practices), [`font-display`](https://developer.chrome.com/docs/lighthouse/performance/font-display).
- **Komprese a minifikace:** [optimalizace přenášených textových souborů](https://web.dev/articles/optimizing-content-efficiency-optimize-encoding-and-transfer).
- **Cache:** [RFC 9111: HTTP Caching](https://httpwg.org/specs/rfc9111.html), [RFC 8246: `immutable`](https://www.rfc-editor.org/rfc/rfc8246.html), [MDN: verzování, roční cache a revalidace HTML](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Caching).
- **Nepoužitý kód:** [JavaScript a diagnostický práh 20 KiB](https://developer.chrome.com/docs/lighthouse/performance/unused-javascript), [CSS a diagnostický práh 2 KiB](https://developer.chrome.com/docs/lighthouse/performance/unused-css-rules), [Coverage](https://developer.chrome.com/docs/devtools/coverage).
- **Načítání kódu:** [rozdělení JavaScriptu](https://web.dev/learn/performance/code-split-javascript), [minifikace, produkční optimalizace a blokující zdroje](https://web.dev/learn/performance/optimize-resource-loading).
- **Výkonnostní rozpočty:** [MDN: stanovení podle cílových podmínek](https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Performance_budgets), [starší doporučení Lighthouse: 1 600 KiB](https://developer.chrome.com/docs/lighthouse/performance/total-byte-weight).
- **Třetí strany:** [inventář, odložené načítání a měření dopadu blokováním požadavků](https://web.dev/articles/optimizing-content-efficiency-loading-third-party-javascript), [úsporné načítání vloženého obsahu](https://web.dev/articles/embed-best-practices).

Doplněné zdroje pro opravy, ověřené 27. 10. 2026:

- **Definice LCP:** [způsobilé prvky včetně videa](https://web.dev/articles/lcp).
- **Měření přenosu:** [curl: `--compressed`, `--write-out` a `size_download`](https://curl.se/docs/manpage.html).
