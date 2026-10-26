# Bezpečnost

**Týká se:** každého webu. Část „Aplikace" jen projektů s přihlášením nebo databází.

Agent dělá dobře známé vzory, ale selhává tam, kde bezpečnost závisí na kontextu. Co není v zadání, to neudělá.

## Klíče a hesla

- [ ] V kódu, který běží v prohlížeči, není žádný klíč, token ani heslo. Co je v kódu stránky, je veřejné, a zamaskování nic neřeší.
- [ ] Klíče nejsou v repozitáři ani v jeho historii. Git si pamatuje i smazané soubory.
- [ ] Klíče pro vývoj a pro produkci jsou různé a každý má jen oprávnění, která potřebuje.
- [ ] Když chybí nastavení s tajným klíčem, aplikace spadne, místo aby použila výchozí hodnotu. Agent rád doplní výchozí klíč, se kterým pak jde podvrhnout přihlášení.
- [ ] Když klíč někdy unikl (do repa, do kódu stránky, do chatu): je vyměněný. Smazání nestačí, boti veřejná repa prohledávají v řádu minut.

## Knihovny

- [ ] Každá knihovna, kterou agent přidal, existuje a je ta správná. Zhruba 20 % balíčků, které AI navrhne, neexistuje, a útočníci si tyhle názvy registrují.
- [ ] Verze knihoven jsou zamčené a aktualizace se pravidelně procházejí.

## Hlavičky a chybové stránky

- [ ] Web posílá základní bezpečnostní hlavičky a nejde vložit do cizího webu v rámu. Ověřit jde online testem bezpečnostních hlaviček.
- [ ] Chybové stránky na produkci neukazují technické výpisy, cesty k souborům ani názvy tabulek.
- [ ] Na produkci nejsou dostupné testovací a ladicí stránky. Agent je rád vytvoří „na chvíli" a zapomene.

## Účty

- [ ] Všechny účty kolem webu (repozitář, hosting, doména, databáze) mají dvoufázové ověření.
- [ ] Účty jsou na jméno vlastníka webu, ne dodavatele.

## Aplikace

- [ ] Data se kontrolují na serveru, ne jen v prohlížeči. Kontrola ve formuláři je pro pohodlí uživatele, ne pro bezpečnost.
- [ ] Přihlášení, registrace a další veřejné akce mají limit počtu pokusů a registrace ochranu proti botům.
- [ ] Přihlášený uživatel se nedostane k cizím datům tím, že v adrese nebo požadavku změní číslo záznamu. Zkus to ručně.
- [ ] Než jde změna do produkce, prošel ji druhý pár očí: člověk, nebo aspoň AI review.
