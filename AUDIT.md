# Jak projít projekt podle checklistu

Instrukce pro agenta, který kontroluje cizí projekt. Uživatel tě sem poslal, abys jeho web nebo aplikaci prošel podle souborů ve složce `checklist/`.

## 1. Zjisti, co je to za projekt

Než otevřeš první kategorii, projdi projekt (soubory, konfiguraci, nasazenou adresu, pokud existuje) a urči:

- **Typ:** statický web, web s formulářem, aplikace s přihlášením, aplikace s platbami.
- **Stack a hosting.**
- **Jestli už běží** a na jaké adrese.
- **Kdo to bude používat:** jen autor, pár lidí, nebo cizí lidé.
- **Jestli jsou v projektu osobní data cizích lidí nebo peníze.**
- **Jak dlouho to má žít** a co se stane, když to spadne nebo se ztratí data.
- **Úroveň projektu** podle tabulky níž.

| Úroveň | Co to je | Když se to pokazí |
| --- | --- | --- |
| `web` | prezentační web, landing page, blog, případně kontaktní formulář nebo vložená rezervace. Bez uživatelských účtů. | nefunguje web nebo formulář |
| `malá` | aplikace s přihlášením nebo daty pro známé uživatele: autor, rodina, firma, desítky lidí. Bez plateb od cizích lidí. | výpadek na pár hodin nevadí, data se obnoví ze zálohy |
| `veřejná` | registrují se cizí lidé, aplikace drží jejich osobní data nebo přijímá platby | únik dat, ztráta peněz, právní problém |
| `velká` | mnoho uživatelů nebo tým, časté vydávání, výpadek stojí peníze nebo zákazníky | ztráta tržeb a zákazníků |

Co z projektu nezjistíš, se zeptej. Všechno najednou v jedné zprávě, ne po jedné otázce. Úroveň napiš uživateli na začátek reportu, ať ji může opravit.

## 2. Vyber kategorie

Každý soubor v `checklist/` má nahoře řádek **Týká se**. Kategorie, které se projektu netýkají, přeskoč a v reportu je vyjmenuj jedním řádkem.

## 3. Projdi položky

Každá položka má na začátku úroveň, od které platí (`[web]`, `[malá]`, `[veřejná]`, `[velká]`). Položky nad úrovní projektu přeskoč a nevypisuj, v reportu uveď jen jejich počet. Položka, která po úrovni začíná „Když…", platí jen za dané podmínky. Jak položku zkontrolovat, říká poznámka *Ověření:* na jejím konci. Co jde, ověř sám (příkaz, API, kód). Položky s *Ověření (prohlížeč):* ověř, když umíš ovládat prohlížeč, jinak je dej do „Ověř ručně". Položky s *Ověření (člověk):* dej rovnou do „Ověř ručně".

U každé položky urči stav:

- **OK:** splněno a máš důkaz (soubor a řádek, výstup příkazu).
- **Chybí:** nesplněno.
- **Ověř ručně:** z projektu se to zjistit nedá (účet u registrátora, Google Business Profile, nastavení v dashboardu). Napiš, kde a jak to člověk ověří.
- **Nerelevantní:** jednou větou proč.
- **Otázka:** nevíš, jestli to uživatel chce řešit (analytika, newsletter, dark mode, platby). Nedávej to do „Chybí", zeptej se.

Ověřuj, neodhaduj. Když web běží, použij `curl` nebo prohlížeč. Kontrast spočítej, ne odhadni. Čísla v položkách (velikosti, limity) ber jako vodítko, ne jako zákon.

## 4. Report

1. **Shrnutí:** typ projektu, prošlé a přeskočené kategorie, počet nálezů.
2. **Nálezy** v tabulce `kategorie | co chybí | kde | návrh opravy`, seřazené podle dopadu:
   1. bezpečnost a únik dat (klíče v kódu, databáze bez pravidel přístupu),
   2. věci, které web tiše rozbíjejí (`noindex`, nefunkční formulář, chybějící zálohy),
   3. právo (cookie lišta, zásady zpracování),
   4. zbytek.
3. **Otázky** na uživatele.
4. **Ověř ručně:** seznam věcí ke kontrole mimo projekt.

Položky ve stavu OK nevypisuj jednotlivě, stačí jejich počet.

## 5. Opravy

Nic neopravuj, dokud o to uživatel výslovně nepožádá. Pak opravuj po kategoriích, ne všechno naráz, a po každém kole kontrolu zopakuj. Běžně se opraví tři nálezy a čtvrtý se přehlédne.
