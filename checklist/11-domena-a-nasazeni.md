# Doména a nasazení

**Týká se:** každého webu na vlastní doméně.

## Jak se nasazuje

- [ ] Změny nejdou přímo do `main`. Každá změna je větev a pull request, i když na projektu pracuješ sám. Preview adresa od hostingu je zkušebna.
- [ ] Víš, jak vrátit rozbitou produkci: rychlý návrat na předchozí verzi v hostingu (na Vercelu Instant Rollback), pak Revert pull requestu. Nikdy `git reset` a force push.
- [ ] Tarif hostingu odpovídá použití. Vercel Hobby je jen pro nekomerční provoz, web firmy patří na placený plán (stav 10/2026).

## Doména a DNS

- [ ] Je vybraná jedna varianta domény (s www, nebo bez) a druhá je 301 přesměrovaná.
- [ ] Hlavní doména míří přes záznam `A`, `www` přes `CNAME`. Hodnoty jsou opsané z dashboardu hostingu, ne z návodu na internetu.
- [ ] Certifikát se nekupuje, moderní hosting ho vystaví a obnovuje sám.
- [ ] Zkontrolovaný záznam `CAA`. Starý záznam pro jinou certifikační autoritu tiše zablokuje vystavení certifikátu.
- [ ] Při změně DNS je den předem snížené TTL na 300. Ověřeno nezávisle (dnschecker.org, `dig`) a z mobilních dat, ne jen z domácí wifi.

## E-mail na doméně

- [ ] Při přechodu na nameservery hostingu jsou ručně přenesené záznamy `MX`, `SPF` a `DKIM`. Tohle je nejčastější způsob, jak si při nasazení webu vypnout vlastní e-mail.
- [ ] Když se z domény odesílají e-maily: funguje SPF a DKIM, `DMARC` se přidává až po 48 hodinách bez problémů.

## Drobnosti, které chybí skoro vždycky

- [ ] Favicon ve třech souborech: `favicon.ico`, `favicon.svg` a `apple-touch-icon.png` (180x180 px, bez průhlednosti, jinak ji iOS podloží černou). Všechny jsou odkázané v `<head>` a ikona je čitelná i v 16 px.
- [ ] Vlastní stránka 404, která vypadá jako zbytek webu a má odkaz na hlavní stránku a hlavní akci.
- [ ] Neexistující adresa vrací stav 404, ne přesměrování na hlavní stránku.
- [ ] Fungují všechny čtyři varianty adresy (http, https, s www, bez www) a všechny končí na té jedné správné.
