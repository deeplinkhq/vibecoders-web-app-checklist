# Aplikace

**Týká se:** aplikace s přihlášením, uživateli, e-maily nebo platbami. Statický web tuhle kategorii přeskočí.

## Než začneš

- [ ] Je rozhodnuté, jestli to vůbec stavět. Na běžné věci (e-shop s fyzickým zbožím, rezervace) existují hotové služby. Vibe coduj to, co jinde nekoupíš.
- [ ] Když aplikace pracuje s daty cizích lidí nebo s penězi: má zadání, testy, oddělený vývoj a produkci a vědomé vydávání nových verzí. Je to pomalejší, ale tady se chyba platí únikem dat.

## Prostředí

- [ ] Vývoj a produkce jsou oddělené: vlastní data, vlastní klíče, vlastní adresa.
- [ ] Nová verze jde do produkce vědomě, až po vyzkoušení, ne automaticky s každou změnou.

## Přihlášení

- [ ] Odkazy v e-mailech (potvrzení účtu, reset hesla) vedou na produkční adresu, ne na vývojovou.
- [ ] Registrace, potvrzení e-mailu a reset hesla jsou vyzkoušené naostro, až po kliknutí na odkaz v doručeném e-mailu.
- [ ] Hláška při přihlášení a resetu hesla neprozrazuje, jestli účet existuje („Pokud účet existuje, poslali jsme e-mail").
- [ ] Odhlášení a změna hesla opravdu ukončí přihlášení, ne jen schovají tlačítko.
- [ ] Uživatel si nemůže sám přidělit vyšší oprávnění (třeba admina). Role se nebere z ničeho, co může uživatel změnit.

## Soubory

- [ ] Když uživatelé nahrávají soubory: soubory nejsou veřejně dostupné každému, kdo uhodne adresu, a kontroluje se jejich typ a velikost.

## Chyby

- [ ] Když něco selže, uživatel vidí srozumitelnou hlášku a ví, co dál. Ne bílou stránku ani technický výpis.
- [ ] Chyba se neschovává. Selhání při načítání dat se netváří jako prázdný seznam nebo „nejsi přihlášený". Agent chyby rád tiše spolkne.

## E-maily

- [ ] Když aplikace posílá e-maily: chodí z vlastní domény, s nastaveným ověřením odesílatele (SPF, DKIM), jinak končí ve spamu.
- [ ] Z vývoje nechodí e-maily skutečným lidem.
- [ ] Limity na počet odeslaných e-mailů a registrací jsou nastavené na reálný provoz. Výchozí limity služeb bývají nízké a registrace pak potichu přestanou fungovat.

## Platby

- [ ] Když aplikace přijímá platby: vývoj běží v testovacím režimu platební brány a testovací a ostré klíče jsou oddělené.
- [ ] Zaplaceno je, až když to potvrdí platební brána, ne když se uživatel vrátil na stránku „Děkujeme".
- [ ] Stejné potvrzení platby zpracované dvakrát nevytvoří dvě objednávky.

## Obsah

- [ ] Když texty mění někdo, kdo nepracuje s agentem: má na to jednoduchý nástroj a texty nejsou natvrdo v kódu.

## Zdroje

- [OWASP Top 10:2025](https://top10.owasp.org/2025)
- [vibe-coding-security](https://github.com/boxed-dev/vibe-coding-security)
