# Doména a nasazení

**Týká se:** každého webu na vlastní doméně.

## Jak se nasazuje

- [ ] **NAS-1** Změny nejdou přímo do `main`. Každá změna je větev a pull request, i když na projektu pracuješ sám. Preview adresa od hostingu je zkušebna.
- [ ] **NAS-2** Víš, jak vrátit rozbitou produkci: rychlý návrat na předchozí verzi v hostingu (na Vercelu Instant Rollback), pak Revert pull requestu. Nikdy `git reset` a force push.
- [ ] **NAS-3** Tarif hostingu odpovídá použití. Vercel Hobby je jen pro nekomerční provoz, web firmy patří na placený plán (stav 10/2026).

## Doména a DNS

- [ ] **NAS-4** Je vybraná jedna varianta domény (s www, nebo bez) a druhá je 301 přesměrovaná.
- [ ] **NAS-5** Hlavní doména míří přes záznam `A`, `www` přes `CNAME`. Hodnoty jsou opsané z dashboardu hostingu, ne z návodu na internetu.
- [ ] **NAS-6** Certifikát se nekupuje, moderní hosting ho vystaví a obnovuje sám.
- [ ] **NAS-7** Zkontrolovaný záznam `CAA`. Starý záznam pro jinou certifikační autoritu tiše zablokuje vystavení certifikátu.
- [ ] **NAS-8** Při změně DNS je den předem snížené TTL na 300. Ověřeno nezávisle (dnschecker.org, `dig`) a z mobilních dat, ne jen z domácí wifi.

## E-mail na doméně

- [ ] **NAS-9** Při přechodu na nameservery hostingu jsou ručně přenesené záznamy `MX`, `SPF` a `DKIM`. Tohle je nejčastější způsob, jak si při nasazení webu vypnout vlastní e-mail.
- [ ] **NAS-10** Když se z domény odesílají e-maily: funguje SPF a DKIM, `DMARC` se přidává až po 48 hodinách bez problémů.

## Drobnosti, které chybí skoro vždycky

- [ ] **NAS-11** Favicon ve třech souborech: `favicon.ico`, `favicon.svg` a `apple-touch-icon.png` (180x180 px, bez průhlednosti, jinak ji iOS podloží černou). Všechny jsou odkázané v `<head>` a ikona je čitelná i v 16 px.
- [ ] **NAS-12** Vlastní stránka 404, která vypadá jako zbytek webu a má odkaz na hlavní stránku a hlavní akci.
- [ ] **NAS-13** Neexistující adresa vrací stav 404, ne přesměrování na hlavní stránku.
- [ ] **NAS-14** Fungují všechny čtyři varianty adresy (http, https, s www, bez www) a všechny končí na té jedné správné.
