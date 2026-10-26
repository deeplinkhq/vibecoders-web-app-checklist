# Databáze

**Týká se:** projektu s databází. Příklady jsou pro Supabase, princip platí obecně.

## Kdo co vidí

- [ ] **DB-1** Každá tabulka má zapnutá pravidla přístupu (Row Level Security). Bez nich veřejný klíč z prohlížeče čte a zapisuje všechno. Zhruba 10 % aplikací z Lovable mělo v roce 2025 databázi bez pravidel (CVE-2025-48757).
- [ ] **DB-2** Ověřeno zvenku: `curl` na tabulku jen s veřejným (anon) klíčem a bez přihlášení nevrátí nic, co nemá vidět kdokoli.
- [ ] **DB-3** Přihlášený uživatel nevidí ani nezmění cizí záznamy. Ověř dvěma testovacími účty.
- [ ] **DB-4** Bezpečnostní kontrola databáze (Supabase Security Advisor) je bez varování.
- [ ] **DB-5** Klíč s plným přístupem (service role) je jen na serveru, nikdy v kódu pro prohlížeč.

## Data

- [ ] **DB-6** Pravidla pro data (povinná pole, unikátnost, vazby) jsou v databázi nebo na serveru, ne jen ve formuláři.
- [ ] **DB-7** Struktura databáze se mění přes migrace uložené v gitu, ne klikáním v produkčním dashboardu.
- [ ] **DB-8** Testovací data a účty z vývoje neskončily v produkci.
- [ ] **DB-9** Limity zvednuté kvůli testům (třeba počet registrací za hodinu) jsou před produkcí vrácené.

## Prostředí a zálohy

- [ ] **DB-10** Vývoj a produkce mají každá svou databázi. Supabase zdarma má dva aktivní projekty a po týdnu bez provozu je uspí (stav 10/2026).
- [ ] **DB-11** Produkční databáze se zálohuje. Na Supabase zdarma automatické zálohy nejsou, je potřeba `supabase db dump` nebo placený plán.
- [ ] **DB-12** Obnova ze zálohy je aspoň jednou vyzkoušená. Záloha bez vyzkoušené obnovy není záloha.
