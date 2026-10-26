# Provoz

**Týká se:** čehokoli, co má běžet déle než týden.

## Hlídání

- [ ] Je zapnuté hlídání dostupnosti (UptimeRobot a podobně, základ zdarma).
- [ ] Upozornění z hostingu (neúspěšné nasazení, doména), Search Console a hlídání dostupnosti chodí na e-mail, který někdo opravdu čte.
- [ ] Když jde o aplikaci: chyby na produkci zachytává nástroj na sledování chyb (Sentry a podobně) s upozorněním na e-mail. Ověřeno schválně vyvolanou chybou.
- [ ] Víš, jak dlouho hosting drží logy. Vercel Hobby drží runtime logy 1 hodinu, Pro 1 den (stav 8/2026), chybu nahlášenou druhý den v nich nenajdeš.
- [ ] Logy ani nástroj na chyby neukládají hesla, tokeny ani osobní údaje z formulářů.
- [ ] První týden po spuštění je ověřené, že chodí zprávy z formuláře. Tiché selhání doručování je nejčastější skrytá porucha.

## Peníze

- [ ] Hosting, databáze a placená API mají nastavený rozpočet nebo upozornění na útratu. Účet za zneužitou funkci přijde až na konci měsíce.

## Doména

- [ ] Doména má zapnuté automatické prodloužení a platební karta u registrátora je platná.

## Pravidelná údržba

- [ ] Jednou měsíčně 15 minut: formulář funguje, Search Console je bez chyb, doména neexpiruje, aktualizace závislostí jsou prošlé přes preview.
- [ ] Když projekt má databázi: zálohy běží a poslední je čerstvá.
- [ ] Když se data z analytiky dají číst agentem (třeba přes Google Analytics MCP, jen pro čtení): po pár týdnech provozu je nech projít a navrhnout úpravy.

## Když se něco pokazí

- [ ] Je sepsané, co dělat, když web spadne nebo unikne klíč: kdo to řeší, jak vrátit verzi, jak zrotovat klíče a jak dát vědět uživatelům.

## Předání

- [ ] README projektu říká, kde web běží, kde jsou účty (bez hesel), kam chodí formulář, kde jsou zálohy a jak vrátit předchozí verzi. Za půl roku to nebudeš vědět ani ty.
