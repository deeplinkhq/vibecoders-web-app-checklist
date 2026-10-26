# Bezpečnost

**Týká se:** každého webu. Část „Aplikace" jen projektů s backendem, přihlášením nebo databází.

Agent dělá dobře známé vzory (SQL injection skoro nevyrábí), ale selhává tam, kde bezpečnost závisí na kontextu. Co není v zadání, to neudělá.

## Klíče a tajemství

- [ ] V kódu, který běží v prohlížeči, není žádný API klíč, token ani adresa webhooku. Co je v HTML nebo JavaScriptu, je veřejné, zamaskování v proměnné nebo v base64 nic neřeší. Hledej třeba `sk-`, `eyJ`, `hooks.slack`, `discord.com/api/webhooks`.
- [ ] `.env` je v `.gitignore` od prvního commitu. Ověř `git log --all -- .env`, historie gitu si pamatuje i smazané soubory.
- [ ] Klíče jsou v proměnných prostředí hostingu, zvlášť pro vývoj a produkci.
- [ ] Žádné tajemství nemá prefix `NEXT_PUBLIC_` (ve Vite `VITE_`). Takovou proměnnou build vloží do kódu pro prohlížeč a agent prefix rád přidá, když opravuje chybu „undefined".
- [ ] Když chybí proměnná s tajemstvím, aplikace spadne, místo aby použila výchozí hodnotu. Agent rád doplní výchozí JWT secret, se kterým jde podvrhnout přihlášení.
- [ ] Klíče mají jen oprávnění, která aplikace potřebuje (klíč k mapám omezený na doménu, klíč k e-mailům jen na odesílání).
- [ ] Když klíč někdy unikl (do repa, do HTML, do chatu): je zrotovaný. Smazání commitu nic neřeší, boti veřejná repa prohledávají v řádu minut. Pořadí je nejdřív rotovat, pak čistit historii.

## Závislosti

- [ ] Každý balíček existuje a je ten správný. Zhruba 20 % balíčků, které AI navrhne, neexistuje, a útočníci si tyhle názvy registrují. Ověř `npm view <balíček>`, datum vzniku a počet verzí.
- [ ] Skripty z CDN mají pevnou verzi a atribut `integrity`. Každý odkaz na CDN otevři, jestli vede tam, kam má.
- [ ] Lockfile (`package-lock.json` a podobně) je v gitu. Bez něj se na hostingu můžou nainstalovat jiné verze balíčků než u tebe.
- [ ] Když projekt má závislosti: je zapnutý Dependabot (nebo podobný nástroj) a jeho pull requesty se procházejí přes preview.

## Bezpečnostní hlavičky

- [ ] Web posílá `X-Content-Type-Options: nosniff`, `Referrer-Policy: strict-origin-when-cross-origin` a `Permissions-Policy`. Hosting je sám neposílá (Vercel jen HSTS), nastavují se v jeho konfiguraci, třeba `headers` ve `vercel.json`.
- [ ] Web zakazuje vložení do cizího rámu přes `frame-ancestors 'none'` v CSP (nebo `X-Frame-Options: SAMEORIGIN`).
- [ ] Content-Security-Policy je nasazená nejdřív v režimu `Report-Only`. Musí povolit `frame-src` pro každý vložený obsah, jinak si ho zablokuješ a chybu uvidíš jen v konzoli.
- [ ] Nepřidává se `X-XSS-Protection`, je zastaralá.
- [ ] Ověřeno na securityheaders.com, cíl je známka A.

## Účty

- [ ] Na GitHubu, hostingu, u registrátora domény a u databáze je zapnuté dvoufázové ověření.
- [ ] Účty jsou na jméno vlastníka webu, ne dodavatele.

## Aplikace

- [ ] Data se ověřují na serveru, ne jen v prohlížeči. Kontrola ve formuláři je pro pohodlí uživatele, ne pro bezpečnost.
- [ ] Přihlášení, registrace a veřejné endpointy mají limit počtu pokusů.
- [ ] Registrace má ochranu proti botům (Cloudflare Turnstile a podobně).
- [ ] Když přihlášení stojí na cookies: formuláře mají ochranu proti CSRF. Frameworky ji často mají vestavěnou, ověř, že je zapnutá. Webhooky platebních bran z ní musí být vyjmuté.
- [ ] Přihlášený uživatel se nedostane k cizím datům změnou ID v adrese nebo v požadavku. Zkus to ručně. Pravidla v databázi jsou v [Databázi](10-databaze.md).
- [ ] Chybové stránky a odpovědi API na produkci neukazují stack trace, cesty k souborům ani názvy tabulek. Ověř tak, že pošleš nesmyslný požadavek.
- [ ] Na produkci nejsou dostupné testovací a ladicí stránky ani endpointy (`/test`, `/debug`, `/api/seed`). Agent je rád vytvoří „na chvíli" a zapomene.
- [ ] Než jde změna do produkce, prošel ji druhý pár očí: člověk, nebo aspoň AI review pull requestu.
