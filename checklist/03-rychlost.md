# Rychlost, obrázky a fonty

**Týká se:** každého webu.

## Metriky

- [ ] **RYCH-1** LCP pod 2,5 s, INP pod 200 ms, CLS pod 0,1. FID už neexistuje, v roce 2024 ho nahradilo INP.
- [ ] **RYCH-2** Měřeno v PageSpeed Insights nebo Lighthouse. Google hodnotí 75. percentil reálných návštěv za 28 dní, ne tvůj počítač na optice. Nový web reálná data ještě nemá, vidíš jen laboratorní výsledek.

## Obrázky

- [ ] **RYCH-3** Žádný obrázek není v originále z foťáku. 4000x3000 px a 6 MB je 20 až 40krát víc, než je potřeba.
- [ ] **RYCH-4** Fotky jsou ve WebP, případně AVIF (o 20 až 30 % menší). PNG jen jako záloha přes `<picture>`.
- [ ] **RYCH-5** Loga, ikony a piktogramy jsou SVG. Nerozmažou se na displejích s vysokým rozlišením.
- [ ] **RYCH-6** Úvodní obrázek má šířku 1600 až 1920 px a nejvýš 200 KB, ideálně 100 až 150 KB.
- [ ] **RYCH-7** Ostatní obrázky mají pod 100 až 200 KB, kvalita komprese 80 až 85.
- [ ] **RYCH-8** Celá stránka má ideálně pod 1 MB, tvrdý strop 2 MB.
- [ ] **RYCH-9** Žádný velký obrázek není zmenšený jen přes CSS. Prohlížeč stáhne celý soubor a pak ho zahodí.
- [ ] **RYCH-10** Každý `<img>` má `width` a `height` podle skutečné velikosti souboru (a v CSS `height: auto`). Chybějící rozměry jsou nejčastější příčina poskakování stránky (CLS), týká se 62 % mobilních stránek.
- [ ] **RYCH-11** Úvodní obrázek má `fetchpriority="high"` a nikdy `loading="lazy"`.
- [ ] **RYCH-12** Všechno pod zlomem má `loading="lazy"`. Pravidlo: vidím to bez scrollování? Pak se načítá hned.
- [ ] **RYCH-13** `srcset` a `sizes` jen u úvodního obrázku a velkých fotek přes celou šířku. U malých obrázků je to zbytečná složitost.

## Fonty

- [ ] **RYCH-14** Fonty jsou v projektu, ne načítané z Google Fonts. Medián zlepšení LCP zhruba 180 ms a odpadne problém s GDPR.
- [ ] **RYCH-15** Fonty jsou ve WOFF2, se sadou znaků `latin-ext` (jinak chybí česká diakritika) a jen v řezech, které se opravdu používají.
- [ ] **RYCH-16** `font-display: swap`, jinak je text chvíli neviditelný.
- [ ] **RYCH-17** Přednačtený (`preload`) je jen jeden hlavní řez, s atributem `crossorigin`. Přednačítání všeho konkuruje úvodnímu obrázku.
- [ ] **RYCH-18** Zváženo, jestli nestačí systémový font. Nejrychlejší font je žádný font.

## Vývojářské nástroje v produkci

- [ ] **RYCH-19** Na produkci neběží Tailwind Play CDN (`cdn.tailwindcss.com`). Generuje CSS až v prohlížeči a rozbíjí LCP i INP. Místo něj build, třeba samostatné Tailwind CLI s `--minify` (10 až 30 KB místo stovek).
- [ ] **RYCH-20** Na produkci není vývojová verze knihoven ani zdrojové mapy (`.map`), pokud je tam nechceš schválně.

## Co za tebe udělá hosting

- [ ] **RYCH-21** Víš, co hosting dělá sám a co ne. Moderní hosting (Vercel, Netlify, Cloudflare Pages) řeší kompresi, CDN, HTTPS a HTTP/2. Nezmenší obrázky u statického webu, nezbuilduje CSS a nespraví obsah. Rychlý hosting nespraví pomalý web.
