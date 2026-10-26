# Testování a spuštění

**Týká se:** každého webu.

## Každá změna

- [ ] **TEST-1** Projekt má sepsanou „definici hotovo", ideálně v instrukcích pro agenta: změna je vidět na preview, je zkontrolovaná na mobilu, diff obsahuje jen zadané soubory a Lighthouse neklesl.
- [ ] **TEST-2** Před sloučením je preview prohlédnuté na počítači i na mobilu a konzole prohlížeče je bez chyb. Když agent „při té příležitosti" přepsal půl webu, pull request zavři a zadej úžeji.
- [ ] **TEST-3** Po každém nasazení proběhne dvouminutová kontrola v anonymním okně, včetně odeslání testovacího formuláře.

## Prohlížeče

- [ ] **TEST-4** Web je otestovaný v Chrome na počítači, v Safari na iPhonu a v Chrome na Androidu. Safari na iPhonu je povinné, chová se jinak než Chrome i na Macu.
- [ ] **TEST-5** Na iPhonu sedí výška prvků přes celou obrazovku. `100vh` počítá i s lištou prohlížeče, použij `100dvh` a stejně ověř.
- [ ] **TEST-6** Web je otestovaný na pomalém připojení (DevTools, Slow 4G).

## Před spuštěním

- [ ] **TEST-7** Všechny odkazy fungují, včetně patičky a sociálních sítí. Nikde nezůstal `href="#"`.
- [ ] **TEST-8** Nikde nezůstal výplňový obsah: lorem ipsum, vymyšlená čísla, ukázkové recenze. U každého čísla na webu víš, odkud je.
- [ ] **TEST-9** V kódu nezůstaly `console.log`, TODO komentáře a testovací data.
- [ ] **TEST-10** Formulář je vyzkoušený naostro, včetně prázdných polí a chybného vstupu.
- [ ] **TEST-11** Lighthouse prošel ve všech čtyřech kategoriích (výkon, přístupnost, osvědčené postupy, SEO).
- [ ] **TEST-12** Texty po tobě přečetl někdo další. Překlep v nadpisu působí hůř než pomalé načítání.

## Hned po spuštění

- [ ] **TEST-13** Web je otevřený z cizího zařízení a z mobilních dat, s platným certifikátem.
- [ ] **TEST-14** Konzole prohlížeče na produkci je bez chyb.
- [ ] **TEST-15** Web je odeslaný do Search Console a měření běží.
- [ ] **TEST-16** Web prošel někdo, kdo ho nezná, a ty se díváš, kde zaváhá.
