# Aplikace

**Týká se:** aplikace s přihlášením, uživateli, e-maily nebo platbami. Statický web tuhle kategorii přeskočí.

## Než začneš

- [ ] Je rozhodnuté, jestli to vůbec stavět. E-shop s fyzickým zbožím patří na Shoptet nebo Shopify, vibe coduj to, co jinde nekoupíš.
- [ ] Když aplikace pracuje s daty cizích lidí nebo s penězi: projekt má zadání, rozhodnutí zapsaná v repu, testy, dvě prostředí a vědomé vydávání do produkce. Je to pomalejší, ale tady se chyba platí únikem dat.

## Prostředí

- [ ] Vývoj a produkce jsou oddělené: vlastní databáze, vlastní klíče, vlastní proměnné prostředí, vlastní adresa.
- [ ] Do produkce jde změna vědomě, přes pull request a preview, ne automaticky s každým commitem do vývoje.

## Přihlášení

- [ ] Adresa webu a povolené adresy pro přesměrování v nastavení přihlášení míří na produkční doménu, ne na `localhost`. Jinak odkazy z potvrzovacích e-mailů a resetu hesla vedou na tvůj počítač.
- [ ] Potvrzení e-mailu a reset hesla jsou vyzkoušené naostro až po kliknutí na odkaz v doručeném e-mailu. U vlastního SMTP je vypnuté měření prokliků, jinak se jednorázový odkaz spotřebuje.
- [ ] Hláška při přihlášení a resetu hesla neprozrazuje, jestli účet existuje („Pokud účet existuje, poslali jsme e-mail").
- [ ] Odhlášení a změna hesla zneplatní přihlášení i na serveru, ne jen smažou cookie v prohlížeči.
- [ ] Uživatel si nemůže sám nastavit roli ani příznak admin. Role se nebere z dat od prohlížeče, v Supabase ani z `user_metadata`, kterou si uživatel může přepsat.

## Soubory

- [ ] Když uživatelé nahrávají soubory: úložiště je privátní, soubory se zobrazují přes dočasné podepsané odkazy a kontroluje se typ i velikost. Veřejné úložiště otevře kdokoli, kdo uhodne adresu.

## Chyby

- [ ] Když něco selže, uživatel vidí srozumitelnou hlášku a ví, co dál. Ne bílou stránku ani technický výpis.
- [ ] Selhání se neschovává: v kódu není prázdný `catch` a chyba při načítání dat se netváří jako prázdný seznam nebo „nejsi přihlášený". Je to nová kategorie OWASP Top 10 2025 a agent ji dělá běžně.

## E-maily

- [ ] Když přihlášení běží přes Supabase: je nastavený vlastní SMTP. Výchozí služba posílá jen členům týmu projektu a nejvýš 2 e-maily za hodinu, registrace cizích lidí neprojde (stav 10/2026).
- [ ] Když aplikace posílá e-maily: chodí z vlastní domény přes službu na odesílání (Resend a podobně), s nastavenými DNS záznamy SPF a DKIM.
- [ ] Když aplikace posílá e-maily: klíč pro vývoj a pro produkci je jiný a z vývoje nechodí e-maily skutečným lidem.

## Platby

- [ ] Když aplikace přijímá platby: vývoj běží proti testovacímu režimu platební brány (Stripe sandbox), testovací a ostré klíče jsou oddělené.
- [ ] Když aplikace přijímá platby: stav platby se bere z webhooku od brány, ne z toho, že se uživatel vrátil na stránku „Děkujeme". Webhook ověřuje podpis.
- [ ] Když aplikace přijímá platby: webhook zpracuje stejnou událost jen jednou (eviduje její ID) a nespoléhá na pořadí. Stripe píše, že událost může přijít víckrát a pořadí není zaručené.

## Obsah

- [ ] Když texty mění někdo, kdo nepracuje s agentem: obsah je v CMS (Sanity a podobně), ne natvrdo v kódu.
