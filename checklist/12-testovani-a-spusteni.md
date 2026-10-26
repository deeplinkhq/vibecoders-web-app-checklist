# Testování a spuštění

**Týká se:** každého webu.

## Každá změna

- [ ] Projekt má sepsanou „definici hotovo", ideálně v instrukcích pro agenta: změna je vidět na preview, je zkontrolovaná na mobilu, diff obsahuje jen zadané soubory a Lighthouse neklesl.
- [ ] Před sloučením je preview prohlédnuté na počítači i na mobilu a konzole prohlížeče je bez chyb. Když agent „při té příležitosti" přepsal půl webu, pull request zavři a zadej úžeji.
- [ ] Po každém nasazení proběhne dvouminutová kontrola v anonymním okně, včetně odeslání testovacího formuláře.

## Automatické testy

- [ ] Když jde o aplikaci: 3 až 5 hlavních průchodů (registrace a přihlášení, hlavní akce, platba) má automatický test (třeba Playwright) a agent ho pouští po každé změně. Úprava od AI sahá i do souborů, které jsi neotevřel.
- [ ] Test ověřuje výsledek (text na stránce, vzniklý záznam), ne jen to, že se proklikal.
- [ ] Ničivé akce (smazat, zrušit, odebrat) jsou vyzkoušené a mažou správný záznam, ne cizí ani všechny.
- [ ] Víš, že testy průchodů neověřují bezpečnost. Přístup k cizím datům a uniklé klíče se kontrolují zvlášť podle [Bezpečnosti](08-bezpecnost.md).

## Prohlížeče

- [ ] Web je otestovaný v Chrome na počítači, v Safari na iPhonu a v Chrome na Androidu. Safari na iPhonu je povinné, chová se jinak než Chrome i na Macu.
- [ ] Na iPhonu sedí výška prvků přes celou obrazovku. `100vh` počítá i s lištou prohlížeče, použij `100dvh` a stejně ověř.
- [ ] Web je otestovaný na pomalém připojení (DevTools, Slow 4G).

## Před spuštěním

- [ ] Všechny odkazy fungují, včetně patičky a sociálních sítí. Nikde nezůstal `href="#"`.
- [ ] Nikde nezůstal výplňový obsah: lorem ipsum, vymyšlená čísla, ukázkové recenze. U každého čísla na webu víš, odkud je.
- [ ] V kódu nezůstaly `console.log`, TODO komentáře a testovací data.
- [ ] Formulář je vyzkoušený naostro, včetně prázdných polí a chybného vstupu.
- [ ] Lighthouse prošel ve všech čtyřech kategoriích (výkon, přístupnost, osvědčené postupy, SEO).
- [ ] Když jde o aplikaci a chystáš kampaň: limity registrací jsou zvednuté. Supabase s vlastním SMTP má výchozí limit 30 nových uživatelů za hodinu (stav 10/2026).
- [ ] Texty po tobě přečetl někdo další. Překlep v nadpisu působí hůř než pomalé načítání.

## Hned po spuštění

- [ ] Web je otevřený z cizího zařízení a z mobilních dat, s platným certifikátem.
- [ ] Konzole prohlížeče na produkci je bez chyb.
- [ ] Web je odeslaný do Search Console a měření běží.
- [ ] Web prošel někdo, kdo ho nezná, a ty se díváš, kde zaváhá.
