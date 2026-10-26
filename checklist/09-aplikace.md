# Aplikace

**Týká se:** aplikace s přihlášením, uživateli, e-maily nebo platbami. Statický web tuhle kategorii přeskočí.

## Než začneš

- [ ] Je rozhodnuté, jestli to vůbec stavět. E-shop s fyzickým zbožím patří na Shoptet nebo Shopify, vibe coduj to, co jinde nekoupíš.
- [ ] Když aplikace pracuje s daty cizích lidí nebo s penězi: projekt má zadání, rozhodnutí zapsaná v repu, testy, dvě prostředí a vědomé vydávání do produkce. Je to pomalejší, ale tady se chyba platí únikem dat.

## Prostředí

- [ ] Vývoj a produkce jsou oddělené: vlastní databáze, vlastní klíče, vlastní proměnné prostředí, vlastní adresa.
- [ ] Do produkce jde změna vědomě, přes pull request a preview, ne automaticky s každým commitem do vývoje.

## Chyby

- [ ] Když něco selže, uživatel vidí srozumitelnou hlášku a ví, co dál. Ne bílou stránku ani technický výpis.

## E-maily

- [ ] Když aplikace posílá e-maily: chodí z vlastní domény přes službu na odesílání (Resend a podobně), s nastavenými DNS záznamy SPF a DKIM.
- [ ] Když aplikace posílá e-maily: klíč pro vývoj a pro produkci je jiný a z vývoje nechodí e-maily skutečným lidem.

## Platby

- [ ] Když aplikace přijímá platby: vývoj běží proti testovacímu režimu platební brány (Stripe sandbox), testovací a ostré klíče jsou oddělené.
- [ ] Když aplikace přijímá platby: stav platby se bere z webhooku od brány, ne z toho, že se uživatel vrátil na stránku „Děkujeme". Webhook ověřuje podpis.

## Obsah

- [ ] Když texty mění někdo, kdo nepracuje s agentem: obsah je v CMS (Sanity a podobně), ne natvrdo v kódu.
