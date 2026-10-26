# SEO a sdílení

**Týká se:** webu, který má být k nalezení ve vyhledávačích nebo se sdílí na sítích. Interní aplikace za přihlášením většinu z toho nepotřebuje.

## Základ

- [ ] Každá stránka má vlastní titulek (50 až 60 znaků) a popis (120 až 158 znaků). Podstatné je vpředu.
- [ ] Nikde nezůstal název ze šablony („Document", „My App").
- [ ] Web běží na jedné adrese. Varianta s www nebo bez a dočasná adresa od hostingu jsou přesměrované na hlavní doménu, jinak vyhledávač vidí duplicitní web.

## Sdílení na sítích

- [ ] Web má vyplněné údaje pro náhled při sdílení (Open Graph): titulek, popis a obrázek 1200x630 px s plnou adresou včetně `https://`. Relativní cesta je nejčastější důvod, proč se náhled nezobrazí.
- [ ] Náhled je vyzkoušený sdílením nebo v nástroji na kontrolu náhledů. Sítě náhledy dlouho drží v paměti.

## Strukturovaná data

- [ ] Když web má strukturovaná data: odpovídají realitě (firma, provozovna) a shodují se s textem na stránce. Agent rád vygeneruje formálně platná, ale nesmyslná data.

## Indexace

- [ ] Web neblokuje vyhledávače. Nezůstal zákaz indexace z vývoje (v `robots.txt` ani v hlavičce stránky). Tohle je nejčastější způsob, jak si zabít celý web.
- [ ] Web má mapu stránek (`sitemap.xml`) a odkaz na ni v `robots.txt`.
- [ ] Rozhodnutí o AI crawlerech je vědomé. Zákaz těch, které sbírají data na trénink, nezablokuje citace v AI vyhledávání. Web, který chce být nalezen, neblokuje nic, nebo jen tréninkové.

## AI vyhledávání

- [ ] Odpovědi jsou přímo na stránce, ne za formulářem nebo v PDF. Co model nenajde, to necituje.
- [ ] Pod nadpisem je přímá odpověď v první jedné až dvou větách.
- [ ] Konkrétní čísla, ceny a jména místo obecných frází. Modely citují ověřitelná tvrzení.
- [ ] Obsah je čitelný i bez JavaScriptu. Řada crawlerů stránku nevykresluje.

## Vyhledávače

- [ ] Web je ověřený v nástroji pro webmastery Googlu (Search Console), s odeslanou mapou stránek. Po pár dnech je zkontrolované, že se stránky indexují.
- [ ] Web je přidaný i do Seznamu a Bingu. Seznam drží v ČR 11 až 15 % vyhledávání a neindexuje tak spolehlivě jako Google, Bing napájí vyhledávání v ChatGPT.

## Lokální služba

- [ ] Když jde o lokální službu: firma má vyplněný profil v mapách Googlu i Seznamu (kategorie, oblast, otevírací doba, telefon, fotky).
- [ ] Když jde o lokální službu: jméno, adresa a telefon jsou znak po znaku stejné na webu i ve všech profilech.
- [ ] Když jde o lokální službu: obec a čtvrť jsou napsané v textu stránky, ne jen v mapě.

## Zdroje

- Google Search Central: titulky, duplicitní adresy, strukturovaná data, robots.txt, AI funkce ve vyhledávání.
- [ogp.me](https://ogp.me): náhledy při sdílení.
- Dokumentace AI crawlerů OpenAI, Anthropic a Applu.
