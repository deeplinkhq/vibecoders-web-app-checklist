# Testování a spuštění

**Týká se:** každého webu. Položky pro vlastní logiku, ukládání dat, přihlášení nebo platby použij jen tam, kde tyto funkce existují.

## Co musí testování pokrýt

- [ ] [web] Projekt má seznam kritických uživatelských cest s očekávaným výsledkem. Kritická je cesta, jejíž selhání zablokuje hlavní účel webu, poškodí data nebo způsobí finanční škodu. *Ověření:* porovnej zadání a dostupné funkce se seznamem scénářů; každý scénář musí určit výchozí stav, kroky a konkrétní výsledek.

- [ ] [web] Testovací scénáře vycházejí z požadovaného chování. Test napsaný podle chybné implementace může tutéž chybu potvrdit. *Ověření:* porovnej očekávané výsledky testů se zadáním, pravidly výpočtu nebo schválenými příklady; samotná shoda s aktuálním výstupem programu nestačí.

Podklad: [ISTQB: Acceptance Testing, sekce 2.1 a 2.2](https://istqb.org/wp-content/uploads/2024/11/ISTQB-CT-AcT_Syllabus_v1.0_2019.pdf).

## Testy jako pojistka při práci s AI agentem

- [ ] [web] Když změna upravuje nebo odstraňuje existující test: změna očekávání má oporu ve změně požadavku nebo v doložené chybě testu. Zelený výsledek po oslabení kontroly neprokazuje opravu aplikace. *Ověření:* projdi diff testů a konfigurace kontrol, vynechané testy, odstraněné assertions, nové mocky, ignorované chyby a aktualizované snapshoty; každou změnu očekávaného chování porovnej se zadáním.

- [ ] [malá] Když opravuješ reprodukovatelnou funkční chybu: existuje regresní test, který ji zachytí. Chrání před návratem stejné chyby při další úpravě. *Ověření:* dohledávej výsledek testu na chybné a opravené verzi; test má na chybné verzi selhat kvůli dané chybě a na opravené projít.

Podklady: [GitHub: odpovědné použití coding agentů](https://docs.github.com/en/copilot/responsible-use/agents), [Google SRE: regresní testy a ověřování změn](https://sre.google/sre-book/testing-reliability/). Kontrola oslabování testů je praktická aplikace těchto zásad pro práci s agentem.

## Typ testu odpovídá riziku

- [ ] [malá] Když projekt obsahuje vlastní výpočty nebo rozhodovací pravidla: nová a měněná pravidla mají unit testy. Chybu ve výpočtu je levnější a přesnější hledat na malé části programu. *Ověření:* přiřaď pravidla k testům a spusť je; kontroluj konkrétní očekávané hodnoty.

- [ ] [malá] Když kritická funkce propojuje více částí aplikace: jejich spolupráci ověřuje integrační test. Samostatně fungující části ještě nezaručují správný přenos a zpracování dat. *Ověření:* přiřaď kritické přenosy dat k testům a spusť je, například požadavek API, uložení a následné načtení; zjisti, které závislosti test nahrazuje mockem.

- [ ] [veřejná] Když aplikace obsahuje kritické uživatelské cesty: automatické E2E testy přes uživatelské rozhraní pokrývají jejich reprezentativní výběr podle rizika. Unit a integrační testy nemusí zachytit rozbité propojení obrazovek. *Ověření:* porovnej seznam kritických cest s E2E sadou a zdůvodněním jejího rozsahu; spusť vybrané scénáře a ověř, že zahrnují cesty s nejvyšším dopadem selhání; samotné testování API tuto položku nesplňuje.

Podklad: [Google Testing Blog: kombinace unit, integračních a E2E testů](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html). Poměr jednotlivých typů určuj podle projektu, bez povinného procentuálního rozdělení.

- [ ] [malá] Když funkce přijímá vstup s omezeními: testy pokrývají neplatné a hraniční hodnoty. Běžný platný vstup neodhalí chybu na povoleném limitu. *Ověření:* z validace a zadání odvoď platné a neplatné skupiny vstupů; u hranic otestuj hodnotu na hranici a sousední hodnoty podle typu dat.

- [ ] [web] Když kritická funkce závisí na síti nebo jiné službě: je otestované selhání této závislosti. Aplikace nesmí neprovedenou operaci oznámit jako úspěšnou. *Ověření:* v testovacím prostředí nasimuluj relevantní chybu, například odmítnutý požadavek nebo přerušení spojení; ověř chybový stav a možnost dalšího postupu podle zadání.

- [ ] [malá] Když aplikace maže nebo ruší záznamy: test ověřuje přesný rozsah změny. Chybně zvolený záznam nebo filtr může poškodit další data. *Ověření:* na testovacích datech proveď operaci a následným načtením potvrď změnu cílového záznamu i zachování ostatních.

Podklady: [ISTQB CTFL v4.0.1, sekce 4.2](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf), [Google SRE: správné a chybné požadavky](https://sre.google/sre-book/testing-reliability/), [Playwright: simulace síťových odpovědí a selhání](https://playwright.dev/docs/network).

- [ ] [velká] Když spuštění zahrnuje očekávanou špičku provozu: aplikace má zátěžový test odpovídající této špičce. Jeden úspěšný průchod neověří chování při souběžném používání. *Ověření:* dohledávej zdůvodněný model zátěže, délku testu a předem stanovené limity chybovosti a odezvy; porovnej je s výsledkem testu v určeném prostředí.

Podklad: [k6: předem stanovená kritéria úspěchu zátěžového testu](https://grafana.com/docs/k6/latest/using-k6/thresholds/). Číselné příklady v dokumentaci nejsou univerzální limity pro všechny aplikace.

## Automatickým testům se dá věřit

- [ ] [malá] Když projekt má automatické testy: jejich spuštění je reprodukovatelné z dokumentovaného postupu. Test závislý na zapomenutém lokálním nastavení neposkytuje spolehlivou pojistku. *Ověření:* podle dokumentace připrav testovací prostředí a spusť příslušný příkaz; ověř, že se skutečně našly a provedly očekávané testy.

- [ ] [malá] Když test ověřuje uživatelskou operaci: kontroluje její skutečný výsledek. Kliknutí nebo úspěšná HTTP odpověď sama neprokazuje správné provedení. *Ověření:* projdi assertions; u ukládání ověř následné načtení dat, u ostatních operací výsledek odpovídající zadání.

- [ ] [malá] Když projekt má automatické testy: každý scénář má řízený výchozí stav. Výsledek nesmí záviset na tom, který jiný test běžel před ním. *Ověření:* zkontroluj přípravu účtů, dat a relací; spusť vybraný scénář samostatně i v sadě a ověř nezávislost testovacích dat.

- [ ] [malá] Když E2E test čeká na asynchronní operaci: čekání vychází z očekávaného stavu. Pevná prodleva může být na pomalém prostředí krátká a na rychlém zbytečná. *Ověření:* projdi čekání v testech; místo pevného uspání požaduj čekání na konkrétní prvek, odpověď nebo stav s omezeným timeoutem.

Podklady: [Playwright: testování výsledku a izolace](https://playwright.dev/docs/best-practices), [Playwright: assertions čekající na stav](https://playwright.dev/docs/test-assertions).

- [ ] [malá] Když test projde až při opakování: výsledek je evidovaný jako nestabilní test. Opakování nesmí skrýt původní selhání. *Ověření:* porovnej report prvního běhu a opakování; u nestabilního testu dohledávej příčinu nebo evidovaný problém a dopad na rozhodnutí o vydání.

Podklad: [Playwright: rozlišení passed, flaky a failed](https://playwright.dev/docs/test-retries).

## Prohlížeče a zařízení

- [ ] [web] Projekt má určené podporované kombinace prohlížeče, verze a zařízení. Výběr má odpovídat cílovým uživatelům. *Ověření:* dohledávej seznam a jeho zdůvodnění pomocí návštěvnosti nebo zamýšleného publika; bez těchto údajů zaznamenej rozsah jako nepotvrzený.

- [ ] [web] Kritické cesty prošly v podporovaných kombinacích prohlížečů a zařízení. Úspěch v jednom prohlížeči neprokazuje kompatibilitu ostatních. *Ověření (prohlížeč):* spusť stejné scénáře podle seznamu podpory a u výsledku zaznamenej prohlížeč, verzi, operační systém a skutečné nebo emulované zařízení.

Podklad: [MDN: výběr prohlížečů a strategie testování](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Testing_strategies).

- [ ] [web] Když mezi podporovaná zařízení patří telefony: kritické cesty jsou ověřené na skutečných telefonech zastupujících podporované mobilní platformy. Emulace viewportu nepokrývá celé chování telefonu. *Ověření (člověk):* na uvedeném telefonu projdi kritické cesty; když zahrnují formulář, ověř i zadávání přes softwarovou klávesnici až po poslední pole a odeslání; zaznamenej model, systém, prohlížeč a výsledek.

Podklady: [Chrome DevTools: omezení emulace zařízení](https://developer.chrome.com/docs/devtools/device-mode), [MDN: testování na skutečných zařízeních](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Introduction).

- [ ] [web] Hlavní cesta je použitelná i při zpomaleném připojení. Pomalý přenos může odhalit nefunkční čekání nebo předčasně dostupná tlačítka. *Ověření (prohlížeč):* zaznamenej použitý profil omezení sítě, vypni cache a proveď hlavní cestu; výsledek musí odpovídat zadání i při delším načítání.

Podklad pro způsob simulace: [Chrome DevTools: omezení rychlosti sítě](https://developer.chrome.com/docs/devtools/device-mode). Volba profilu závisí na cílovém použití.

## Před spuštěním nebo vydáním změny

- [ ] [web] Kandidát na vydání prošel kontrolou v režimu odpovídajícím produkčnímu běhu. Vývojový server nemusí odhalit chybu sestavení nebo produkční konfigurace. *Ověření:* spusť dokumentovaný produkční build nebo ekvivalentní přípravu a smoke test výsledného artefaktu na zkušební adrese; ověř shodu testované a vydávané verze.

Podklad: [Google SRE: testování konkrétní vydávané verze a sestavených artefaktů](https://sre.google/sre-book/release-engineering/).

- [ ] [web] Při průchodu kritickými cestami nevznikají nevysvětlené chyby aplikace v konzoli ani selhání požadavků potřebných pro danou cestu. Vizuálně správná stránka může skrývat nefunkční část. *Ověření (prohlížeč):* zaznamenej konzoli a síťové požadavky během scénářů; očekávaná selhání při negativních testech odděl od neočekávaných chyb.

Podklad pro získání důkazů: [Playwright Trace Viewer: konzole, síť a průběh testu](https://playwright.dev/docs/trace-viewer).

- [ ] [web] Odkazy ve veřejné navigaci a publikovaném obsahu vedou na zamýšlené cíle. Kontroluj i patičku, kotvy a odkazy mimo web. *Ověření (prohlížeč):* spusť automatickou kontrolu odkazů a kotev; v prohlížeči doplň odkazy vytvářené JavaScriptem a nejednoznačné výsledky, například blokování automatických požadavků; porovnej cíle s textem odkazu a zadáním, protože úspěšná HTTP odpověď sama nepotvrzuje správný cíl.

Podklad pro automatickou kontrolu: [W3C Link Checker](https://github.com/w3c/link-checker).

- [ ] [web] Kandidát na vydání má vyhodnocené nálezy z relevantních kategorií checklistu. Samotné spuštění automatického auditu nestačí. *Ověření:* dohledávej aktuální report pro vydávanou verzi; nevyřešené nálezy musí mít popsaný dopad a rozhodnutí vlastníka projektu, zda vydání blokují.

Podklady: [ISTQB CTFL v4.0.1: exit criteria a test completion](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf), [W3C WAI: omezení automatického hodnocení přístupnosti](https://www.w3.org/WAI/test-evaluate/).

- [ ] [web] Když web nebo aplikaci budou používat lidé mimo autorský tým: hlavní úkol vyzkoušel zástupce cílových uživatelů bez navádění. Funkční automatický test neodhalí, že uživatel neví, jak pokračovat. *Ověření (člověk):* dej účastníkovi cíl bez návodu, pozoruj průchod a zaznamenej dokončení, místa zaváhání a nutné zásahy.

Podklady: [MDN: uživatelské testování](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Testing_strategies), [GOV.UK: úkoly a pozorování při testování použitelnosti](https://www.gov.uk/service-manual/user-research/using-moderated-usability-testing).

## Hned po spuštění nebo nasazení

- [ ] [web] Nasazená verze prošla smoke testem na skutečné produkční adrese v čisté relaci. Zkušební prostředí neověří všechny vlastnosti produkční konfigurace. *Ověření (prohlížeč):* ověř identitu nasazené verze a proveď bezpečně opakovatelné kritické scénáře bez vývojářské relace; pro přihlášení použij určený testovací účet s běžnými oprávněními; výsledek zaznamenej k danému nasazení.

- [ ] [web] Když kritická cesta používá externí službu: je ověřený skutečný výsledek přes produkční integraci. Test s mockem nepotvrzuje doručení zprávy ani správné propojení ostrého prostředí. *Ověření:* dohledávej výsledek řízeného testu, například přijetí zprávy v určené schránce; zápisové nebo placené operace ověřuj jen podle předem určeného produkčního testovacího postupu, jinak je předej člověku.

Podklad: [Google SRE: produkční probes a rozdíly proti testovacímu prostředí](https://sre.google/sre-book/testing-reliability/).

- [ ] [velká] Když nasazuješ změnu do běžící aplikace: jsou po nasazení vyhodnocené signály selhání kritických cest. Úspěšný smoke test nemusí zachytit problém při skutečném provozu. *Ověření:* porovnej dostupné výsledky transakcí, chybovost a odezvu s předem stanovenými mezemi projektu; dohledávej délku sledování, důvod její volby a postup při překročení mezí.

Podklad: [Google SRE Workbook: vyhodnocování vydání podle provozních signálů](https://sre.google/workbook/canarying-releases/).

## Zdroje

- [ISTQB: Acceptance Testing, v1.0](https://istqb.org/wp-content/uploads/2024/11/ISTQB-CT-AcT_Syllabus_v1.0_2019.pdf) - měřitelná akceptační kritéria a testy odvozené z požadavků.
- [ISTQB: CTFL syllabus, v4.0.1](https://istqb.org/wp-content/uploads/2024/11/ISTQB_CTFL_Syllabus_v4.0.1.pdf) - testovací techniky, hranice vstupů, kritéria ukončení testování.
- [GitHub: Responsible use of GitHub Copilot agents](https://docs.github.com/en/copilot/responsible-use/agents) - nutnost kontroly a testování výstupů AI agentů.
- [Google Testing Blog: Just Say No to More End-to-End Tests](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html) - účel a omezení unit, integračních a E2E testů.
- [Google SRE: Testing for Reliability](https://sre.google/sre-book/testing-reliability/) - regresní testy, smoke testy a produkční ověřování.
- [Google SRE: Release Engineering](https://sre.google/sre-book/release-engineering/) - opakovatelné sestavení a testování vydávané verze.
- [Playwright: Best Practices](https://playwright.dev/docs/best-practices) - výsledky viditelné uživateli, izolace a řízená testovací data.
- [Playwright: Assertions](https://playwright.dev/docs/test-assertions) - čekání na očekávaný stav.
- [Playwright: Network](https://playwright.dev/docs/network) - simulace odpovědí a síťových selhání.
- [Playwright: Retries](https://playwright.dev/docs/test-retries) - evidence nestabilních testů.
- [Playwright: Trace Viewer](https://playwright.dev/docs/trace-viewer) - důkazy z konzole, sítě a jednotlivých kroků.
- [MDN: Introduction to cross-browser testing](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Introduction) - kompatibilita a skutečná zařízení.
- [MDN: Strategies for carrying out testing](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Testing/Testing_strategies) - výběr podporovaných zařízení a uživatelské testování.
- [Chrome DevTools: Device Mode](https://developer.chrome.com/docs/devtools/device-mode) - možnosti a omezení emulace.
- [W3C: Link Checker](https://github.com/w3c/link-checker) - kontrola odkazů a kotev.
- [W3C WAI: Evaluating Web Accessibility](https://www.w3.org/WAI/test-evaluate/) - automatické nástroje samy neprokazují přístupnost.
- [k6: Thresholds](https://grafana.com/docs/k6/latest/using-k6/thresholds/) - projektová kritéria úspěchu zátěžových testů.
- [Google SRE Workbook: Canarying Releases](https://sre.google/workbook/canarying-releases/) - signály selhání a vyhodnocení změny v provozu.
- [GOV.UK: Using moderated usability testing](https://www.gov.uk/service-manual/user-research/using-moderated-usability-testing) - výběr skutečných nebo pravděpodobných uživatelů, zadání cíle bez návodu a pozorování průchodu.
