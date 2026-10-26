# Bezpečnost

**Týká se:** každého webu. Část „Aplikace" jen projektů s backendem, přihlášením nebo databází.

Agent dělá dobře známé vzory (SQL injection skoro nevyrábí), ale selhává tam, kde bezpečnost závisí na kontextu. Co není v zadání, to neudělá.

## Klíče a tajemství

- [ ] **BEZ-1** V kódu, který běží v prohlížeči, není žádný API klíč, token ani adresa webhooku. Co je v HTML nebo JavaScriptu, je veřejné, zamaskování v proměnné nebo v base64 nic neřeší. Hledej třeba `sk-`, `eyJ`, `hooks.slack`, `discord.com/api/webhooks`.
- [ ] **BEZ-2** `.env` je v `.gitignore` od prvního commitu. Ověř `git log --all -- .env`, historie gitu si pamatuje i smazané soubory.
- [ ] **BEZ-3** Klíče jsou v proměnných prostředí hostingu, zvlášť pro vývoj a produkci.
- [ ] **BEZ-4** Klíče mají jen oprávnění, která aplikace potřebuje (klíč k mapám omezený na doménu, klíč k e-mailům jen na odesílání).
- [ ] **BEZ-5** Když klíč někdy unikl (do repa, do HTML, do chatu): je zrotovaný. Smazání commitu nic neřeší, boti veřejná repa prohledávají v řádu minut. Pořadí je nejdřív rotovat, pak čistit historii.

## Závislosti

- [ ] **BEZ-6** Každý balíček existuje a je ten správný. Zhruba 20 % ukázek kódu od AI odkazuje na neexistující balíček a útočníci si tyhle názvy registrují. Ověř `npm view <balíček>`, datum vzniku a počet verzí.
- [ ] **BEZ-7** Skripty z CDN mají pevnou verzi a atribut `integrity`. Každý odkaz na CDN otevři, jestli vede tam, kam má.
- [ ] **BEZ-8** Když projekt má závislosti: je zapnutý Dependabot (nebo podobný nástroj) a jeho pull requesty se procházejí přes preview.

## Bezpečnostní hlavičky

- [ ] **BEZ-9** Web posílá `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin` a `Permissions-Policy`. Hosting je sám neposílá (Vercel jen HSTS), nastavují se v jeho konfiguraci, třeba `headers` ve `vercel.json`.
- [ ] **BEZ-10** Web zakazuje vložení do cizího rámu přes `frame-ancestors 'none'` v CSP (nebo `X-Frame-Options: SAMEORIGIN`).
- [ ] **BEZ-11** Content-Security-Policy je nasazená nejdřív v režimu `Report-Only`. Musí povolit `frame-src` pro každý vložený obsah, jinak si ho zablokuješ a chybu uvidíš jen v konzoli.
- [ ] **BEZ-12** Nepřidává se `X-XSS-Protection`, je zastaralá.
- [ ] **BEZ-13** Ověřeno na securityheaders.com, cíl je známka A.

## Účty

- [ ] **BEZ-14** Na GitHubu, hostingu, u registrátora domény a u databáze je zapnuté dvoufázové ověření.
- [ ] **BEZ-15** Účty jsou na jméno vlastníka webu, ne dodavatele.

## Aplikace

- [ ] **BEZ-16** Data se ověřují na serveru, ne jen v prohlížeči. Kontrola ve formuláři je pro pohodlí uživatele, ne pro bezpečnost.
- [ ] **BEZ-17** Přihlášení, registrace a veřejné endpointy mají limit počtu pokusů.
- [ ] **BEZ-18** Registrace má ochranu proti botům (Cloudflare Turnstile a podobně).
- [ ] **BEZ-19** Formuláře za přihlášením mají ochranu proti CSRF. Frameworky ji často mají vestavěnou, ověř, že je zapnutá. V testu z roku 2025 ji neměla ani jedna z 15 aplikací od pěti agentů.
- [ ] **BEZ-20** Přihlášený uživatel se nedostane k cizím datům změnou ID v adrese nebo v požadavku. Zkus to ručně. Pravidla v databázi jsou v [Databázi](10-databaze.md).
- [ ] **BEZ-21** Než jde změna do produkce, prošel ji druhý pár očí: člověk, nebo aspoň AI review pull requestu.
