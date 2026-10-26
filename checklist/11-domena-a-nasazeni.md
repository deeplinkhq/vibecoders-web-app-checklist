# Doména a nasazení

**Týká se:** každého nasazovaného webu nebo aplikace. Části o vlastní doméně, DNS a e-mailu použij podle skutečného zapojení projektu.

U kontrol nasazení a rollbacku vycházej z konfigurace, historie běhů a záznamů předchozích zkoušek. Chybějící důkaz označ „Ověř ručně“. Samotný audit není pokyn k nasazení, přepnutí DNS ani provedení rollbacku.

## Oddělená prostředí

- [ ] Vývoj a test jsou oddělené od produkce. U aplikace mají oddělené prostředky a přístupová oprávnění, aby chyba při testování nezasáhla ostrý provoz. [Zdroj](https://pages.nist.gov/nccoe-devsecops/appendix-c.html) *Ověření:* z konfigurace sestav přehled prostředí a jejich připojených prostředků; porovnej adresy databází, úložišť, front a oprávnění použitých identit. Tajné hodnoty nevypisuj do reportu.

- [ ] Když aplikace pracuje s neveřejnými daty: testovací dataset obsahuje syntetická nebo anonymizovaná data. Kopie ostré databáze se skutečnými osobními údaji není bezpečný výchozí dataset pro testování. [Zdroj](https://github.com/OWASP/www-project-devsecops-verification-standard/blob/main/document/TEST-001-Security-Test-Management.md) *Ověření:* přečti generátory testovacích dat, importní skripty a postup přípravy datasetu; bez přístupu k datům nebo důkazu anonymizace označ „Ověř ručně“.

- [ ] Když testovaná funkce provádí vnější akci: testovací prostředí používá testovací režim nebo zachycení této akce. Test nemá účtovat skutečnou platbu, obeslat zákazníky ani spustit ostrou integraci. [Zdroj](https://sre.google/workbook/canarying-releases/) *Ověření:* zkontroluj konfiguraci příslušných integrací a záznam testu; ověř testovací endpoint, účet nebo omezení příjemců podle typu akce.

- [ ] Když zkušební nasazení obsahuje neveřejný obsah nebo funkce: přístup vyžaduje autentizaci nebo síťové omezení. Neodhadnutelná URL ani `noindex` nenahrazují řízení přístupu. [Zdroj](https://api-security.owasp.org/editions/2019/en/0xa9-improper-assets-management/) *Ověření:* bez přihlášení požádej přes `curl` o chráněnou stránku a přímo o její API nebo soubor; ověř, že se chráněný obsah nevrátí.

- [ ] Když aplikace závisí na runtime nebo podpůrných službách: zkušební prostředí používá jejich stejné typy a kompatibilní verze jako produkce. Podstatné rozdíly jsou popsané, aby bylo jasné, co zkušební nasazení neověřuje. [Zdroj](https://12factor.net/dev-prod-parity) *Ověření:* porovnej deklarované i skutečně nasazené verze a konfiguraci prostředí; zaznamenej rozdíly ovlivňující chování.

## Konfigurace

- [ ] Když se konfigurace liší mezi prostředími: je oddělená od zdrojového kódu a předává se při sestavení nebo spuštění. Pro běžné hodnoty použij proměnné prostředí; tajné hodnoty může dodat také správce tajných údajů. [Zdroje](https://12factor.net/config), [správa tajných údajů](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html). *Ověření:* najdi načítání konfigurace a porovnej ho s nasazovací konfigurací; hledej natvrdo vložené adresy služeb, identifikátory prostředí a přístupové údaje.

- [ ] Když aplikace vyžaduje konfiguraci: chybějící nebo neplatná povinná hodnota zastaví sestavení nebo spuštění s konkrétní chybou. Výchozí hodnota nesmí potichu připojit jiné prostředí nebo zapnout nebezpečný režim. [Zdroj](https://pages.nist.gov/nccoe-devsecops/mapping-ssdf.html) *Ověření:* přečti schéma a validaci konfigurace včetně výchozích hodnot; hledej pokrytí chybějících hodnot v testech a výstupech CI.

- [ ] Když aplikace sestavuje veřejné adresy: produkční konfigurace používá skutečnou veřejnou HTTPS adresu. Odkazy v e-mailech a návratové adresy nesmějí vést na `localhost` nebo zkušební nasazení. [Zdroj](https://12factor.net/config) *Ověření:* porovnej konfiguraci veřejné adresy s generátory URL a výsledným artefaktem; u hodnot vložených při sestavení kontroluj také výstup sestavení.

## CI a zkušební nasazení

- [ ] Změna určená k nasazení projde automatickou přípravou nasazovatelného výstupu v čistém prostředí. Postup nesmí záviset na necommitnutých souborech nebo balíčcích přítomných jen na počítači autora. [Zdroj](https://sre.google/workbook/canarying-releases/) *Ověření:* přečti konfiguraci CI a log posledního běhu; ověř čistý checkout, deklarované závislosti a příkaz sestavení nebo přípravy statického webu.

- [ ] Produkční nasazení je zablokované při neúspěchu povinných automatických kontrol. Povinné kontroly odpovídají projektu, například sestavení, kontrola typů, validace nebo testy. [Zdroj](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) *Ověření:* zkontroluj návaznosti úloh, podmínky nasazení a nastavení povinných kontrol; hledej ignorování návratového kódu a povolené pokračování po chybě.

- [ ] Produkční nasazení lze spustit jen z určeného důvěryhodného zdroje změn. Cizí příspěvek ani libovolná větev nemají automaticky získat možnost nasazovat do produkce. [Zdroj](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) *Ověření:* přečti spouštěče pipeline, omezení produkčního prostředí a oprávnění nasazovací identity; nastavení mimo repozitář ověř přes dostupné API, jinak označ „Ověř ručně“.

- [ ] Kandidát na produkční nasazení má předem ověřené zkušební nasazení. Záznam ověření patří ke konkrétní verzi, která se má nasadit. [Zdroje](https://12factor.net/dev-prod-parity), [ověřování nasazení](https://sre.google/workbook/canarying-releases/). *Ověření:* spoj identifikátor commitu nebo artefaktu se zkušební URL a výsledky kontrol podle kategorie „Testování a spuštění“.

- [ ] Nasazený release je dohledatelný ke zdrojové verzi, artefaktu a použité konfiguraci. Změna artefaktu nebo konfigurace vytváří nový identifikovatelný release. [Zdroj](https://12factor.net/build-release-run) *Ověření:* porovnej záznam nasazení, identifikátor commitu, identifikátor nebo hash artefaktu a revizi konfigurace; do reportu nezapisuj obsah tajných hodnot.

- [ ] Produkce dostává artefakt, který prošel povinnými kontrolami. Když se kvůli produkční konfiguraci sestavuje znovu, kontroly se vztahují i na tento výsledný artefakt. [Zdroj](https://dsomm.owasp.org/mapping) *Ověření:* sleduj předání artefaktu mezi úlohami a porovnej jeho identifikátor nebo hash; u nového sestavení dohledávej výsledky kontrol tohoto sestavení.

## Vrácení předchozí verze

- [ ] Předchozí funkční release lze obnovit popsaným a vyzkoušeným postupem. Postup počítá také s konfigurací potřebnou pro jeho běh. [Zdroj](https://12factor.net/build-release-run) *Ověření:* dohledávej uchovaný release, postup návratu a záznam úspěšné zkoušky ve zkušebním prostředí; samotné tlačítko „rollback“ není důkaz proveditelnosti.

- [ ] Když nasazení mění databázi nebo formát uložených dat: plán návratu řeší kompatibilitu předchozí verze s novými daty. Vrácení kódu samo nevrátí databázové změny ani provedené vnější akce. [Zdroj](https://aws.amazon.com/builders-library/ensuring-rollback-safety-during-deployments/) *Ověření:* porovnej migrace a čtení i zápis dat ve staré a nové verzi; dohledávej zkoušku návratu nebo doložený postup nápravy podle kategorie „Databáze“.

## Doména a DNS

- [ ] Když web používá vlastní doménu: její delegace a webové DNS záznamy vedou na aktuální nasazení. Odpověď z jednoho lokálního resolveru sama nestačí. [Zdroj](https://www.rfc-editor.org/info/rfc1034/) *Ověření:* použij `dig +trace`, dotazy na autoritativní servery a nezávislé rekurzivní resolvery; zkontroluj relevantní `NS`, `A`, `AAAA` a `CNAME` podle skutečného zapojení.

- [ ] Když doména publikuje `AAAA`: web je dosažitelný také přes IPv6. Zapomenutý záznam může část návštěvníků posílat na starý nebo nefunkční server. [Zdroj](https://developers.google.com/search/docs/crawling-indexing/site-move-no-url-changes) *Ověření:* porovnej odpovědi přes `curl -4` a `curl -6`; bez IPv6 konektivity auditního prostředí označ ověření IPv6 jako „Ověř ručně“.

- [ ] Když web používá vlastní doménu: varianty HTTP/HTTPS a s `www`/bez `www` končí na jedné zvolené HTTPS variantě. Alternativy používají serverové přesměrování `301` nebo `308`, zachovávají cestu a relevantní parametry a netvoří smyčku. [Zdroj](https://developers.google.com/search/docs/crawling-indexing/301-redirects) *Ověření:* pro všechny čtyři varianty proveď GET přes `curl` s výpisem hlaviček a sledováním přesměrování; zkus úvodní i existující vnořenou URL s parametrem.

- [ ] Když se mění provozovatel autoritativního DNS: nová zóna zachovává všechny potřebné záznamy původní zóny. Přenos zahrnuje také e-mailové záznamy, subdomény a ověřovací záznamy služeb. [Zdroje](https://www.rfc-editor.org/info/rfc1034/), [DKIM](https://www.rfc-editor.org/info/rfc6376/). *Ověření:* porovnej export nebo inventář staré a nové zóny; zvlášť zkontroluj `MX`, SPF, všechny používané DKIM selektory a DMARC. Úplnost zóny nelze doložit jediným dotazem `ANY`.

- [ ] Když se web přesouvá změnou DNS: přechod počítá s dosavadními TTL a souběhem starého a nového cíle. Snížení TTL těsně před přepnutím nezkrátí platnost odpovědí, které už jsou v cache. [Zdroje](https://www.rfc-editor.org/info/rfc1034/), [přesun hostingu](https://developers.google.com/search/docs/crawling-indexing/site-move-no-url-changes). *Ověření:* porovnej původní TTL, čas jeho změny, čas přepnutí a plán vypnutí starého cíle; po přepnutí zkontroluj odpovědi autoritativních i nezávislých rekurzivních serverů.

- [ ] Když doména používá DNSSEC: ověření řetězce důvěry prochází i po změně DNS. Nesoulad mezi rodičovským `DS` a podepisováním nové zóny může doménu znepřístupnit validujícím resolverům. [Zdroj](https://www.rfc-editor.org/rfc/rfc4035.html) *Ověření:* spusť DNSViz a zkontroluj delegaci, `DS`, `DNSKEY` a podpisy; samotná přítomnost těchto záznamů není důkaz úspěšné validace.

## HTTPS

- [ ] Každý veřejně používaný HTTPS hostname má platný a důvěryhodný certifikát pro své jméno. Platí to také pro hostname, který pouze přesměrovává jinam, protože TLS spojení předchází HTTP přesměrování. [Zdroj](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html) *Ověření:* proveď požadavky přes `curl` bez vypnutí kontroly certifikátu; pomocí OpenSSL ověř jména, dobu platnosti a řetězec certifikátu.

- [ ] Obnova certifikátu je automatizovaná a má doložený funkční mechanismus. Aktuálně platný certifikát nedokazuje, že se obnoví i příště. [Zdroj](https://letsencrypt.org/docs/integration-guide/) *Ověření:* zkontroluj konfiguraci spravované obnovy nebo plánovaného klienta a záznam úspěšné obnovy či podporované zkoušky; bez přístupu k nastavení označ „Ověř ručně“.

- [ ] HTTPS stránky nenačítají prostředky přes nezabezpečené HTTP. Mixed content může být zablokovaný nebo znehodnotit ochranu stránky. [Zdroj](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html) *Ověření (prohlížeč):* projdi hlavní typy stránek a sleduj síťové požadavky i konzoli; zahrň dynamicky načítané obrázky, skripty, styly, vložený obsah a API požadavky.

## E-mailové DNS záznamy

- [ ] Když doména autorizuje odesílání pomocí SPF: má právě jeden použitelný SPF záznam a jeho vyhodnocení nepřekračuje limit 10 mechanismů a modifikátorů vyžadujících DNS dotazy. Limit zahrnuje také vnořené vyhodnocení; nejde o prosté spočítání TXT záznamů. [Zdroj](https://www.rfc-editor.org/rfc/rfc7208.html#section-4.6.4) *Ověření:* načti TXT záznamy příslušné odesílací domény a použij SPF validátor; ověř také vnořené `include` a `redirect`.

- [ ] Když se e-maily podepisují DKIM: DNS obsahuje veřejné klíče pro skutečně používané selektory. Záznam pro jiný selektor nepomůže ověřit odeslanou zprávu. [Zdroj](https://www.rfc-editor.org/info/rfc6376/) *Ověření:* z dostupné zprávy přečti `s=` a `d=` v `DKIM-Signature` a dohledávej odpovídající záznam na `<selektor>._domainkey.<doména>` včetně případného CNAME.

- [ ] Když se z domény odesílají e-maily: má platnou DMARC politiku a nastavený příjem agregovaných reportů. Volba přísnější politiky vychází z ověření legitimních odesílatelů, ne z univerzálního požadavku na `p=reject` (stav 10/2026). [Zdroj](https://www.rfc-editor.org/rfc/rfc9989.html) *Ověření:* ověř příslušný DMARC záznam, syntaxi a `rua`; při externím příjemci ověř i jeho autorizaci.

- [ ] Když se z domény odesílají e-maily: zpráva z každého legitimního odesílacího systému projde DMARC. Úspěch vyžaduje alespoň jeden úspěšný a s doménou ve `From` zarovnaný mechanismus SPF nebo DKIM. [Zdroj](https://www.rfc-editor.org/rfc/rfc9989.html#section-4.4) *Ověření:* analyzuj dostupné zprávy a výsledky důvěryhodného přijímajícího serveru v `Authentication-Results`; bez těchto důkazů označ „Ověř ručně“.

## Směrování a stránka 404

- [ ] Když web má vnořené veřejné adresy: funguje jejich přímé otevření i obnovení stránky. Funkční proklik z úvodu neověřuje správné směrování nasazeného webu. [Zdroj](https://developers.google.com/search/docs/crawling-indexing/javascript/fix-search-javascript) *Ověření (prohlížeč):* otevři existující vnořenou URL přímo v nové relaci a obnov ji; ověř načtení správného obsahu i prostředků.

- [ ] Neexistující veřejná URL bez odpovídající náhrady vrací HTTP `404`. U záměrně trvale odstraněného obsahu je přípustné `410`; chybová stránka s `200` ani plošné přesměrování na úvod nejsou náhradou. [Zdroje](https://www.rfc-editor.org/rfc/rfc9110.html#section-15.5.5), [Google](https://support.google.com/webmasters/answer/2445990?hl=en). *Ověření:* proveď GET na náhodnou neexistující cestu a u dynamického obsahu také na neexistující identifikátor; zkontroluj skutečný HTTP status i tělo odpovědi.

- [ ] Stránka 404 srozumitelně říká, že požadovaný obsah nebyl nalezen, a nabízí funkční cestu zpět na web. [Zdroj](https://support.google.com/webmasters/answer/2445990?hl=en) *Ověření (prohlížeč):* otevři neexistující URL, zkontroluj zobrazení chybové stránky a použij nabízený odkaz na úvod nebo jinou existující část webu.

## Favicon a ikona na ploše

- [ ] Web deklaruje vlastní favicon a odkaz vede na platný obrázek. Vrácené HTML s kódem `200` není platná ikona. [Zdroj](https://html.spec.whatwg.org/multipage/links.html#rel-icon) *Ověření:* přečti `<link rel="icon">`, stáhni cílový soubor a ověř jeho skutečný formát i shodu deklarovaných rozměrů s obrázkem.

- [ ] Když projekt podporuje přidání na plochu telefonu: má vlastní dostupnou ikonu pro cílovou platformu. Pro iOS zkontroluj `apple-touch-icon`, u instalované webové aplikace také ikony v manifestu. [Zdroje](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html), [manifest](https://www.w3.org/TR/appmanifest/). *Ověření:* načti příslušné deklarace, stáhni ikony a ověř formát, rozměry a případné `purpose`; výsledný vzhled na zařízení ověř podle kategorie „Testování a spuštění“.

## Zdroje

Zdroje ověřené k 26. 10. 2026. Provozní doporučení jsou převedená na kontrolní položky; nejsou všechna normativním požadavkem standardu.

- [NIST SSDF: PO.5, oddělení a ochrana prostředí](https://pages.nist.gov/nccoe-devsecops/appendix-c.html).
- [NIST SSDF: mapování kontrol sestavení, testování a bezpečné konfigurace](https://pages.nist.gov/nccoe-devsecops/mapping-ssdf.html).
- [OWASP: Security Test Management](https://github.com/OWASP/www-project-devsecops-verification-standard/blob/main/document/TEST-001-Security-Test-Management.md), testovací prostředí a necitlivá data.
- [OWASP API Security: Improper Assets Management](https://api-security.owasp.org/editions/2019/en/0xa9-improper-assets-management/), přístup k neprodukčním prostředím.
- [The Twelve-Factor App: Config](https://12factor.net/config).
- [The Twelve-Factor App: Dev/prod parity](https://12factor.net/dev-prod-parity).
- [The Twelve-Factor App: Build, release, run](https://12factor.net/build-release-run).
- [OWASP: Secrets Management](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).
- [OWASP: CI/CD Security](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html).
- [OWASP DSOMM: mapování praktik](https://dsomm.owasp.org/mapping), zejména stejný artefakt mezi prostředími.
- [Google SRE: Canarying Releases](https://sre.google/workbook/canarying-releases/), automatizace sestavení, testů a nasazení.
- [Amazon Builders’ Library: Ensuring rollback safety during deployments](https://aws.amazon.com/builders-library/ensuring-rollback-safety-during-deployments/).
- [RFC 1034](https://www.rfc-editor.org/info/rfc1034/), DNS a význam TTL.
- [RFC 4035](https://www.rfc-editor.org/rfc/rfc4035.html), validace DNSSEC.
- [Google Search Central: Changing your hosting](https://developers.google.com/search/docs/crawling-indexing/site-move-no-url-changes).
- [Google Search Central: Redirects](https://developers.google.com/search/docs/crawling-indexing/301-redirects).
- [OWASP: Transport Layer Security](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html).
- [Let’s Encrypt: Integration Guide](https://letsencrypt.org/docs/integration-guide/), automatizace obnovy certifikátů.
- [RFC 7208, zejména § 3.2 a § 4.6.4](https://www.rfc-editor.org/rfc/rfc7208.html), SPF a limit DNS vyhodnocování.
- [RFC 6376](https://www.rfc-editor.org/info/rfc6376/), DKIM a selektory.
- [RFC 9989](https://www.rfc-editor.org/rfc/rfc9989.html), DMARC, květen 2026; nahrazuje RFC 7489 a RFC 9091.
- [RFC 9110, § 15.5.5 a § 15.5.11](https://www.rfc-editor.org/rfc/rfc9110.html), HTTP `404` a `410`.
- [Google Search Console: 404 errors](https://support.google.com/webmasters/answer/2445990?hl=en).
- [Google Search Central: Fix search-related JavaScript problems](https://developers.google.com/search/docs/crawling-indexing/javascript/fix-search-javascript).
- [WHATWG HTML: link type icon](https://html.spec.whatwg.org/multipage/links.html#rel-icon).
- [Apple: Configuring Web Applications](https://developer.apple.com/library/archive/documentation/AppleApplications/Reference/SafariWebContent/ConfiguringWebApplications/ConfiguringWebApplications.html), archivovaná dokumentace deklarace ikony.
- [W3C: Web Application Manifest](https://www.w3.org/TR/appmanifest/).

---
