# Provoz

**Týká se:** každého nasazeného webu nebo aplikace, které mají zůstat v provozu. Podmíněné položky vybírej podle funkcí a dopadu jejich selhání.

Ověřuj skutečnou produkční konfiguraci a dostupné záznamy. Soubor v repozitáři sám nedokazuje, že monitoring běží. Když nemáš přístup k nastavení nebo důkazu, označ „Ověř ručně“ a napiš, co má provozovatel doložit.

Samotný audit není pokyn k vyvolání produkční chyby, odeslání zprávy, zastavení služby ani obnově dat. Použij existující důkazy nebo izolované testovací prostředí.

## Dostupnost a funkčnost

Podkladem je rozlišení vnějšího a vnitřního monitoringu v [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/).

- [ ] [web] Dostupnost veřejného webu pravidelně kontroluje monitor mimo prostředí, jehož výpadek má odhalit. Kontrola ověřuje očekávaný HTTP status i rozpoznatelný obsah přes skutečnou veřejnou HTTPS adresu. *Ověření:* přečti konfiguraci monitoru a historii jeho běhů; porovnej URL, očekávanou odpověď a skutečný GET přes `curl`.

- [ ] [velká] Monitoring dostupnosti má stanovenou cílovou dobu od vzniku výpadku do odeslání upozornění. Nastavení intervalu kontrol, timeoutu, opakování a zpoždění upozornění tomuto cíli odpovídá. *Ověření:* porovnej nastavení se zdokumentovaným cílem provozovatele a časovými údaji z poslední zkoušky; potvrzenou neexistenci cíle označ „Chybí“.

- [ ] [web] Když web obsahuje kritický uživatelský postup: pravidelná kontrola ověřuje jeho výsledný účinek. U kontaktního formuláře jde o doručení do cílové schránky nebo systému, ne jen o zobrazení potvrzení. *Ověření:* porovnej seznam kritických postupů s naplánovanými automatickými nebo doloženými ručními kontrolami a záznamy výsledků; ověř oddělení testovacích účtů, příjemců a dat.

- [ ] [malá] Když aplikace vykonává vlastní kód: produkční chyby relevantních částí aplikace se zaznamenávají mimo lokální vývojovou konzoli. Zahrň server, prohlížeč a úlohy na pozadí podle skutečné architektury. *Ověření:* projdi inicializaci záznamu chyb v nasazené konfiguraci a dohledávej odpovídající události z existujícího testu. Podklad: [Google SRE: Production Readiness Review](https://sre.google/sre-book/evolving-sre-engagement-model/).

- [ ] [malá] Když na včasném dokončení plánovaných úloh nebo zpracování na pozadí závisí funkčnost aplikace či ochrana dat: monitoring odhalí překročení povolené doby bez úspěšného dokončení. Samotný záznam spuštění ani upozornění o vyhozené výjimce neodhalí úlohu, která vůbec nenastartovala. *Ověření:* porovnej plán úloh, poslední úspěšná dokončení a pravidla pro zpoždění; u front zkontroluj také stáří nezpracované práce. Podklad: [Prometheus: Instrumentation](https://prometheus.io/docs/practices/instrumentation/).

- [ ] [web] Když web používá vlastní HTTPS hostname: na blížící se expiraci certifikátu přijde upozornění s časem na opravu. Automatická obnova nenahrazuje kontrolu jejího výsledku. *Ověření:* načti skutečný certifikát pomocí OpenSSL a porovnej jeho platnost s nastavením monitoru expirace. Podklad: [Monitoring TLS certifikátů](https://letsencrypt.org/docs/monitoring-options/).

## Upozornění

Podklady: [Google SRE: Production Services Best Practices](https://sre.google/sre-book/service-best-practices/) a [Prometheus: Alerting](https://prometheus.io/docs/practices/alerting/).

- [ ] [velká] Každé provozní upozornění má určeného příjemce odpovědného za reakci. Je popsané, kdy je dostupný, do kdy má reagovat a komu se problém předá při jeho nedostupnosti. *Ověření:* porovnej skutečné směrování upozornění s provozními kontakty a pravidly zastupování; ověř, že pokrytí odpovídá požadavkům projektu.

- [ ] [veřejná] Upozornění vyžadující zásah mají jednoznačnou spouštěcí podmínku a navazující postup. Podmínka určuje sledovanou událost nebo měřený jev s prahem a případnou dobou trvání; zpráva identifikuje dotčený projekt a odkazuje na diagnostiku nebo postup nápravy. *Ověření:* projdi aktivní pravidla a ukázky doručených zpráv; zkontroluj také slučování duplicit stejného problému.

- [ ] [web] Doručení upozornění je doložené zkouškou celého řetězce od sledované události po cílový kanál. Odeslání testovacího e-mailu samo neověří sběr dat a vyhodnocení pravidla. *Ověření:* dohledávej časově propojený záznam testovací události, aktivace pravidla a doručení; při nové zkoušce použij izolovaný cíl bez dopadu na uživatele.

## Logy

Podklady: [OWASP: Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) a [The Twelve-Factor App: Logs](https://12factor.net/logs).

- [ ] [veřejná] Když aplikace vytváří provozní logy: událost lze přiřadit k času, prostředí, komponentě a nasazené verzi. Události jedné operace propojuje identifikátor požadavku nebo úlohy. *Ověření:* projdi vzorek skutečných záznamů a dohledávej průchod jedné testovací operace.

- [ ] [malá] Když aplikace vytváří provozní logy: záznamy zůstávají dostupné i po restartu nebo nahrazení běžící instance. *Ověření:* zkontroluj odvod logů a dohledávej událost před posledním restartem či nasazením.

- [ ] [malá] Když se uchovávají logy nebo hlášení chyb: jejich skutečná retence odpovídá zdokumentované potřebě vyšetřování a povinnostem projektu. Uchování není neomezené bez konkrétního důvodu. *Ověření:* porovnej retenční politiku s nastavením mazání, archivů a dostupností starších záznamů.

- [ ] [web] Když se sbírají logy nebo hlášení chyb: neobsahují hesla, tajné klíče ani použitelné přístupové tokeny. Osobní údaje jsou omezené na doložený účel. *Ověření:* prověř sanitizaci a vzorek událostí včetně URL, hlaviček, těl požadavků a příloh; nalezené hodnoty nevypisuj do reportu.

## Náklady a limity

Podklady: [FinOps Foundation: Budgeting](https://www.finops.org/framework/capabilities/budgeting/), [Anomaly Management](https://www.finops.org/framework/capabilities/anomaly-management/) a [OWASP API4: Unrestricted Resource Consumption](https://owasp.org/API-Security/editions/2023/en/0xa4-unrestricted-resource-consumption/).

- [ ] [web] Když projekt používá placené služby: má stanovený rozpočet pro určené období a při variabilním účtování upozornění na hrozící překročení. Přehled zahrnuje také variabilní náklady integrací, přenosů, úložišť a monitoringu. *Ověření:* porovnej inventář služeb s rozpočty, skutečnou spotřebou a způsobem účtování; u variabilních nákladů ověř aktivní upozornění a jejich příjemce.

- [ ] [web] Když funkce vytváří variabilní náklady: její spotřebu omezuje vynucovaný limit, nebo je doložený náhradní postup jejího omezení. Samotné rozpočtové upozornění nemusí další účtování zastavit. *Ověření:* ověř skutečný rozsah a zpoždění limitu podle aktuální dokumentace poskytovatele; bez limitu dohledávej upozornění a konkrétní postup vypnutí či omezení funkce.

- [ ] [veřejná] Když vyčerpání kapacity nebo kvóty může přerušit službu: její využití se sleduje a upozornění přijde s rezervou na zásah. Práh vychází z limitu, růstu spotřeby a potřebné doby reakce. *Ověření:* porovnej aktuální kvóty, historii využití a pravidla upozornění; u limitů služeb uveď datum kontroly.

- [ ] [web] Když projekt používá vlastní doménu: její prodloužení má funkční platební a upozorňovací postup. Automatické prodloužení je přijatelné, stejně jako doložené ruční prodlužování před expirací. *Ověření (člověk):* u registrátora ověř datum expirace, způsob prodloužení, platební podmínky a aktuální kontaktní adresu. Podklad: [ICANN: Domain Name Renewals and Expiration](https://www.icann.org/resources/pages/domain-name-renewal-expiration-faqs-2018-12-07-en/).

## Incidenty a obnova

Podklady: [NIST SP 800-61r3](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r3.pdf), [NIST SP 800-34r1](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-34r1.pdf) a [Google SRE: Managing Incidents](https://sre.google/sre-book/managing-incidents/).

- [ ] [veřejná] Existuje provozní postup pro relevantní závažné incidenty, dostupný i při výpadku aplikace. Podle projektu pokrývá nedostupnost, poškození dat, únik přístupu a nekontrolovanou spotřebu. *Ověření:* dohledávej konkrétní první kroky, odpovědnosti a odkazy na obnovu či omezení služby; ověř dostupnost dokumentu nezávisle na aplikaci.

- [ ] [velká] Když výpadek může způsobit významnou škodu: projekt má stanovený časový cíl obnovy provozu, RTO. *Ověření:* přečti schválenou hodnotu a porovnej ji s naměřenou délkou poslední zkoušky obnovy; potvrzenou neexistenci cíle označ „Chybí“.

- [ ] [malá] Když projekt vyžaduje obnovu po závažném selhání: existuje záznam úspěšné zkoušky obnovy celé kritické funkce. Obnova samotné databáze neověřuje potřebnou konfiguraci, soubory a navazující služby. *Ověření:* zkontroluj scénář, datum, obnovenou verzi a výsledky funkčních kontrol v izolovaném prostředí.

- [ ] [veřejná] Když incident zasahuje uživatele: je určený způsob informování, který zůstane použitelný i při výpadku aplikace. *Ověření:* ověř komunikační kanál, odpovědnou osobu a připravený postup aktualizace informací.

- [ ] [veřejná] Když nastal závažný nebo opakovaný incident: jeho záznam obsahuje nápravná opatření s odpovědností a termínem. *Ověření:* porovnej evidenci incidentů s navazujícími úkoly a důkazy jejich dokončení. Podklad: [Google SRE: Incident Management Guide](https://sre.google/resources/practices-and-processes/incident-management-guide/).

## Aktualizace a údržba

Podklady: [CISA: Poor Patch Management](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-278a) a [OWASP: Vulnerable Dependency Management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html).

- [ ] [malá] Pravidelná provozní kontrola má odpovědnou osobu, interval a evidovaný výsledek. Rozsah odpovídá projektu a zahrnuje relevantní kontroly funkčnosti, nákladů, obnovy a expirací z této kategorie. *Ověření:* porovnej plán s posledními provedenými kontrolami; univerzální měsíční interval nepředpokládej.

- [ ] [web] Když projekt používá softwarové komponenty ve správě provozovatele: nové bezpečnostní informace se vyhodnocují i mezi pravidelnými kontrolami. Potvrzené nálezy mají termín řešení podle dopadu a dostupnosti zneužití. *Ověření:* zkontroluj odběr advisories nebo automatické kontroly, jejich skutečné běhy a způsob předání nálezů odpovědné osobě.

- [ ] [web] Když se aktualizuje komponenta aplikace: změna má doložené ověření dotčených funkcí před produkčním nasazením. Automatické vytvoření aktualizačního návrhu ani zelený sken zranitelností neověřují funkčnost aplikace. *Ověření:* dohledávej konkrétní změnu verze, výsledky relevantních testů a návaznost na nasazený release.

## Předání projektu

Podkladem je [Google SRE: The Evolving SRE Engagement Model](https://sre.google/sre-book/evolving-sre-engagement-model/), zejména dokumentace, školení a převod odpovědností.

- [ ] [malá] Provozní dokumentace obsahuje aktuální inventář prostředí a služeb s jejich účelem a vlastníkem. Zahrnuje podle projektu doménu, nasazení, ukládání dat, doručování zpráv, monitoring a placené integrace. *Ověření:* porovnej inventář se skutečnou konfigurací a dostupným přehledem účtů.

- [ ] [malá] Provozní dokumentace odkazuje na proveditelné postupy nasazení, návratu verze, diagnostiky a obnovy. Obsahuje názvy potřebné konfigurace a bezpečný způsob získání přístupů, bez hodnot tajemství. *Ověření:* porovnej postupy se současnými příkazy, konfigurací a posledními záznamy jejich použití.

- [ ] [malá] Když projekt přebírá jiný správce: předání je doložené praktickým ověřením jeho schopnosti projekt provozovat. *Ověření (člověk):* přebírající správce svými oprávněními otevře provozní přehledy a podle dokumentace provede dohodnutou operaci v testovacím prostředí; zaznamenej výsledek a chybějící přístupy.

## Zdroje

Ověřeno k 26. 10. 2026. Položky jsou praktickou syntézou doporučení, nikoli doslovným přepisem povinností standardů. Časové a finanční prahy určuje projekt podle dopadu selhání.

- [Google SRE: Monitoring Distributed Systems](https://sre.google/sre-book/monitoring-distributed-systems/) - vnější kontroly, symptomy a návrh monitoringu.
- [Google SRE: Production Services Best Practices](https://sre.google/sre-book/service-best-practices/) - rozlišení okamžitého zásahu, úkolu a pouhého záznamu.
- [Prometheus: Alerting](https://prometheus.io/docs/practices/alerting/) - použitelné alerty a kontrola celého upozorňovacího řetězce.
- [Prometheus: Instrumentation](https://prometheus.io/docs/practices/instrumentation/) - úspěšné dokončení úloh, průchod zpracováním a provozní metriky.
- [Let's Encrypt: Monitoring Service Options](https://letsencrypt.org/docs/monitoring-options/) - sledování expirace.
- [Let's Encrypt: Ending Support for Expiration Notification Emails](https://letsencrypt.org/2025/01/22/ending-expiration-emails/) - od 4. 6. 2025 Let's Encrypt neposílá e-maily o blížící se expiraci, upozornění musí zajistit vlastní monitor.
- [OWASP: Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html) - obsah logů, citlivé údaje a retence.
- [The Twelve-Factor App: Logs](https://12factor.net/logs) - sběr provozních záznamů mimo jednotlivé procesy.
- [FinOps Foundation: Budgeting](https://www.finops.org/framework/capabilities/budgeting/) - rozpočet a odpovědnost za náklady.
- [FinOps Foundation: Anomaly Management](https://www.finops.org/framework/capabilities/anomaly-management/) - detekce neočekávané spotřeby.
- [OWASP API4:2023, Unrestricted Resource Consumption](https://owasp.org/API-Security/editions/2023/en/0xa4-unrestricted-resource-consumption/) - omezení spotřeby a finanční upozornění.
- [ICANN: Domain Name Renewals and Expiration](https://www.icann.org/resources/pages/domain-name-renewal-expiration-faqs-2018-12-07-en/) - prodlužování domén a platební údaje; konkrétní pravidla ověř u příslušného registru a registrátora.
- [NIST SP 800-61r3, duben 2025](https://nvlpubs.nist.gov/nistpubs/specialpublications/nist.sp.800-61r3.pdf) - příprava, řešení a ověření obnovy po incidentu.
- [NIST SP 800-34r1](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-34r1.pdf) - význam RTO a RPO.
- [Google SRE: Managing Incidents](https://sre.google/sre-book/managing-incidents/) - odpovědnosti a komunikace.
- [Google SRE: Incident Management Guide](https://sre.google/resources/practices-and-processes/incident-management-guide/) - vyhodnocení incidentů a nápravná opatření.
- [CISA: Top Ten Cybersecurity Misconfigurations](https://www.cisa.gov/news-events/cybersecurity-advisories/aa23-278a) - pravidelná údržba a prioritizace bezpečnostních oprav.
- [OWASP: Vulnerable Dependency Management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html) - vyhodnocení nálezů a ověření aktualizací.
- [Google SRE: The Evolving SRE Engagement Model](https://sre.google/sre-book/evolving-sre-engagement-model/) - připravenost produkce, dokumentace a praktické předání.
