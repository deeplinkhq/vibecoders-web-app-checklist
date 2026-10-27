# AI vyhledávání a agenti

**Týká se:** veřejného webu, který chce být zdrojem AI odpovědí, nebo webu a aplikace, kde mají AI agenti za uživatele vyhledávat, porovnávat nabídky či provádět akce. Obě části vybírej samostatně.

GEO znamená optimalizaci pro generativní vyhledávání. Technická dostupnost obsahu, jeho citování, návštěva webu a dokončená objednávka jsou různé výsledky. Žádná zde uvedená úprava nezaručuje citaci.

Před kontrolou vyber cílové vyhledávače, typy stránek a uživatelské úlohy. Ulož konkrétní URL, datum, použitý nástroj a důkaz. Nedostupné měření označ „Ověř ručně“, chybějící data nepovažuj za nulu.

Související kontroly proveď podle těchto kategorií a jejich nálezy neopakuj:

- [05 SEO a sdílení](05-seo-a-sdileni.md): HTTP odpovědi, `robots.txt`, `noindex`, omezení náhledů, indexace, odkazy, canonical, strukturovaná data a dostupnost hlavního obsahu bez JavaScriptu.
- [04 Mobil a přístupnost](04-mobil-a-pristupnost.md): sémantické HTML, nadpisy, tabulky, názvy a role prvků, popisky, klávesnice a oznamování stavů.
- [06 Formuláře a vložený obsah](06-formulare-a-vlozeny-obsah.md): běžná funkčnost formulářů.
- [08 Bezpečnost](08-bezpecnost.md): autentizace, oprávnění a ochrana akcí.

## Účast v AI vyhledávání a použití obsahu

- [ ] Když provozovatel řeší použití obsahu AI systémy: má samostatně určený záměr pro vyhledávání, načítání na žádost uživatele a trénink. Zákaz tréninku nemusí znamenat zákaz citování a jednotliví provozovatelé mají odlišné ovládání. [O1] [A1] [G7] [S1] *Ověření:* porovnej záměr s tabulkou níže; technické provedení ověř podle kategorie 05 a nejasný záměr označ jako otázku.

| Provozovatel | Rozlišení, stav 10/2026 |
| --- | --- |
| OpenAI | `OAI-SearchBot` slouží vyhledávání, `GPTBot` možnému trénování. `ChatGPT-User` načítá stránky při některých uživatelských akcích; podle dokumentace se na ně pravidla `robots.txt` nemusejí vztahovat. Není přepínačem účasti ve vyhledávání. [O1] |
| Anthropic | `Claude-SearchBot` slouží vyhledávání, `ClaudeBot` možnému trénování a `Claude-User` načítání na žádost uživatele. Dokumentace popisuje jejich samostatné řízení. [A1] |
| Google | Search používá `Googlebot`. `Google-Extended` řídí popsané použití pro trénink Gemini a vybraný grounding mimo Search; neřídí účast v Google Search. Pro generativní funkce Search existuje samostatné nastavení v Search Console. [G7] [G5] |
| Seznam | `Seznam-Extended`, `AI` a `MachineLearning` jsou dokumentované možnosti zákazu použití webu pro AI odpovědi. Neoznačuj je pouze jako zákaz tréninku. [S1] |

- [ ] Když má web získávat viditelnost v generativních funkcích Google Search: účinné nastavení „Search generative AI“ jeho účast dovoluje. Google uvádí celosvětovou dostupnost ovládání od 31. 8. 2026; property může nastavení dědit. [G5] *Ověření (člověk):* ve správné property otevři Settings > Search generative AI, zaznamenej účinnou volbu a případné dědění; nastavení neměň bez rozhodnutí provozovatele.

## Obsah použitelný jako zdroj odpovědi

Následující položky jsou kontroly srozumitelnosti a ověřitelnosti. Nejde o seznam samostatných potvrzených ranking faktorů.

- [ ] Důležité stránky obsahují přímé odpovědi na otázky, kvůli kterým je návštěvník otevře. Odpověď má pojmenovaný předmět a potřebné podmínky; samotný slogan nebo výzva ke kontaktu ji nenahrazují. [M1] *Ověření:* ke každé vybrané stránce přiřaď otázku odvozenou z jejího účelu a dolož pasáž, která na ni odpovídá; nevyžaduj formát FAQ ani pevný počet slov.

- [ ] Podstatná faktická tvrzení mají dohledatelný podklad. U převzatých údajů jde o konkrétní zdroj, u vlastních tvrzení o odpovídající důkaz; odkaz na cizí homepage nestačí. [G2] *Ověření:* vypiš rozhodující tvrzení a otevři jejich podklady; zaznamenej, zda podporují skutečně uvedený závěr, rozsah a podmínky.

- [ ] Když web zveřejňuje vlastní měření nebo srovnání: uvádí způsob jeho vzniku. Bez metodiky nelze odlišit výsledek testu od odhadu nebo reklamního tvrzení. [G2] *Ověření:* u výsledku najdi popis postupu, testovaného vzorku, podmínek a omezení; porovnej zveřejněný závěr s dostupnými výsledky.

- [ ] Identita organizace, značky a produktů je na webu a spravovaných veřejných profilech věcně konzistentní. Obchodní značka může být jiná než právní název, ale jejich vztah nesmí zůstat nejasný. [G3] [M2] *Ověření:* porovnej stránku o provozovateli, kontakty, produktové stránky a dostupné oficiální profily; lokální kontaktní údaje převezmi z kontroly 05 a u případného `sameAs` ověř skutečnou identitu cíle.

- [ ] Když obsah závisí na čase: uvádí období nebo datum platnosti důležitých údajů. Týká se například ceníků, dostupnosti, pravidel a statistik. [M2] *Ověření:* porovnej údaje s aktuálním primárním podkladem a zkontroluj uvedenou platnost; historický údaj musí být rozpoznatelný jako historický.

- [ ] Když stránka uvádí datum vydání nebo aktualizace: datum popisuje skutečnou událost v historii obsahu. Datum článku nesmí představovat termín popisované akce ani se měnit jen kvůli novému sestavení webu. [G4] *Ověření:* porovnej viditelné datum, případná metadata a historii obsahových změn; rozdíl mezi `lastmod` v sitemapě a skutečností řeš v kategorii 05.

- [ ] Když stránka poskytuje odborné rady, analýzu nebo recenzi: je dohledatelné, kdo za obsah odpovídá. Údaje o autorovi nebo odpovědné organizaci nesmějí předstírat neexistující zkušenosti či kvalifikaci. [G2] *Ověření:* projdi uvedené autorství a návazný profil nebo stránku organizace; nedoložitelnou kvalifikaci označ k ověření, nevytvářej ji z textu modelu.

## Měření viditelnosti a přínosu

Pro tyto kontroly neexistuje univerzální minimální podíl citací. Níže uvedený panel dotazů je metodika tohoto checklistu, ne standard vyhledávačů.

- [ ] Když provozovatel vyhodnocuje GEO: používá předem uložený a opakovaně použitelný soubor dotazů. Jednorázová příznivá odpověď nedokládá obvyklou viditelnost. [R1] *Ověření (prohlížeč):* zopakuj stejné dotazy v nových konverzacích cílových systémů; ulož přesné znění, datum, režim vyhledávání, jazyk, dostupné údaje o lokalitě, odpověď a citované URL. Odděl zmínku značky, citaci vlastního webu a věcnou správnost odpovědi; vykazuj počet výskytů i počet pokusů.

- [ ] Když web cílí na generativní funkce Google Search: vyhodnocuje jejich samostatný report v Search Console. Stav 10/2026: dokumentace reportu popisuje imprese pro AI Overviews a AI Mode, nikoli samostatný přehled všech AI návštěv a konverzí. [G6] *Ověření (člověk):* otevři Generative AI performance report, zaznamenej období, stránky, zemi a dostupná data; chybějící report může znamenat nedostatek impresí. Při exportu zachovej informaci o nedostupných hodnotách, které export může převést na nuly.

- [ ] Když web cílí na AI vyhledávání podporované Bingem: vyhodnocuje AI Performance v Bing Webmaster Tools. Počty citací a `Citation Share` nejsou návštěvnost ani pořadí stránky; report nepokrývá celý trh. [M2] [M3] *Ověření (člověk):* zaznamenej období, citované URL a dostupné grounding queries; u Topics Portfolio počítej se stavem beta a přibližnými agregáty, stav 10/2026. Chybějící témata při nedostatku dat neoznačuj jako nulovou viditelnost. [M4]

- [ ] Když web měří obchodní přínos AI vyhledávání: rozlišuje doložené návštěvy a jejich konverze od citací bez prokliku. Chybějící referrer neumožňuje spolehlivě určit zdroj návštěvy. [W1] *Ověření:* v dostupných exportech analytiky nebo logů ověř pravidla přiřazení zdroje a návaznost na konverze; uveď rozsah nepřiřazené návštěvnosti a nepřičítej ji automaticky AI. Zákonnost měření řeš podle kategorie 07.

## Web použitelný pro prohlížející agenty

Agenti mohou používat zdrojové HTML, vykreslený DOM, accessibility tree i screenshoty. Funkčnost bez JavaScriptu proto posuzuj podle zvoleného klienta; nevyžaduj, aby každá interaktivní aplikace fungovala celá bez něj. Sémantiku a dostupnost obsahu ověř podle kategorií 04 a 05. [B1]

- [ ] Když agent porovnává ceny: z dostupného textu nebo podporovaného strojového výstupu jednoznačně přiřadí cenu ke konkrétní nabídce a variantě. Součástí významu ceny je měna, účtované období či jednotka a relevantní podmínky, například DPH nebo cena „od“. [D1] *Ověření:* extrahuj nabídku cestou používanou cílovým klientem a porovnej ji s viditelným ceníkem a zdrojovými daty; neznámou cenu nebo dostupnost nepřeváděj na nulu.

- [ ] Když agent porovnává parametry: strojový výstup zachovává vztah mezi produktem, variantou, názvem parametru a hodnotou. U měřených veličin musí zůstat zachovaná jednotka. [D2] *Ověření:* z vybraných detailů a srovnávacího výpisu vytvoř záznamy parametrů a porovnej je se stránkou; prověř zejména smíchané varianty, tabulky a rozdíl mezi chybějící hodnotou a nulou.

- [ ] Když má agent provádět hlavní uživatelskou úlohu: dokončí její povolenou část ze zadání běžným jazykem. Průchod podle předem připravených selektorů ověřuje automatizaci, ale sám nedokládá použitelnost pro agenta. [B1] *Ověření (prohlížeč):* cílovému agentovi zadej úlohu bez návodu na konkrétní prvky; podle nabídky webu ověř nalezení, porovnání, výběr varianty a vyplnění. Použij testovací data, ulož průběh a konkrétní místo selhání; ostrou platbu ani závazné odeslání kvůli auditu neprováděj.

- [ ] Když má web přijímat legitimní uživatelské agenty: ochrana proti botům neblokuje jejich povolený scénář bez rozlišení. Výjimka založená pouze na textu `User-Agent` nedokazuje identitu klienta. [B2] [B3] *Ověření (prohlížeč):* proveď scénář skutečným cílovým agentem a porovnej ho s bezpečnostními logy; rozliš blokaci, opakovanou challenge, limit požadavků a očekávané předání člověku. Anonymní GET ani podvržený user-agent nepovažuj za důkaz průchodu.

## Volitelná strojová rozhraní

Absence níže uvedených rozhraní sama o sobě není nález „Chybí“. Kontroluj je, když už existují nebo když je požaduje doložený scénář konkrétního klienta. Implementace rozhraní a zvýšení počtu citací jsou různé výsledky.

| Rozhraní | Skutečný stav podpory k 10/2026 | Doložený přínos a hranice důkazu |
| --- | --- | --- |
| `llms.txt` | Komunitní návrh, verze 2 upravená 10. 8. 2026. Existují reálné publikované soubory a nástroje; Lighthouse jeho absenci `404` hodnotí jako nerelevantní. [P1] [L2] | Nabízí stručný rozcestník pro klienta, který ho použije. Google Search výslovně uvádí, že ho pro viditelnost ani ranking nepoužívá. Obecné zvýšení citací v dalších systémech nepotvrzeno. [G1] |
| Markdown verze stránek | Existují implementace samostatných `.md` URL i vyjednání přes `Accept: text/markdown`. Univerzální používání všemi agenty doložené není. [P1] [P2] | Umožňuje předat text s menším množstvím HTML obalu. Zachování obsahu a úsporu tokenů ověř na konkrétním výstupu; zvýšení citací z uvedených zdrojů neplyne. |
| MCP | Otevřený protokol s verzovanou specifikací a podporou ve více agentech a klientech. Podpora konkrétních funkcí vyžaduje kompatibilního klienta a server. [P3] | Zpřístupňuje data a nástroje připojenému klientovi. Samotné vystavení serveru nedokládá jeho automatické objevení vyhledávači ani růst citací. |
| NLWeb | Otevřený projekt s referenčními implementacemi, které projekt označuje jako demonstrace možného řešení. Dokumentuje rozhraní `/ask` a `/mcp`. [P5] [P6] | Umožňuje dotazování nad obsahem webu a přístup přes MCP. Plošná nativní podpora ve vyhledávačích a obecný přínos pro citace nepotvrzeny. |
| Web Bot Auth | Probíhající standardizace IETF; protokol je stále Internet-Draft. Existuje implementace ve službě pro ověřování botů a experimentální podpora některých Google agentů, která nepodepisuje každý požadavek. [B2] [B3] [B4] | Kryptograficky ověřuje identitu podepisujícího klienta. Nepotvrzuje oprávnění uživatele, neškodnost požadavku ani právo provést akci. |
| WebMCP | Samostatný návrh webového API, odlišný od serverového MCP. Chrome dokumentuje origin trial od verze 149; nejde o univerzálně dostupnou vlastnost prohlížečů. [P7] | Umožňuje kompatibilnímu agentovi vyvolat deklarovanou akci stránky. Dokumentované možnosti a dema nenahrazují měření spolehlivosti vlastního scénáře. |

- [ ] Když web publikuje `llms.txt`: soubor vede na existující a aktuální podklady. Rozcestník nesmí poskytovat jiné ceny, pravidla nebo popis produktu než hlavní web. [P1] *Ověření:* stáhni publikovaný soubor, zpracuj jeho odkazy a porovnej obsah s příslušnými stránkami; nezaměňuj ho za `robots.txt`, sitemapu nebo mechanismus oprávnění.

- [ ] Když web poskytuje Markdown verzi stránky: převod zachovává rozhodující informace. Ztráta tabulkových vztahů, varianty produktu nebo podmínek ceny může změnit význam odpovědi agenta. [P1] [P2] *Ověření:* porovnej HTML a Markdown pro stejnou URL, jazyk a stav nabídky; ověř také cíle odkazů a aktuálnost dat.

- [ ] Když stejná URL vyjednává HTML a Markdown podle hlavičky `Accept`: cache rozlišuje obě reprezentace. Jinak může běžný prohlížeč dostat Markdown nebo agent neočekávané HTML. [P2] *Ověření:* proveď GET s `Accept: text/html` a `Accept: text/markdown`, ověř tělo, `Content-Type`, `Vary: Accept` a chování přes nasazenou cache.

- [ ] Když web nabízí MCP: zamýšlený klient skutečně načte a použije deklarované rozhraní. Samotná HTTP odpověď `200` kompatibilitu nedokazuje. [P3] [P4] *Ověření:* proveď inicializaci, načtení dostupných nástrojů či zdrojů a bezpečné testovací volání; ulož vyjednanou verzi protokolu, podporované funkce a výsledek v cílovém klientovi.

- [ ] Když web nabízí NLWeb: odpovědi odpovídají aktuálnímu obsahu a rozsahu webu. Vygenerovaný popis sám o sobě není důkaz pravdivosti výsledku. [P5] [P6] *Ověření:* podle dokumentace nasazené implementace polož dotazy se známým výsledkem i dotaz bez odpovědi v datech; porovnej vrácené URL, položky a údaje s primárním obsahem.

- [ ] Když web vystavuje agentovi akční nástroje: jejich názvy a schémata jednoznačně popisují skutečný účinek. Agent musí rozlišit například zahájení rezervace od jejího závazného vytvoření. [P8] *Ověření:* porovnej deklaraci každého používaného nástroje s implementací a testovacím voláním; ověř význam parametrů i chybové odpovědi.

- [ ] Když agent může provést závaznou nebo obtížně vratnou akci: před provedením existuje účinný krok autorizace nebo potvrzení odpovídající danému toku. Pouhý popis nástroje či anotace není bezpečnostní kontrola. [P9] [P10] *Ověření:* v testovacím prostředí ověř přechod od návrhu k provedení a chování při odmítnutí; serverová oprávnění prověř podle kategorie 08.

- [ ] Když web používá Web Bot Auth: přístupové rozhodnutí vychází z ověřeného podpisu, nikoli z pouhé přítomnosti hlaviček. Identita agenta nenahrazuje přihlášení ani oprávnění uživatele. [B2] [B4] *Ověření:* ověř platný podpis i odmítnutí pozměněného a neplatného požadavku podle nasazené verze protokolu; u klientů, které nepodepisují všechny požadavky, prověř dokumentovanou náhradní cestu ověření.

## Zdroje

Stav podpory a dokumentace ověřen 27. 10. 2026. Při dalším auditu obnov zejména pravidla crawlerů, reporty vyhledávačů a stav experimentálních protokolů.

- [G1] Google: optimalizace pro generativní funkce Search a vyvrácení běžných mýtů.
- [G2] Google: ověřitelnost, původní obsah a pravdivé autorství.
- [G3] Google: identifikace organizace a oficiálních profilů.
- [G4] Google: význam a konzistence dat vydání a aktualizace.
- [G5] Google: Search generative AI control.
- [G6] Google: Generative AI performance report.
- [G7] Google: účel tokenu `Google-Extended`.
- [O1] OpenAI: účely crawlerů a načítání na žádost uživatele.
- [A1] Anthropic: rozlišení crawlerů.
- [S1] Seznam: zákaz použití webu pro AI odpovědi.
- [M1] Microsoft: struktura a konkrétnost obsahu pro AI odpovědi. Doporučení provozovatele, nikoli důkaz univerzálního účinku.
- [M2] Bing: AI Performance a význam základních metrik.
- [M3] Bing: Citation Share, Intents, Topics a Compare.
- [M4] Bing: Topics Portfolio, beta a omezení agregátů.
- [R1] Aggarwal a kol.: GEO, KDD 2024. Experimentální výsledky a jejich omezení.
- [W1] W3C: Referrer Policy.
- [D1] Schema.org: význam nabídky a ceny.
- [D2] Schema.org: produkt a jeho parametry.
- [B1] web.dev: způsoby čtení webu a použitelnost pro agenty.
- [B2] IETF: návrh HTTP Message Signatures for automated traffic.
- [B3] Cloudflare: dokumentovaná implementace Web Bot Auth.
- [B4] Google: experimentální ověřování pomocí Web Bot Auth.
- [P1] `llms.txt`: komunitní návrh, verze 2.
- [P2] Cloudflare: implementace vyjednávání Markdown a oddělení cache.
- [P3] MCP: účel a podpora protokolu.
- [P4] MCP Inspector: ověřování kompatibility a volání.
- [P5] NLWeb: stav a účel projektu.
- [P6] NLWeb: dokumentace referenčního REST API.
- [P7] Chrome: WebMCP a stav origin trial.
- [P8] Chrome: návrh a testování nástrojů WebMCP.
- [P9] Chrome: bezpečnost nástrojů WebMCP.
- [P10] MCP: bezpečnost, souhlas a řízení přístupu.
- [L1] Lighthouse: experimentální audity Agentic Browsing.
- [L2] Lighthouse: volitelnost `llms.txt` a význam výsledku auditu.

[G1]: https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
[G2]: https://developers.google.com/search/docs/fundamentals/creating-helpful-content
[G3]: https://developers.google.com/search/docs/appearance/structured-data/organization
[G4]: https://developers.google.com/search/docs/appearance/publication-dates
[G5]: https://support.google.com/webmasters/answer/16908024?hl=en
[G6]: https://support.google.com/webmasters/answer/16984139
[G7]: https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers
[O1]: https://developers.openai.com/api/docs/bots
[A1]: https://privacy.anthropic.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler
[S1]: https://o-seznam.cz/napoveda/vyhledavani/seznambot/zakaz-tvorby-ai-odpovedi-z-vaseho-webu/
[M1]: https://about.ads.microsoft.com/en/blog/post/october-2025/optimizing-your-content-for-inclusion-in-ai-search-answers
[M2]: https://blogs.bing.com/webmaster/2026/2/Introducing-AI-Performance-in-Bing-Webmaster-Tools-Public-Preview/
[M3]: https://blogs.bing.com/search/2026/6/New-AI-Visibility-Insights-in-Bing-Webmaster-Tools-Intents-Topics-Citation-Share-Compare/
[M4]: https://blogs.bing.com/webmaster/2026/10/introducing-topics-portfolio-beta-in-ai-performance/
[R1]: https://arxiv.org/html/2311.09735v3
[W1]: https://www.w3.org/TR/referrer-policy/
[D1]: https://schema.org/Offer
[D2]: https://schema.org/Product
[B1]: https://web.dev/articles/ai-agent-site-ux
[B2]: https://datatracker.ietf.org/doc/draft-ietf-webbotauth-httpsig-protocol/
[B3]: https://developers.cloudflare.com/bots/reference/bot-verification/web-bot-auth/
[B4]: https://developers.google.com/crawling/docs/crawlers-fetchers/web-bot-auth
[P1]: https://llmstxt.org/
[P2]: https://developers.cloudflare.com/fundamentals/reference/markdown-for-agents/
[P3]: https://modelcontextprotocol.io/docs/getting-started/intro
[P4]: https://modelcontextprotocol.io/docs/tools/inspector
[P5]: https://github.com/nlweb-ai/NLWeb/blob/main/README.md
[P6]: https://github.com/nlweb-ai/NLWeb/blob/main/docs/nlweb-rest-api.md
[P7]: https://developer.chrome.com/docs/ai/webmcp/
[P8]: https://developer.chrome.com/docs/ai/webmcp/best-practices
[P9]: https://developer.chrome.com/docs/ai/webmcp/secure-tools
[P10]: https://modelcontextprotocol.io/specification/2026-07-28
[L1]: https://developer.chrome.com/docs/lighthouse/agentic-browsing/scoring
[L2]: https://developer.chrome.com/docs/lighthouse/agentic-browsing/llms-txt
