# SEO a sdílení

**Týká se:** webu, který má být k nalezení ve vyhledávačích nebo se sdílí na sítích. Interní aplikace za přihlášením většinu z toho nepotřebuje.

## Základ

- [ ] **SEO-1** `<title>` má 50 až 60 znaků, je unikátní pro každou stránku, klíčové slovo je na začátku, značka na konci.
- [ ] **SEO-2** Meta description má 120 až 158 znaků, podstatné je vpředu (na mobilu je vidět zhruba 110).
- [ ] **SEO-3** V hlavičce nezůstalo „Document", „Vite App" ani jiný název ze šablony.
- [ ] **SEO-4** `<meta charset="utf-8">`, jinak se v náhledech rozbije diakritika.
- [ ] **SEO-5** Každá stránka má canonical odkaz sama na sebe, na finální doméně.
- [ ] **SEO-6** Web neběží duplicitně na adrese od hostingu (`nazev.vercel.app` a podobně). Ta je přesměrovaná, nebo má canonical na vlastní doménu.
- [ ] **SEO-7** Hreflang u čistě jednojazyčného webu nepotřebuješ.

## Sdílení na sítích

- [ ] **SEO-8** Jsou vyplněné `og:title`, `og:description`, `og:image`, `og:url`, `og:type` a `og:locale` (`cs_CZ`).
- [ ] **SEO-9** OG obrázek je JPG nebo PNG (ne SVG), 1200x630 px, do 5 MB, s absolutní adresou včetně `https://`. Relativní cesta je nejčastější důvod, proč se náhled nezobrazí.
- [ ] **SEO-10** `twitter:card` je `summary_large_image`.
- [ ] **SEO-11** Náhled je ověřený v debuggeru (Facebook Sharing Debugger, opengraph.xyz, metatags.io). Sítě náhledy dlouho drží v mezipaměti, po opravě je potřeba je obnovit.

## Strukturovaná data

- [ ] **SEO-12** Strukturovaná data jsou jako JSON-LD v `<head>`, ne Microdata.
- [ ] **SEO-13** Typ odpovídá realitě: `LocalBusiness` s `name` a `address`, když existuje provozovna, jinak `Organization`.
- [ ] **SEO-14** Žádné `FAQPage`. Google tyhle výsledky zrušil od 7. 5. 2026 a pro AI odpovědi speciální markup nepotřebuješ. Otázky a odpovědi stačí jako obyčejné HTML.
- [ ] **SEO-15** Údaje v JSON-LD se shodují s viditelným textem na stránce.
- [ ] **SEO-16** Ověřeno v Rich Results Test. Agent rád vygeneruje platný, ale typově nesmyslný JSON-LD.

## Indexace

- [ ] **SEO-17** `robots.txt` existuje a neobsahuje `Disallow: /`. Tohle je nejčastější způsob, jak si zabít celý web.
- [ ] **SEO-18** Nikde nezůstal `<meta name="robots" content="noindex">` z vývoje. Pozor, `Disallow` v `robots.txt` indexaci nebrání, jen vyhledávači zabrání přečíst `noindex`.
- [ ] **SEO-19** `sitemap.xml` existuje a v `robots.txt` je na ni řádek `Sitemap:`. Takhle ji najde i Seznam.
- [ ] **SEO-20** Vyhledávačům nejsou zakázané CSS a JavaScript.
- [ ] **SEO-21** Rozhodnutí o AI crawlerech je vědomé. Od 2026 se dělí na tréninkové (GPTBot, ClaudeBot, Google-Extended, Applebot-Extended) a vyhledávací (OAI-SearchBot, Claude-SearchBot, PerplexityBot). Zákaz tréninkových nezablokuje citace v AI vyhledávání. Web, který chce být nalezen, neblokuje nic, nebo jen tréninkové.

## AI vyhledávání

- [ ] **SEO-22** Odpovědi jsou na stránce, ne za formulářem nebo v PDF. Co model nenajde, to necituje.
- [ ] **SEO-23** Text je psaný od odpovědi: pod nadpisem je přímá odpověď v první jedné až dvou větách.
- [ ] **SEO-24** Nadpisy jsou formulované jako otázky, které lidé reálně píšou.
- [ ] **SEO-25** Konkrétní čísla, ceny a jména místo obecných frází. Modely citují ověřitelná tvrzení.
- [ ] **SEO-26** Obsah je čitelný bez JavaScriptu. Řada AI crawlerů stránku nevykresluje, statické HTML je tady výhoda.
- [ ] **SEO-27** Žádný `llms.txt`. Google v červnu 2026 potvrdil, že ho žádný z AI systémů nepoužívá.

## Search Console a další nástroje

- [ ] **SEO-28** Web je v Google Search Console jako doménová vlastnost ověřená DNS záznamem (pokryje www i bez www najednou).
- [ ] **SEO-29** Sitemapa je odeslaná a po pár dnech je zkontrolovaný přehled indexace. Ruční opatření a bezpečnostní problémy jsou prázdné.
- [ ] **SEO-30** Web je v Bing Webmaster Tools (import ze Search Console na dvě kliknutí). Bing napájí ChatGPT search a Copilot.

## Česko

- [ ] **SEO-31** Web je v Seznam Webmaster (reporter.seznam.cz/wm). Seznam drží 11 až 15 % vyhledávání a neindexuje tak spolehlivě jako Google.
- [ ] **SEO-32** Když jde o lokální službu: založený a vyplněný Google Business Profile (kategorie, oblast, otevírací doba, telefon, aspoň 5 fotek). Google má v ČR zhruba 80 % vyhledávání.
- [ ] **SEO-33** Když jde o lokální službu: zápis na Firmy.cz, který se propisuje do Mapy.cz.
- [ ] **SEO-34** Když jde o lokální službu: jméno, adresa a telefon jsou znak po znaku stejné na webu, v Google profilu i na Firmy.cz.
- [ ] **SEO-35** Když jde o lokální službu: obec a čtvrť jsou v textu stránky, ne jen v mapě.
