# Právo a analytika

**Týká se:** každého webu provozovaného v České republice.

Nejsme právníci a tohle není právní poradenství. Ber to jako seznam otázek, které si máš položit.

## Cookie lišta

- [ ] **PRAVO-1** Když web nepoužívá jiné než technické cookies, cookie lištu nemá. Úřad pro ochranu osobních údajů to říká přímo.
- [ ] **PRAVO-2** Když lišta je: souhlas je předem (opt-in, povinné od 1. 1. 2022) a před souhlasem se nenačte žádný netechnický skript. Na tomhle padá většina webů. Ověř v DevTools, záložka Network, ještě před jakýmkoli kliknutím.
- [ ] **PRAVO-3** Když lišta je: odmítnout jde stejně snadno jako souhlasit, už v první vrstvě. Souhlas jde kdykoli odvolat, text je česky a konkrétní a lišta neblokuje čtení stránky.

## Formulář a GDPR

- [ ] **PRAVO-4** U formuláře je krátká věta o účelu a odkaz na zásady zpracování, viditelné před odesláním.
- [ ] **PRAVO-5** Kontaktní formulář nemá zaškrtávátko „souhlasím se zpracováním". Právní základ je vyřízení poptávky, ne souhlas, a zaškrtávátko je chybný vzor.
- [ ] **PRAVO-6** Je stanovená a napsaná doba uchování dat z formuláře (u dotazů běžně 1 až 3 roky).

## Zásady zpracování

- [ ] **PRAVO-7** Zásady jsou samostatná stránka, odkázaná z patičky i od formuláře. Jsou povinné, jakmile existuje formulář.
- [ ] **PRAVO-8** Obsahují: kdo je správce, jaké údaje a proč, právní základ, dobu uchování, zpracovatele (hosting, analytika, e-maily, formulářová služba), předávání mimo EU, práva lidí a právo stěžovat si u ÚOOÚ.
- [ ] **PRAVO-9** Vygenerované zásady jsou proškrtané a pravdivé. Nepravdivé zásady jsou horší než stručné pravdivé.

## Patička

- [ ] **PRAVO-10** Když web provozuje podnikatel: v patičce je jméno, sídlo nebo místo podnikání, IČO, údaj o zápisu do rejstříku a funkční e-mail (§ 435 občanského zákoníku).

## Newsletter

- [ ] **PRAVO-11** Když web sbírá e-maily na newsletter: souhlas je samostatný, dobrovolný a prokazatelný (§ 7 zákona 480/2004 Sb.). Double opt-in zákon nepředepisuje, ale bez něj souhlas neprokážeš.
- [ ] **PRAVO-12** Každá rozesílka má označení obchodního sdělení, odesílatele a funkční odhlášení.
- [ ] **PRAVO-13** Na adresy z kontaktního formuláře nechodí newsletter. Tohle je reálně největší riziko celé sekce, stěžuje si konkrétní naštvaný člověk.

## Analytika

Rozhodnutí je hlavně o tom, jestli kvůli analytice chceš cookie lištu.

- [ ] **PRAVO-14** Je vědomě vybraná jedna cesta: Google Analytics 4 (nejvíc dat, ale lišta navíc), nebo analytika bez cookies (Plausible, Simple Analytics, analytika hostingu jako Vercel Web Analytics), která lištu nepotřebuje.
- [ ] **PRAVO-15** Když web používá GA4: měřicí kód se načte až po souhlasu, je zapojený Consent Mode v2, jsou přijaté Data Processing Terms a zkrácená retence. Google Tag Manager kvůli jednomu kódu zavádět nemusíš.
- [ ] **PRAVO-16** Když web používá Matomo: cookieless režim je zapnutý, výchozí nastavení cookies používá.
- [ ] **PRAVO-17** Analytický nástroj je uvedený v zásadách zpracování, i když je bez cookies. Souhlas nepotřebuje, informační povinnost ano.

## Co měřit

- [ ] **PRAVO-18** Měří se návštěvy a zdroje, konverzní poměr hlavní akce (odeslání ku návštěvám) a kliky na jednotlivá tlačítka zvlášť, ať víš, které pozice fungují.
- [ ] **PRAVO-19** Neměří se nic, podle čeho bys nic nezměnil. Míra okamžitého opuštění na jednostránkovém webu ani heatmapy většinou nic neřeknou. Realistická laťka: medián konverze landing pages je kolem 6,6 %.

## Přístupnost a zákon

- [ ] **PRAVO-20** Je jasné, jestli se na web vztahuje zákon 424/2023 Sb. (European Accessibility Act, účinný od 28. 6. 2025). Týká se e-shopů, bankovnictví, dopravy, e-knih a dalších vyjmenovaných služeb, mikropodniky (pod 10 zaměstnanců a obrat do 2 mil. EUR) mají výjimku. Prezentační web s kontaktním formulářem tam nespadá.

## Proporce

ÚOOÚ udělil za cookies od ledna 2023 pokuty za 4,4 mil. Kč celkem a předtím poslal přes 120 varovných dopisů. Míří na velké weby s marketingovým sledováním. Když nepoužiješ GA4 ani reCAPTCHu, odpadne lišta úplně a zbyde stránka se zásadami a pár řádků v patičce.
