# Databáze

**Týká se:** projektu s databází. Příklady jsou pro Supabase, princip platí obecně.

## Kdo co vidí

- [ ] Každá tabulka má zapnutá pravidla přístupu (Row Level Security). Bez nich veřejný klíč z prohlížeče čte a zapisuje všechno. Zhruba 10 % aplikací z Lovable mělo v roce 2025 databázi bez pravidel (CVE-2025-48757).
- [ ] Každá tabulka, kterou agent vytvoří v SQL nebo migraci, má hned zapnuté RLS a pravidla. Automaticky se RLS zapíná jen u tabulek z Table Editoru. Podle UpGuard (10/2026) má přes 16 000 databází na Supabase tabulky čitelné pro kohokoli.
- [ ] Žádné pravidlo nepouští všechny (`using (true)`) k datům, která nejsou veřejná. Zapnuté RLS s takovým pravidlem je totéž co žádné.
- [ ] Pohledy (views) mají `security_invoker = true`. Jinak běží s právy vlastníka a RLS obcházejí.
- [ ] Ověřeno zvenku: `curl` na tabulku jen s veřejným (anon) klíčem a bez přihlášení nevrátí nic, co nemá vidět kdokoli.
- [ ] Přihlášený uživatel nevidí ani nezmění cizí záznamy. Ověř dvěma testovacími účty.
- [ ] Bezpečnostní kontrola databáze (Supabase Security Advisor) je bez varování.
- [ ] Klíč s plným přístupem (service role) je jen na serveru, nikdy v kódu pro prohlížeč.
- [ ] Od 30. 10. 2026 má nová tabulka v Supabase v migraci i explicitní `GRANT`, jinak ji aplikace přes Data API nevidí. Když agent hlásí chybu oprávnění, řešením je grant, ne vypnutí RLS.

## Data

- [ ] Pravidla pro data (povinná pole, unikátnost, vazby) jsou v databázi nebo na serveru, ne jen ve formuláři.
- [ ] Struktura databáze se mění přes migrace uložené v gitu, ne klikáním v produkčním dashboardu.
- [ ] Agent nemá zápis do produkční databáze ani právo měnit její strukturu. Změny jdou jen přes migrace a nasazení. V roce 2025 agent v Replitu během zákazu změn smazal produkční databázi.
- [ ] Nejčastější dotazy mají index a Performance Advisor je bez varování. Agent indexy skoro nepřidává a aplikace zpomalí, až přibudou data.
- [ ] Testovací data a účty z vývoje neskončily v produkci.
- [ ] Limity zvednuté kvůli testům (třeba počet registrací za hodinu) jsou před produkcí vrácené.

## Prostředí a zálohy

- [ ] Vývoj a produkce mají každá svou databázi. Supabase zdarma má dva aktivní projekty a po týdnu bez provozu je uspí (stav 10/2026).
- [ ] Produkční databáze se zálohuje. Na Supabase zdarma automatické zálohy nejsou, je potřeba `supabase db dump` nebo placený plán.
- [ ] Nahrané soubory se zálohují zvlášť. Záloha databáze v Supabase obsahuje jen záznamy o souborech, ne soubory samotné.
- [ ] Obnova ze zálohy je aspoň jednou vyzkoušená. Záloha bez vyzkoušené obnovy není záloha.
