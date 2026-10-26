# Mobil a přístupnost

**Týká se:** každého webu.

## Mobil

- [ ] Web se přizpůsobí šířce telefonu a přibližování není zakázané.
- [ ] Otestované šířky od 320 px (malý telefon) po 1440 px (velký monitor).
- [ ] Nikde není vodorovný scroll. Široké prvky (tabulky, vložené mapy) se posouvají uvnitř sebe, ne celá stránka.
- [ ] Text na mobilu má aspoň 16 px. Pod tuhle hranici iPhone po kliknutí do pole stránku samo přiblíží.
- [ ] Úvodní sekce i s hlavním tlačítkem se vejde na výšku malého telefonu.

## Dotykové cíle

- [ ] Tlačítka a odkazy jsou dost velké na prst, ideálně 44 až 48 px, a mezi sousedními je mezera. Nejčastěji chybí u ikon v patičce.
- [ ] Telefon a e-mail jsou klikatelné odkazy.

## Kontrast

- [ ] Běžný text má kontrast aspoň 4,5:1, velký text aspoň 3:1. Tuhle chybu má 79 % domovských stránek, nejčastěji u světle šedého textu.
- [ ] Rámečky formulářových polí a ikony, které nesou význam, mají kontrast aspoň 3:1.
- [ ] Text přes fotku má ztmavení. Jinak kontrast závisí na tom, jakou fotku tam zrovna dáš.
- [ ] Žádná informace není předaná jen barvou.

## Obrázky a struktura

- [ ] Každý obrázek má popisek (alt). Dekorativní obrázek má popisek prázdný.
- [ ] Popisek říká, co obrázek sděluje, ne jak vypadá. U obrázku v odkazu říká, kam odkaz vede.
- [ ] Stránka má jeden hlavní nadpis a nadpisy nepřeskakují úrovně. Úroveň nadpisu je obsah, ne velikost písma.
- [ ] Stránka má nastavený jazyk. Bez toho čte českou stránku anglická hlasová syntéza.
- [ ] Co provádí akci, je tlačítko. Co vede jinam, je odkaz. Klikací obyčejný blok neexistuje.

## Klávesnice

- [ ] Celá stránka jde projít Tabem a je vždy vidět, kde jsi. Agent rád zvýraznění fokusu vypne, protože „ruší design".
- [ ] Na začátku stránky je odkaz „Přeskočit na obsah", viditelný při Tabu.
- [ ] Prvek s fokusem nezakrývá přilepená hlavička ani cookie lišta.
- [ ] Mobilní menu jde zavřít Escapem a zavřené se Tabem neprochází.

## Pohyb

- [ ] Web respektuje nastavení „omezit pohyb" v systému. Vestibulární potíže a migrény má přes 20 % dospělých.
- [ ] Nic se nehýbe déle než 5 sekund bez možnosti zastavit. Nic nebliká víc než 3krát za sekundu.

## Jak kontrolovat s agentem

- [ ] Web prošel automatickým auditem přístupnosti a agent dostal konkrétní nálezy, ne skóre.
- [ ] K opravě kontrastu je přidané omezení, jinak agent překope barvy podle sebe: „drž aspoň 4,5:1 a neměň barvu značky". Po opravě je kontrast přeměřený, agent ho jen odhaduje.
- [ ] Oprava není jen umlčení nástroje. Když agent přidá blok s rolí tlačítka, nález zmizí, ale klávesnicí to pořád nejde ovládat.
- [ ] Zbytek prošel člověk. Automat najde zhruba polovinu chyb, smysluplnost popisků a srozumitelnost hlášek nepozná.
