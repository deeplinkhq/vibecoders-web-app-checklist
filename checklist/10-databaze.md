# Databáze

**Týká se:** projektu, který ukládá data.

## Kdo co vidí

- [ ] Ke každé tabulce je nastavené, kdo smí co číst a měnit. Bez toho se k datům dostane kdokoli, kdo má veřejný klíč ze stránky.
- [ ] Pravidla platí i pro tabulky, které agent přidal později. Nová tabulka bez pravidel je nejčastější díra.
- [ ] Ověřeno zvenku: bez přihlášení se nedá přečíst nic, co nemá vidět kdokoli.
- [ ] Ověřeno dvěma testovacími účty: jeden uživatel nevidí ani nezmění data druhého.
- [ ] Klíč s plným přístupem k databázi je jen na serveru.

## Data

- [ ] Pravidla pro data (povinná pole, jedinečnost) hlídá databáze nebo server, ne jen formulář.
- [ ] Testovací data a účty z vývoje neskončily v produkci.
- [ ] Agent nemá přístup k produkčním datům. V roce 2025 agent smazal produkční databázi, i když měl zákaz změn.

## Zálohy

- [ ] Produkční data se zálohují. U levných a bezplatných tarifů automatické zálohy často nejsou.
- [ ] Zálohují se i nahrané soubory, nejen databáze.
- [ ] Obnova ze zálohy je aspoň jednou vyzkoušená. Záloha bez vyzkoušené obnovy není záloha.

## Zdroje

- [UpGuard: Systemic Data Exposure in Supabase Apps](https://www.upguard.com/blog/everything-everywhere-systemic-data-exposure-in-supabase-apps) (10/2026): tisíce databází s daty čitelnými pro kohokoli.
- [Incident Replit](https://oecd.ai/en/incidents/2025-07-19-1eb1): agent smazal produkční databázi (7/2025).
