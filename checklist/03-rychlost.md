# Rychlost, obrázky a fonty

**Týká se:** každého webu.

## Metriky

- [ ] Hlavní obsah se načte do 2,5 s, stránka reaguje na kliknutí do 200 ms a při načítání neposkakuje (Core Web Vitals: LCP, INP, CLS).
- [ ] Rychlost je změřená na mobilu a na pomalejším připojení, ne jen na tvém počítači na optice. Nový web ještě nemá data od reálných návštěvníků, vidíš jen laboratorní měření.

## Obrázky

- [ ] Žádný obrázek není v originále z foťáku. 4000x3000 px a 6 MB je 20 až 40krát víc, než je potřeba.
- [ ] Fotky jsou v moderním formátu (WebP, AVIF), ne v PNG nebo velkém JPG.
- [ ] Loga a ikony jsou ve vektoru (SVG). Nerozmažou se na žádném displeji.
- [ ] Úvodní obrázek má nejvýš 200 KB, ostatní obrázky pod 100 až 200 KB.
- [ ] Celá stránka má ideálně pod 1 MB, tvrdý strop 2 MB.
- [ ] Žádný velký obrázek není jen zmenšený stylem. Prohlížeč stáhne celý soubor a pak ho zahodí.
- [ ] Obrázky mají zadané rozměry, takže stránka při načítání neposkakuje. Je to nejčastější příčina poskakování.
- [ ] Úvodní obrázek se načítá hned a přednostně, obrázky níž na stránce až při rolování.

## Fonty

- [ ] Fonty jsou součástí webu, ne načítané z cizího serveru. Je to rychlejší a odpadne problém s GDPR.
- [ ] Fonty obsahují českou diakritiku a jsou jen v řezech, které se opravdu používají.
- [ ] Text je vidět hned, i než se font načte - existuje vybraný záložní základní font, který je podobný tomu vlastnímu

## Vývojové nástroje v produkci

- [ ] Na produkci neběží nic, co je určené jen pro vývoj: knihovny, které generují styly až v prohlížeči, vývojové verze knihoven, ladicí výpisy. Agent je použije, protože je to nejrychlejší cesta k funkčnímu výsledku.
- [ ] Rychlý hosting nespraví pomalý web. Kompresi a doručení řeší hosting, velikost obrázků a množství kódu ne.

## Zdroje

- [web.dev](https://web.dev): Core Web Vitals, fonty, obrázky.
