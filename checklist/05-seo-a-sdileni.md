# SEO a sdílení

**Týká se:** veřejných stránek, které mají být dohledatelné ve vyhledávačích nebo se sdílejí odkazem. U interní aplikace kontroluj jen veřejnou část a případné náhledy sdílených odkazů.

Před kontrolou rozliš URL určené k indexaci, jejich duplicitní varianty a stránky, které ve výsledcích být nemají. Kontroluj nasazený web. U vzorku uveď konkrétní URL a nepovažuj výsledek za kontrolu všech stránek.

## Procházení a indexace

- [ ] Stránky určené k indexaci vracejí po případném přesměrování HTTP `200` a skutečný obsah. Přihlašovací obrazovka nebo CAPTCHA nejsou úspěšné zpřístupnění obsahu crawleru. [G1] *Ověření:* proveď anonymní GET přes `curl`, zkontroluj stav, konečnou URL a tělo odpovědi; dostupnost pro skutečného crawlera dolož také jeho diagnostikou nebo serverovými logy.

- [ ] Pravidla `robots.txt` dovolují cílovým vyhledávačům procházet stránky určené k indexaci. Neexistující `robots.txt` s odpovědí `404` sám o sobě není chyba. [G3] [S5] *Ověření:* stáhni `/robots.txt` a vyhodnoť konkrétní URL pro příslušné user-agenty včetně jejich vlastních skupin pravidel.

- [ ] Stránky určené k indexaci nemají účinný zákaz `noindex`. Zkontroluj HTML i HTTP hlavičky; samotné `index` nepřebije jiný platný zákaz. [G2] *Ověření:* z GET odpovědi vypiš `X-Robots-Tag`, `<meta name="robots">` a pravidla pro konkrétní vyhledávač; u JavaScriptu zkontroluj také výsledný DOM.

- [ ] Když veřejná stránka nemá být indexovaná: crawler může přečíst její `noindex`. Zákaz procházení v `robots.txt` není spolehlivý zákaz zobrazení URL ve výsledcích. [G2] [G3] *Ověření:* ověř dostupnost stránky pro crawlera a přítomnost zákazu; pro Seznam vyžaduj `noindex` v HTML, protože podle jeho dokumentace `X-Robots-Tag` ignoruje, stav 10/2026. [S1]

- [ ] Podstatné informace stránky jsou dostupné jako text v HTML nebo výsledném DOM. Text pouze v obrázku, canvasu nebo CSS `content` nemusí být indexovatelný. [G5] *Ověření:* extrahuj text hlavního obsahu a porovnej ho s informacemi, které stránka skutečně prezentuje.

- [ ] Když obsah vzniká pomocí JavaScriptu: Google při vykreslení získá podstatný obsah stránky. Funkční stránka v běžném prohlížeči sama o sobě průchod vykreslením nedokazuje. [G4] *Ověření (člověk):* v Search Console spusť živý test konkrétní URL a ve vykresleném HTML ověř hlavní obsah i chyby načítání potřebných zdrojů.

- [ ] Když má obsah získávat i crawler bez vykreslování JavaScriptu: podstatný obsah dostane už v HTML odpovědi. Google JavaScript zpracovává, ale tuto schopnost nelze předpokládat u všech robotů. [G4] *Ověření:* stáhni stránku přes `curl` bez přihlášení a porovnej text odpovědi s hlavním obsahem stránky; samotnou závislost na JavaScriptu neoznačuj za automatickou chybu pro Google.

## Odkazy a URL

- [ ] Každá důležitá obsahová stránka má alespoň jeden procházený interní odkaz. Odkaz používá `<a href="…">` s adresou, kterou lze načíst; samotný obslužný kód kliknutí nestačí. [G6] *Ověření:* projdi interní odkazy od úvodní stránky a porovnej nalezené URL se seznamem důležitých stránek.

- [ ] Když web používá nekonečné rolování nebo „Načíst další“: další obsah lze objevit přes samostatné URL a procházené odkazy. Googlebot běžně nekliká na tlačítka ani nespouští načítání rolováním. [G8] *Ověření:* ověř dostupnost další části výpisu přímým GET a dosažitelnost jejích položek přes odkazy.

- [ ] Když je stejný nebo velmi podobný obsah na více URL: duplicity mají zvolenou reprezentativní URL. Použij trvalé přesměrování, pokud má varianta zaniknout, nebo canonical, pokud má zůstat dostupná. [G7] *Ověření:* porovnej obsah variant a jejich přesměrování nebo deklarace canonical.

- [ ] Když stránka deklaruje canonical: deklarace jednoznačně míří na správnou reprezentativní stránku. Chyba v šabloně nesmí posílat všechny podstránky na homepage nebo vývojovou doménu. [G7] *Ověření:* zkontroluj HTML i případnou HTTP hlavičku `Link`, absolutní cílovou URL, její dostupnost a obsahovou odpovídající stránku.

- [ ] Když web používá canonical: sitemap a interní odkazy nepředávají protichůdnou preferenci URL. Canonical je pro Google signál, nikoli záruka jeho výběru. [G7] *Ověření:* porovnej deklaraci s URL v sitemapě a interních odkazech; skutečnou volbu Googlu ověř při kontrole indexace.

- [ ] Když má výpis více očíslovaných stránek s odlišným obsahem: každá má vlastní canonical URL. Druhá a další stránka se nesmějí plošně kanonizovat na první. [G8] *Ověření:* porovnej obsah a canonical alespoň první, následující a poslední dostupné stránky výpisu.

- [ ] Když filtry nebo řazení vytvářejí mnoho URL: procházení nepotřebných kombinací je omezené. Samotný canonical není spolehlivá ochrana před neomezeným procházením filtrů. [G9] *Ověření:* projdi generování parametrů a odkazy mezi kombinacemi; ověř, že zvolená pravidla ponechávají dostupné důležité kategorie a detaily.

- [ ] Když web nabízí jazykové nebo regionální varianty stejné stránky: každá varianta má samostatnou dostupnou URL. Pouhá změna obsahu podle cookie nedává vyhledávači samostatnou adresu varianty. [G10] *Ověření:* načti každou variantu přímým anonymním GET a ověř jazyk jejího hlavního obsahu.

- [ ] Když web používá `hreflang`: deklarace propojují odpovídající varianty obousměrně a zahrnují i samotnou stránku. Používají podporované jazykové a případně regionální kódy, například `cs` nebo `cs-CZ`. [G10] *Ověření:* z HTML, HTTP hlaviček nebo sitemapy sestav vazby a ověř návratové odkazy, cílové URL a jejich jazyk.

## Titulky a popisy

- [ ] Každá stránka určená k indexaci má výstižný `<title>` odpovídající jejímu obsahu a jazyku. Obsahově odlišné stránky mají rozlišitelné titulky; nesmějí zůstat názvy typu „Document“ nebo „My App“. Google neurčuje pevný počet znaků. [G11] *Ověření:* extrahuj titulky, najdi prázdné hodnoty, duplicity a zbytky šablony a porovnej je s obsahem stránek.

- [ ] Každá důležitá obsahová stránka má vlastní relevantní `meta description`. Google nemá pevný znakový limit a může zobrazit jiný úryvek; stránky jedné stránkované série mohou popis sdílet. [G12] [G8] *Ověření:* extrahuj popisy a porovnej je s obsahem; odliš skutečné duplicity od odůvodněné společné šablony.

## Sitemap

- [ ] Když je web nový, rozsáhlý nebo má obtížně objevitelné stránky: má sitemapu pro vyhledávače. U malého a dobře interně propojeného webu její absence sama o sobě není závada. [G13] *Ověření:* porovnej strukturu webu a dostupné sitemapy; případnou nerelevantnost zdůvodni, neodvozuj ji jen z počtu URL.

- [ ] Když web má sitemapu: obsahuje zamýšlené kanonické URL určené k indexaci. Neobsahuje nefunkční stránky, přesměrování ani URL se zákazem indexace. [G14] *Ověření:* zpracuj sitemapu a případné indexy, porovnej je se seznamem zamýšlených stránek a ověř uvedené URL pomocí GET.

- [ ] Když web má sitemapu: její soubor odpovídá protokolu a velikostním limitům. Jedna XML sitemap smí obsahovat nejvýš 50 000 URL a mít nejvýš 52 428 800 bajtů po rozbalení, stav 10/2026. [P1] *Ověření:* ověř XML, UTF-8, absolutní URL, počet záznamů a nekomprimovanou velikost; větší soubor musí být rozdělený.

- [ ] Když má sitemapu zpracovávat Seznam: její absolutní URL je uvedená v `robots.txt`. Seznam tuto cestu oznámení výslovně požaduje, stav 10/2026. [S2] *Ověření:* načti `/robots.txt`, najdi direktivu `Sitemap:` a ověř dostupnost XML odpovědi na uvedené adrese.

- [ ] Když sitemap obsahuje `lastmod`: hodnota odpovídá poslední podstatné změně stránky. Nesmí se automaticky měnit při každém požadavku nebo nasazení bez změny obsahu. [G14] [P1] *Ověření:* porovnej generátor a vzorek dat s historií změn hlavního obsahu; `lastmod` není povinný.

## Náhledy sdílených odkazů

- [ ] Když se stránka sdílí odkazem: její HTML obsahuje Open Graph metadata pro konkrétní stránku. Základ tvoří `og:title`, `og:type`, `og:url` a `og:image`; doplň relevantní `og:description` a popis obrázku `og:image:alt`. [OG1] *Ověření:* načti zdrojové HTML přes GET a ověř hodnoty, jejich vazbu na obsah a správnou identitu stránky v `og:url`.

- [ ] Když náhled používá obrázek: crawler ho může stáhnout z trvalé absolutní HTTPS URL. Obrázek nesmí vyžadovat přihlášení nebo odkaz s krátkou platností. [OG1] [L1] *Ověření:* proveď anonymní GET obrázku, ověř HTTP `200`, skutečný obrazový formát a odpovídající `Content-Type`; zkontroluj případné blokování crawlera.

- [ ] Když se odkaz sdílí na síti s dokumentovanými požadavky na obrázek: obrázek je splňuje. Například LinkedIn pro modul sdílení uvádí nejméně 1200 × 627 px, nejvýš 5 MB a doporučený poměr 1,91:1, stav 10/2026; nejde o univerzální pravidlo Open Graph. [L1] *Ověření:* zjisti rozměry a velikost staženého souboru a porovnej je s aktuální dokumentací cílové sítě.

- [ ] Když se odkaz sdílí na konkrétní síti: její skutečný náhled odpovídá aktuální stránce. Samotná přítomnost tagů nedokazuje správný výběr obrázku ani obnovení cache. [L2] *Ověření (prohlížeč):* použij kontrolní nástroj cílové sítě nebo náhled konceptu příspěvku bez publikování; ověř titulek, obrázek a jeho ořez.

## Strukturovaná data

- [ ] Když stránka obsahuje strukturovaná data: jejich zápis a použité typy odpovídají příslušnému slovníku. Syntakticky platný JSON ještě neznamená správná strukturovaná data. [G15] *Ověření (prohlížeč):* ověř nasazenou URL ve Schema Markup Validatoru; JSON-LD navíc parsuj automaticky a zkontroluj chyby generování.

- [ ] Když stránka obsahuje strukturovaná data: popisují skutečný a uživateli dostupný obsah. Nesmějí obsahovat vymyšlenou firmu, hodnocení, ceny, dostupnost ani data událostí. [G15] *Ověření:* porovnej jednotlivé hodnoty s obsahem stránky a zdrojovými daty, včetně případných rozporů mezi více bloky.

- [ ] Když mají strukturovaná data získat konkrétní rozšířený výsledek Googlu: splňují aktuální požadavky tohoto výsledku. Podporovaný typ a povinné vlastnosti ověřuj podle dokumentace platné v den auditu. [G15] *Ověření (prohlížeč):* spusť Rich Results Test na nasazené URL a vyhodnoť kritické chyby; samotná upozornění ani absence nepodporovaného typu nejsou automaticky chyba.

- [ ] Když firma značí hodnocení sebe sama jako `LocalBusiness` nebo `Organization`: nepočítá s hvězdičkami z vlastních referencí jako s podporovaným review snippetem Googlu. Omezení platí i pro hodnocení vložené cizím widgetem, stav 10/2026. [G16] *Ověření:* zjisti hodnocenou entitu a kdo ovládá stránku; odděl pravdivost recenzí od způsobilosti k rozšířenému výsledku.

## AI crawlery

Rozhodnutí o účasti v AI vyhledávání a jednotlivé AI crawlery jsou v [AI vyhledávání a agenti](16-ai-vyhledavani-a-agenti.md). Tady zůstává jen technická kontrola přístupu.

- [ ] Když má být web dostupný vybranému AI vyhledávači: jeho vyhledávací crawler není nechtěně blokovaný pravidly ani ochranou serveru. Povolení crawlera nezaručuje citaci. [O1] [A1] *Ověření:* zkontroluj účinná pravidla, konfiguraci ochrany a logy skutečných návštěv; GET s podvrženým user-agentem používej jen jako pomocnou diagnostiku.

- [ ] Když má být obsah dostupný jako podklad pro AI odpovědi Googlu: pravidla náhledů neomezují zamýšlené použití. Zkontroluj zejména `nosnippet`, `max-snippet` a `data-nosnippet`; záměrné omezení není chyba. [G17] *Ověření:* porovnej pravidla v HTTP odpovědi a HTML s konkrétním textem určeným k použití a se záměrem provozovatele.

## Google a Seznam

- [ ] Když je Google cílový vyhledávač: provozovatel má ověřenou správnou property v Search Console. Kontrola cizí domény nebo neodpovídajícího URL prefixu nedokládá stav produkčního webu. [G20] *Ověření (člověk):* potvrď přístup k odpovídající property; pokud existuje sitemap, ověř také její úspěšné načtení.

- [ ] Když web už běží: je zkontrolovaný skutečný stav důležitých URL v indexu Googlu. Odliš technickou způsobilost od indexace a zaznamenej případnou jinou canonical URL vybranou Googlem. [G20] [G21] *Ověření:* s oprávněným přístupem použij URL Inspection API a ulož stav, čas posledního procházení a canonical; bez přístupu zařaď kontrolu URL v Search Console do „Ověř ručně“.

- [ ] Když je Seznam cílový vyhledávač: stav důležitých URL je zkontrolovaný také v Seznam Webmasteru. Úspěch v Googlu nedokazuje průchod ani indexaci u Seznamu. [S3] *Ověření:* s oprávněným přístupem použij dokumentované API Seznam Webmasteru pro konkrétní URL; bez přístupu požádej člověka o ověření příslušného webu, stavu URL a hlášených chyb.

## Lokální SEO

- [ ] Když firma přijímá zákazníky na místě nebo za nimi fyzicky jezdí a chce být na Googlu dohledatelná lokálně: má odpovídající spravovaný firemní profil. Čistě online podnikání automaticky nesplňuje podmínky Google Business Profile. [B1] *Ověření (člověk):* ověř způsobilost, vlastnictví a stav profilu; nezakládej duplicitní profil místo převzetí existujícího.

- [ ] Když firma cílí na místní zákazníky v ČR: má odpovídající profil na Firmy.cz. Jeho údaje se používají také na Mapy.com a ve službách Seznamu. [B3] *Ověření:* vyhledej veřejný profil a porovnej firmu a provozovnu; možnost jeho správy nech potvrdit provozovatele.

- [ ] Když firma má lokální profily: jejich veřejné údaje věcně odpovídají webu a skutečné provozovně. Kontroluj název, telefon, web, adresu nebo obsluhovanou oblast a běžnou i mimořádnou otevírací dobu; nevyžaduj shodu formátování znak po znaku. [B1] [B2] *Ověření:* porovnej dostupné údaje pro každou provozovnu; neveřejné nastavení a aktuálnost výjimečných hodin nech potvrdit člověka.

- [ ] Když firma obsluhuje konkrétní území: skutečná lokalita nebo obsluhovaná oblast je uvedená v textu webu. Nevytvářej smyšlené provozovny ani série stránek, které pouze zaměňují názvy měst a neposkytují vlastní hodnotu. [B1] [G22] *Ověření:* extrahuj text lokalit a porovnej stránky mezi sebou i s údaji firmy; samotná vložená mapa nestačí k ověření textové informace.

## Zdroje

Pravidla služeb ověřena 26. 10. 2026. Při pozdějším auditu obnov hlavně dokumentaci AI funkcí, crawlerů, rozšířených výsledků a sociálních náhledů.

- [G1 - Google: technické požadavky pro indexaci][G1].
- [G2 - Google: zákaz indexace pomocí `noindex`][G2].
- [G3 - Google: účel a omezení `robots.txt`][G3].
- [G4 - Google: JavaScript SEO][G4].
- [G5 - Google: SEO pro vývojáře a dostupnost textového obsahu][G5].
- [G6 - Google: procházené odkazy][G6].
- [G7 - Google: canonical a slučování duplicitních URL][G7].
- [G8 - Google: stránkování a postupné načítání][G8].
- [G9 - Google: procházení filtrovaných URL][G9].
- [G10 - Google: jazykové a regionální varianty][G10].
- [G11 - Google: titulky výsledků][G11].
- [G12 - Google: popisy a úryvky][G12].
- [G13 - Google: kdy potřebuješ sitemapu][G13].
- [G14 - Google: vytvoření a odeslání sitemapy][G14].
- [G15 - Google: pravidla strukturovaných dat][G15].
- [G16 - Google: review snippets a vlastní hodnocení firmy][G16].
- [G17 - Google: optimalizace pro generativní AI ve Search][G17].
- [G18 - Google: crawlery a token `Google-Extended`][G18].
- [G19 - Google: Search generative AI control][G19].
- [G20 - Google: URL Inspection][G20].
- [G21 - Google: URL Inspection API][G21].
- [G22 - Google: spam, doorway stránky a obsah vytvářený ve velkém][G22].
- [S1 - Seznam: meta robots a nepodporovaný `X-Robots-Tag`][S1].
- [S2 - Seznam: sitemap][S2].
- [S3 - Seznam Webmaster a jeho API][S3].
- [S4 - Seznam: zákaz tvorby AI odpovědí][S4].
- [S5 - Seznam: `robots.txt` a skupiny pravidel][S5].
- [P1 - Sitemaps.org: protokol a limity][P1].
- [OG1 - Open Graph Protocol][OG1].
- [L1 - LinkedIn: požadavky na sdílený web a obrázky][L1].
- [L2 - LinkedIn: Post Inspector a cache náhledů][L2].
- [O1 - OpenAI: účely a řízení crawlerů][O1].
- [A1 - Anthropic: účely a řízení crawlerů][A1].
- [B1 - Google: pravidla firemních profilů][B1].
- [B2 - Google: úprava údajů firemního profilu][B2].
- [B3 - Firmy.cz: firemní profil a jeho distribuce][B3].

[G1]: https://developers.google.com/search/docs/essentials/technical
[G2]: https://developers.google.com/search/docs/crawling-indexing/block-indexing
[G3]: https://developers.google.com/search/docs/crawling-indexing/robots/intro
[G4]: https://developers.google.com/search/docs/crawling-indexing/javascript/javascript-seo-basics
[G5]: https://developers.google.com/search/docs/fundamentals/get-started-developers
[G6]: https://developers.google.com/search/docs/crawling-indexing/links-crawlable
[G7]: https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls
[G8]: https://developers.google.com/search/docs/specialty/ecommerce/pagination-and-incremental-page-loading
[G9]: https://developers.google.com/crawling/docs/faceted-navigation
[G10]: https://developers.google.com/search/docs/specialty/international/localized-versions
[G11]: https://developers.google.com/search/docs/appearance/title-link
[G12]: https://developers.google.com/search/docs/appearance/snippet
[G13]: https://developers.google.com/search/docs/crawling-indexing/sitemaps/overview
[G14]: https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap
[G15]: https://developers.google.com/search/docs/appearance/structured-data/sd-policies
[G16]: https://developers.google.com/search/docs/appearance/structured-data/review-snippet
[G17]: https://developers.google.com/search/docs/fundamentals/ai-optimization-guide
[G18]: https://developers.google.com/crawling/docs/crawlers-fetchers/google-common-crawlers
[G19]: https://support.google.com/webmasters/answer/16908024?hl=en
[G20]: https://support.google.com/webmasters/answer/9012289?hl=en
[G21]: https://developers.google.com/search/blog/2022/01/url-inspection-api
[G22]: https://developers.google.com/search/docs/essentials/spam-policies
[S1]: https://o-seznam.cz/napoveda/vyhledavani/seznambot/meta-tag-robots/
[S2]: https://o-seznam.cz/napoveda/vyhledavani/seznambot/sitemap-xml/
[S3]: https://o-seznam.cz/napoveda/vyhledavani/seznam-webmaster/
[S4]: https://o-seznam.cz/napoveda/vyhledavani/seznambot/zakaz-tvorby-ai-odpovedi-z-vaseho-webu/
[S5]: https://o-seznam.cz/napoveda/vyhledavani/seznambot/robots-txt/
[P1]: https://www.sitemaps.org/protocol.html
[OG1]: https://ogp.me/
[L1]: https://www.linkedin.com/help/linkedin/answer/a521928
[L2]: https://www.linkedin.com/help/linkedin/answer/a6269011
[O1]: https://developers.openai.com/api/docs/bots
[A1]: https://privacy.anthropic.com/en/articles/8896518-does-anthropic-crawl-data-from-the-web-and-how-can-site-owners-block-the-crawler
[B1]: https://support.google.com/business/answer/3038177
[B2]: https://support.google.com/business/answer/3039617
[B3]: https://napoveda.firmy.cz/zaciname/co-je-firemni-profil/
