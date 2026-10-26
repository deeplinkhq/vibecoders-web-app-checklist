# SEO a sdílení

**Týká se:** webu, který má být k nalezení ve vyhledávačích nebo se sdílí na sítích. Interní aplikace za přihlášením většinu z toho nepotřebuje.

## Základ

- [ ] `<title>` má 50 až 60 znaků, je unikátní pro každou stránku, klíčové slovo je na začátku, značka na konci.
- [ ] Meta description má 120 až 158 znaků, podstatné je vpředu (na mobilu je vidět zhruba 110).
- [ ] V hlavičce nezůstalo „Document", „Vite App" ani jiný název ze šablony.
- [ ] `<meta charset="utf-8">`, jinak se v náhledech rozbije diakritika.
- [ ] Každá stránka má canonical odkaz sama na sebe, na finální doméně.
- [ ] Web neběží duplicitně na adrese od hostingu (`nazev.vercel.app` a podobně). Ta je přesměrovaná, nebo má canonical na vlastní doménu.
- [ ] Hreflang u čistě jednojazyčného webu nepotřebuješ.

## Sdílení na sítích

- [ ] Jsou vyplněné `og:title`, `og:description`, `og:image`, `og:url`, `og:type` a `og:locale` (`cs_CZ`).
- [ ] OG obrázek je JPG nebo PNG (ne SVG), 1200x630 px, do 5 MB, s absolutní adresou včetně `https://`. Relativní cesta je nejčastější důvod, proč se náhled nezobrazí.
- [ ] `twitter:card` je `summary_large_image`.
- [ ] Náhled je ověřený v debuggeru (Facebook Sharing Debugger, opengraph.xyz, metatags.io). Sítě náhledy dlouho drží v mezipaměti, po opravě je potřeba je obnovit.

## Strukturovaná data

- [ ] Strukturovaná data jsou jako JSON-LD v `<head>`, ne Microdata.
- [ ] Typ odpovídá realitě: `LocalBusiness` s `name` a `address`, když existuje provozovna, jinak `Organization`.
- [ ] `FAQPage` se nepřidává kvůli vzhledu ve výsledcích. Google tyhle rozšířené výsledky zrušil od 7. 5. 2026, otázky a odpovědi stačí jako obyčejné HTML.
- [ ] Údaje v JSON-LD se shodují s viditelným textem na stránce.
- [ ] Ověřeno v Rich Results Test. Agent rád vygeneruje platný, ale typově nesmyslný JSON-LD.

## Indexace

- [ ] `robots.txt` existuje a neobsahuje `Disallow: /`. Tohle je nejčastější způsob, jak si zabít celý web.
- [ ] Nikde nezůstal `<meta name="robots" content="noindex">` z vývoje. Pozor, `Disallow` v `robots.txt` indexaci nebrání, jen vyhledávači zabrání přečíst `noindex`.
- [ ] `sitemap.xml` existuje a v `robots.txt` je na ni řádek `Sitemap:`. Takhle ji najde i Seznam.
- [ ] Vyhledávačům nejsou zakázané CSS a JavaScript.
- [ ] Rozhodnutí o AI crawlerech je vědomé. Od 2026 se dělí na tréninkové (GPTBot, ClaudeBot, Google-Extended, Applebot-Extended) a vyhledávací (OAI-SearchBot, Claude-SearchBot, PerplexityBot). Zákaz tréninkových nezablokuje citace v AI vyhledávání. Web, který chce být nalezen, neblokuje nic, nebo jen tréninkové.

## AI vyhledávání

- [ ] Odpovědi jsou na stránce, ne za formulářem nebo v PDF. Co model nenajde, to necituje.
- [ ] Text je psaný od odpovědi: pod nadpisem je přímá odpověď v první jedné až dvou větách.
- [ ] Nadpisy jsou formulované jako otázky, které lidé reálně píšou.
- [ ] Konkrétní čísla, ceny a jména místo obecných frází. Modely citují ověřitelná tvrzení.
- [ ] Obsah je čitelný bez JavaScriptu. Řada AI crawlerů stránku nevykresluje, statické HTML je tady výhoda.
- [ ] `llms.txt` není priorita. Google v červnu 2026 napsal, že pro jeho vyhledávání není potřeba a nepomáhá ani neškodí. U ostatních AI vyhledávačů to není potvrzené.

## Search Console a další nástroje

- [ ] Web je v Google Search Console jako doménová vlastnost ověřená DNS záznamem (pokryje www i bez www najednou).
- [ ] Sitemapa je odeslaná a po pár dnech je zkontrolovaný přehled indexace. Ruční opatření a bezpečnostní problémy jsou prázdné.
- [ ] Web je v Bing Webmaster Tools (import ze Search Console na dvě kliknutí). Bing napájí ChatGPT search a Copilot.

## Česko

- [ ] Když se obsah webu často mění: změněné adresy se posílají přes IndexNow. Podporuje ho Seznam i Bing (Google ne), nová stránka se tak do Seznamu dostane dřív.
- [ ] Web je v Seznam Webmaster (reporter.seznam.cz/wm). Seznam drží 11 až 15 % vyhledávání a neindexuje tak spolehlivě jako Google.
- [ ] Když jde o lokální službu: založený a vyplněný Google Business Profile (kategorie, oblast, otevírací doba, telefon, aspoň 5 fotek). Google má v ČR zhruba 80 % vyhledávání.
- [ ] Když jde o lokální službu: zápis na Firmy.cz, který se propisuje do Mapy.cz.
- [ ] Když jde o lokální službu: jméno, adresa a telefon jsou znak po znaku stejné na webu, v Google profilu i na Firmy.cz.
- [ ] Když jde o lokální službu: obec a čtvrť jsou v textu stránky, ne jen v mapě.
