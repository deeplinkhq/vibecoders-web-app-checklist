# AI funkce v aplikaci

**Týká se:** aplikace, která používá jazykový model, včetně chatu, generování obsahu, vyhledávání v dokumentech a modelu s přístupem k nástrojům. Samotné používání AI agenta při vývoji patří do kategorie 15.

Číselné limity nastav podle účelu aplikace, rozpočtu a dopadu chyby. Pro počet tokenů, požadavků ani přijatelnou chybovost neexistuje univerzální bezpečná hodnota. Limit musí být konkrétní, zdokumentovaný a vynucený mimo model.

Bezpečnostní testy prováděj v testovacím prostředí se syntetickými daty a náhradami nástrojů. U nástrojů ověřuj skutečná volání a změny stavu. Odmítnutí v závěrečné odpovědi nedokazuje, že model předtím nic neprovedl.

## Klíče, kontext a soukromí

- [ ] Když aplikace používá vlastní dlouhodobý klíč k placenému modelu: klíč není dostupný klientovi. Jeho zkopírováním by kdokoli získal přístup na tvůj účet. *Ověření:* projdi sestavené klientské soubory, zdrojové mapy a odpovědi API; ověř, že dlouhodobý klíč používá jen server. [Z1]

- [ ] Systémový prompt a další skryté instrukce neobsahují přístupová tajemství. Jejich utajení nesmí být podmínkou zabezpečení aplikace. *Ověření:* projdi skutečně sestavovaný kontext včetně popisů nástrojů; hledej klíče, hesla, tokeny a připojovací řetězce, hodnoty v reportu nezveřejňuj. [Z2]

- [ ] Do modelu odcházejí jen data potřebná pro daný úkol. Celý uživatelský profil nebo kompletní dokument nemusí být pro odpověď nutný. *Ověření:* na syntetickém požadavku zachyť výsledný payload před odesláním; porovnej jednotlivá pole s účelem funkce a ověř odstranění nepotřebných citlivých údajů. [Z3, Z13]

- [ ] Když aplikaci používá více uživatelů: soukromý kontext jednoho uživatele se nedostane do odpovědi jinému. To platí i pro historii, paměť a sdílenou cache odpovědí. *Ověření:* použij dva testovací účty s odlišnými značkami v soukromých datech; zkus přístup přes cizí identifikátor konverzace, obnovenou relaci a shodný dotaz do cache. [Z3]

- [ ] Když model vyhledává v neveřejných dokumentech: oprávnění omezují už samotné vyhledávání. Filtrování až hotové odpovědi přichází pozdě. *Ověření:* projdi dotaz do indexu a sestavování kontextu; testovacím účtem ověř, že se cizí dokument ani jeho úryvek nevrátí z vyhledávání. [Z4]

- [ ] Když data posíláš externímu modelu nebo AI nástroji: jeho skutečné podmínky zpracování odpovídají schválenému použití dat. Zkontroluj i ukládání vstupů a jejich případné použití pro trénování. *Ověření (člověk):* vlastník účtu porovná aktuální smluvní podmínky a nastavení konkrétního účtu s daty, která aplikace odesílá; doloží datum a výsledek kontroly. [Z3, Z13]

## Prompt injection a trvalé podklady

- [ ] Uživatelský a načtený obsah nemůže přímo nastavovat důvěryhodnou roli zprávy. Oddělení instrukcí od dat snižuje riziko prompt injection, ale samo ji nezastaví. *Ověření:* projdi sestavování zpráv; ověř, že uživatel nemůže podstrčit zprávu v systémové roli a že dokumenty i výsledky nástrojů mají označený původ. [Z5, Z6]

- [ ] Testy prompt injection ověřují bezpečnostní hranice přes všechny podporované vstupní kanály. Pokyn ukrytý v dokumentu se musí testovat jako dokument, ne jen vložením do chatu. *Ověření:* spusť přímé i nepřímé útoky, včetně vícetahových a jazykových variant; kontroluj únik syntetických dat, volání nástrojů a změny stavu, nejen text odpovědi. [Z5, Z6]

- [ ] Když aplikace doplňuje trvalou paměť, znalostní bázi nebo data pro fine-tuning: nové podklady procházejí řízeným přijetím. Neověřená uživatelská zpětná vazba nesmí sama měnit důvěryhodné podklady. *Ověření:* projdi cestu zápisu, oprávnění a záznam původu; vlož syntetický podklad s podvrženými instrukcemi a ověř, že neobejde stanovené přijetí. [Z7]

## Výstup modelu

- [ ] Když zobrazuješ výstup modelu v HTML nebo Markdownu: renderer zabrání spuštění aktivního obsahu. Kontrola musí fungovat i během streamování odpovědi. *Ověření:* projdi escapování a sanitizaci; do rendereru přímo vlož testovací výstupy se skriptem, obsluhou události a nebezpečným URL schématem. [Z8]

- [ ] Když renderer zpracovává odkazy na externí zdroje: nenačítá automaticky libovolné adresy z výstupu modelu. Obrázek nebo náhled odkazu může odeslat obsah konverzace v URL. *Ověření (prohlížeč):* zobraz syntetickou odpověď s externím obrázkem a náhledem odkazu; v síťových požadavcích ověř, že bez schválené politiky nic neodešlo na testovací cizí doménu. [Z8]

- [ ] Když další část aplikace zpracovává strukturovaný výstup modelu: server ověřuje jeho schéma i povolené hodnoty. Platný JSON ještě neznamená platný požadavek. *Ověření:* přímo do navazujícího handleru pošli chybějící pole, jiný typ, nepovolenou hodnotu a neznámé pole; ověř odmítnutí před vedlejším účinkem. [Z5, Z8]

- [ ] Výstup modelu se nevykonává přímo jako privilegovaný příkaz. Vygenerovaný SQL dotaz, shell příkaz nebo cesta k souboru je nedůvěryhodný vstup. *Ověření:* sleduj výstup k databázi, souborům a spouštění procesů; ověř parametrizované operace a omezení cíle, testovací payload nesmí změnit strukturu příkazu ani opustit povolený prostor. [Z8]

## Oprávnění a nástroje modelu

- [ ] Když model používá nástroje: dostává jen funkce a oprávnění potřebná pro konkrétní úkol. Pro čtení dokumentu nepotřebuje mazání ani obecný shell. *Ověření:* porovnej seznam nástrojů a oprávnění jejich přístupových identit s podporovanými úkoly; ověř, že nepotřebná operace není dostupná ani přímým voláním. [Z9]

- [ ] Když model používá nástroje: vykonávající kód ověřuje oprávnění uživatele při každé akci. Identita ani přístupový rozsah se nesmí přebírat z tvrzení modelu. *Ověření:* zavolej nástroj s cizím ID objektu, podvrženou identitou a po odebrání oprávnění; ve všech případech musí přístup odmítnout, také při navazujícím volání dalšího agenta. [Z9]

- [ ] Když model navrhuje rizikovou nebo nevratnou akci: její provedení vyžaduje platné schválení konkrétní akce. Schválení změněného příjemce, částky nebo cíle už neplatí. *Ověření:* v testu změň parametry po schválení, použij prošlé schválení a zkus jeho opakované použití; vykonávající komponenta musí všechny pokusy odmítnout. [Z10]

- [ ] Když model může načítat URL nebo odesílat data ven: přístup omezuje vynucená síťová politika. Prompt nesmí být jedinou překážkou přístupu k interním službám nebo odeslání soukromých dat. *Ověření:* projdi povolené cíle; otestuj nepovolenou doménu, loopback, privátní a link-local adresu i přesměrování na zakázaný cíl. [Z5, Z10]

- [ ] Když aplikace záměrně spouští modelový kód: běží v izolovaném prostředí s omezenými prostředky. Kód nesmí získat produkční tajemství ani přístup k hostitelskému systému. *Ověření:* zkontroluj konfiguraci izolace a limity; syntetickým kódem otestuj čtení souboru mimo pracovní prostor, nepovolené síťové spojení a nekonečný výpočet. [Z10]

## Útrata a limity

- [ ] Když aplikace zpřístupňuje placenou AI funkci: každý uživatel nebo anonymní klient má vynucenou kvótu spotřeby. Samotný počet požadavků nezachytí drahé dlouhé odpovědi. *Ověření:* zkontroluj započítávání tokenů nebo nákladů do kvóty; souběžnými požadavky ověř, že ji nelze obejít a odmítnuté požadavky nevyvolají další placené volání. [Z11]

- [ ] Když provoz AI vytváří proměnlivé náklady: aplikace má vynucený celkový rozpočtový strop. E-mailové upozornění ani automatické dobíjení nejsou strop. *Ověření:* s testovacím účetnictvím nastav nízký rozpočet a ověř zastavení nových placených operací; započti rezervace pro souběžná volání, opakování a placené nástroje. [Z11]

- [ ] Každý vstup do modelu má vynucený limit velikosti. Limit zahrnuje i připojenou historii, načtené dokumenty a podporovaná média. *Ověření:* projdi sestavení výsledného vstupu; překroč nakonfigurovaný limit v každém podporovaném kanálu a ověř odmítnutí nebo řízené zkrácení před placeným zpracováním. [Z11]

- [ ] Každé generování má vynucený limit výstupní spotřeby. U reasoning modelu musí rozpočet zahrnovat také účtované reasoning tokeny, pokud je model používá. *Ověření:* zkontroluj skutečně odesílané parametry a jejich význam pro použitý model; požadavkem na velmi dlouhý výstup ověř ukončení na nastaveném limitu. [Z11]

- [ ] Když model opakovaně volá nástroje nebo další modely: celý běh má konečný limit kroků. Opakování a delegování nesmí založit nový běh s obnoveným rozpočtem. *Ověření:* nasimuluj cyklus a chybující nástroj; ověř ukončení na limitu včetně opakovaných a delegovaných volání. [Z10, Z11]

- [ ] Volání modelu a jeho nástrojů mají vynucený časový limit. Vypršení limitu nesmí nechat nekontrolovaně pokračovat navazující práci. *Ověření:* použij zpožděnou náhradu API; ověř ukončení čekání a zastavení navazujících kroků, také po odpojení klienta. [Z10]

## Logování a životní cyklus dat

- [ ] Z provozního záznamu lze dohledat průběh AI požadavku. Záznam obsahuje identifikátor požadavku, verzi modelu a promptu, spotřebu, výsledek a případné akce nástrojů. *Ověření:* proveď úspěšný, odmítnutý a chybový požadavek; podle identifikátoru dohledáš související volání, rozhodnutí o oprávnění a skutečný výsledek akcí. [Z10, Z12]

- [ ] AI logy a telemetry neukládají nezpracované citlivé údaje bez stanoveného důvodu. Kontrola se týká i chyb, argumentů nástrojů a reasoning traces. *Ověření:* do syntetických dat vlož testovací osobní údaj a falešný klíč; projdi logy a exporty telemetry a ověř požadované vynechání nebo redakci. [Z3, Z12]

- [ ] Když ukládáš konverzace, paměť nebo AI traces: jejich uchovávání má stanovenou a prováděnou dobu. Dobu určuj podle účelu a případných zákonných povinností. *Ověření:* porovnej retenční pravidla s konfigurací mazání; na zestárlém testovacím záznamu ověř skutečné odstranění nebo předepsanou anonymizaci. [Z12, Z13]

- [ ] Když ukládáš neveřejné AI logy nebo konverzace: přístup k nim mají jen oprávněné role. Debug rozhraní nesmí zpřístupnit obsah cizího účtu. *Ověření:* testovacím účtem bez příslušné role zkus seznam, detail a export; ověř odmítnutí také přes přímé API. [Z3, Z12]

- [ ] Když zdrojový dokument smažeš nebo mu odebereš oprávnění: změna se promítne i do odvozeného AI vyhledávání. Stará kopie v indexu nebo cache nesmí dokument dál zpřístupňovat. *Ověření:* na testovacím dokumentu proveď smazání a změnu oprávnění; po zdokumentované lhůtě synchronizace ověř nedostupnost úryvků, embeddingů a odpovědí z cache. [Z4]

## Kvalita a spolehlivost odpovědí

- [ ] Pro podporované úkoly existuje verzovaná evaluační sada s očekávaným výsledkem. Obsahuje běžné případy, hranice použití a dříve nalezené chyby, v jazycích cílových uživatelů. *Ověření:* projdi případy a jejich hodnoticí kritéria; ověř, že pokrývají skutečné funkce aplikace a neobsahují živá zákaznická data. [Z14]

- [ ] Každý podporovaný úkol má předem stanovené kritérium přijatelné kvality. Samotná plynulost odpovědi nebo souhrnné skóre všech úloh nestačí. *Ověření:* spusť evaluaci a porovnej výsledky po jednotlivých úlohách se zdokumentovanými prahy, včetně počtu případů a použitých verzí. [Z14]

- [ ] Změny modelu, promptu, nástrojů a vyhledávání procházejí regresní evaluací před nasazením. Bez ní může drobná změna zhoršit fungující scénář. *Ověření:* najdi výsledky pro nasazovanou konfiguraci; porovnej je s předchozí verzí a ověř, že neprošla změna porušující stanovená kritéria. [Z10, Z14]

- [ ] Když odpověď uvádí zdroje: citace odkazují na skutečně dostupný podklad podporující tvrzení. Existující URL sama o sobě správnost citace nepotvrzuje. *Ověření:* na evaluační sadě porovnej tvrzení s citovanými pasážemi; ověř i neexistující ID zdroje, nesouvisející pasáž a odkaz na dokument bez oprávnění. [Z14, Z15]

- [ ] Když pro odpověď chybí potřebné podklady: aplikace umí přiznat nedostatek informací. Totéž platí při výpadku vyhledávání nebo nástroje. *Ověření:* spusť případy bez odpovědi v podkladech, s rozpornými podklady a s chybou nástroje; výsledek nesmí tvrdit ověřený fakt ani úspěch neprovedené akce. [Z15]

- [ ] Když chybná odpověď může vážně poškodit zdraví, práva nebo finance člověka: před použitím výsledku je zajištěná kontrola odpovídající dopadu. Obecné upozornění na chybovost kontrolu nenahrazuje. *Ověření (člověk):* vlastník procesu a odborník pro danou oblast projdou chybné i zdánlivě správné výstupy; doloží, kdo a podle čeho rozhoduje o jejich použití. [Z14, Z15]

## Modely a dodávané komponenty

- [ ] Nasazenou AI konfiguraci lze dohledat k jejím zdrojům a verzím. Eviduj model, prompt, připojené nástroje a používané datové podklady. *Ověření:* porovnej evidenci s runtime konfigurací; u proměnlivého aliasu modelu ověř postup zachycení změny a opakování evaluace. [Z16]

- [ ] Když aplikace načítá cizí modelové soubory nebo adaptéry: před použitím ověřuje jejich původ a integritu. Bezpečně pojmenovaný formát ani úspěšný malware scan nezaručují bezpečnost modelu. *Ověření:* zkontroluj zdroj, neměnný identifikátor, hash nebo podpis; ověř, že pozměněný artefakt nasazení odmítne a načítání nepovoluje nedůvěryhodný spustitelný kód. [Z16]

## Zdroje

Zdroje ověřené k 26. 10. 2026. Označení LLM odpovídá vydání OWASP 2026.

- **Z1:** [OWASP Secrets Management Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).
- **Z2:** [OWASP LLM08:2026 Hidden Context Exposure](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM08_HiddenContextExposure.md).
- **Z3:** [OWASP LLM02:2026 Sensitive Information Disclosure](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM02_SensitiveInformationDisclosure.md).
- **Z4:** [OWASP LLM09:2026 Vector and Embedding Weaknesses](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM09_VectorAndEmbeddingWeaknesses.md).
- **Z5:** [OWASP LLM01:2026 Prompt Injection](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM01_PromptInjection.md).
- **Z6:** [OWASP LLM Prompt Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/LLM_Prompt_Injection_Prevention_Cheat_Sheet.html).
- **Z7:** [OWASP LLM05:2026 Data and Model Poisoning](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM05_DataModelPoisoning.md).
- **Z8:** [OWASP LLM10:2026 Improper Output Handling](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM10_ImproperOutputHandling.md).
- **Z9:** [OWASP LLM03:2026 Excessive Agency](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM03_ExcessiveAgency.md).
- **Z10:** [OWASP AI Agent Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).
- **Z11:** [OWASP LLM06:2026 Unbounded Consumption](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM06_UnboundedConsumption.md).
- **Z12:** [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html).
- **Z13:** [GDPR](https://eur-lex.europa.eu/legal-content/cs/ALL/?uri=CELEX%3A32016R0679), zejména čl. 5, 6, 28 a pravidla předávání podle kapitoly V.
- **Z14:** [NIST AI 600-1: Generative Artificial Intelligence Profile](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.600-1.pdf), zejména MEASURE 2.3, 2.5 a 2.13.
- **Z15:** [OWASP LLM07:2026 Misinformation](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM07_Misinformation.md).
- **Z16:** [OWASP LLM04:2026 Supply Chain](https://github.com/GenAI-Security-Project/GenAI-LLM-Top10/blob/main/2026/final/LLM04_SupplyChain.md).
