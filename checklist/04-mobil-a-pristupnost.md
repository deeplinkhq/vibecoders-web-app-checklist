# Mobil a přístupnost

**Týká se:** každého webu.

## Mobil

- [ ] V hlavičce je `<meta name="viewport" content="width=device-width, initial-scale=1">`.
- [ ] Přibližování není zakázané, nikde není `user-scalable=no`.
- [ ] Otestované šířky 320, 375, 390, 768, 1024, 1280 a 1440 px.
- [ ] Nikde není vodorovný scroll. Rychlý test v konzoli: `document.documentElement.scrollWidth > document.documentElement.clientWidth` musí vrátit `false`.
- [ ] Široké prvky (iframe, tabulky) mají vlastní obal s `overflow-x: auto`.
- [ ] Text na mobilu má aspoň 16 px. Pod tuhle hranici Safari na iPhonu po kliknutí do pole stránku samo přiblíží.
- [ ] Úvodní sekce i s tlačítkem se vejde na výšku malého telefonu.

## Dotykové cíle

- [ ] Klikatelné prvky mají aspoň 24x24 px (WCAG 2.2 AA), reálný cíl je 44 až 48 px.
- [ ] Mezi sousedními cíli je aspoň 8 px. Nejčastěji chybí u ikon v patičce.
- [ ] Telefon a e-mail jsou klikatelné odkazy (`tel:`, `mailto:`) s dostatečným okrajem.

## Kontrast

- [ ] Běžný text má kontrast aspoň 4,5:1, velký text (24 px, nebo 18,66 px tučně) aspoň 3:1. Tuhle chybu má 79 % domovských stránek.
- [ ] Rámečky formulářových polí a ikony, které nesou význam, mají aspoň 3:1.
- [ ] Pozor na šedé texty z Tailwindu: `text-gray-400` na bílé neprojde (asi 2,8:1), `text-gray-500` projde těsně.
- [ ] Text přes fotku má ztmavení nebo přechod. Jinak kontrast závisí na tom, jakou fotku tam zrovna dáš.
- [ ] Žádná informace není předaná jen barvou.

## Popisky obrázků a struktura

- [ ] Každý `<img>` má atribut `alt`. Dekorativní obrázek má `alt=""`, prázdný, ale přítomný.
- [ ] Alt popisuje funkci, ne vzhled. Uvnitř odkazu popisuje, kam odkaz vede.
- [ ] Na stránce je právě jeden `<h1>` a nadpisy nepřeskakují úrovně. Úroveň nadpisu je obsah, ne velikost písma.
- [ ] Stránka používá `<header>`, jeden `<main>`, `<nav>`, `<section>` a `<footer>`.
- [ ] `<html lang="cs">` (nebo jiný jazyk webu). Bez toho čte českou stránku anglická hlasová syntéza.
- [ ] Co provádí akci, je `<button>`. Co vede jinam, je `<a href>`. Klikací `<div>` neexistuje.

## Klávesnice

- [ ] Celá stránka jde projít Tabem a je vždy vidět, kde jsi.
- [ ] Nikde není `outline: none` bez náhrady, použij `:focus-visible`. Tohle je nejčastější způsob, jak vibe coded web znepřístupnit.
- [ ] Prvek, na kterém je focus, nezakrývá přilepená hlavička ani cookie lišta (WCAG 2.2).
- [ ] Na začátku stránky je odkaz „Přeskočit na obsah", viditelný při Tabu. Bez něj musí člověk s klávesnicí na každé stránce protabovat celou navigaci.
- [ ] Zavřené mobilní menu není tabovatelné a otevřené jde zavřít Escapem.
- [ ] Focus nikde neuvízne, ani ve vloženém iframu.

## Pohyb

- [ ] Web respektuje `prefers-reduced-motion`. Vestibulární potíže a migrény má přes 20 % dospělých. Stačí globální pojistka v CSS, která v `@media (prefers-reduced-motion: reduce)` zkrátí animace a přechody na 0,01 ms.
- [ ] Nic se nehýbe déle než 5 sekund bez možnosti zastavit. Nic nebliká víc než 3krát za sekundu.

## Jak kontrolovat s agentem

- [ ] Web prošel Lighthouse (záložka v Chrome DevTools) a WAVE nebo axe. Agentovi předávej názvy pravidel (`color-contrast`, `label`, `image-alt`, `frame-title`, `heading-order`), ne skóre.
- [ ] K opravě kontrastu přidej omezení, jinak agent překope barvy podle sebe: „drž aspoň 4,5:1 a neměň barvu značky". Po opravě kontrast přeměř, agent ho jen odhaduje.
- [ ] Neopravují se falešné poplachy: nálezy uvnitř cizího iframu (agent rozbije vložení), oranžová upozornění ve WAVE, kontrast neaktivních prvků, skryté mobilní menu.
- [ ] Oprava není jen umlčení nástroje. `<div role="button">` nález schová, ale klávesnicí to pořád nejde ovládat. Špatná ARIA je horší než žádná.
- [ ] Zbytek prošel člověk. Automat (axe) najde zhruba 57 % chyb, smysluplnost popisků, pořadí fokusu a srozumitelnost hlášek nepozná.
