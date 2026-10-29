# Databáze

**Týká se:** projektu, který ukládá trvalá data do databáze.

Kontroluj skutečné schéma, oprávnění a provozní nastavení, nejen definice v kódu. Testy se zápisem, migrace a obnovu spouštěj v odděleném prostředí s testovacími daty. Existující důkaz z produkce můžeš přečíst, ale audit sám nesmí změnit produkční data.

## Datový model a integrita

- [ ] Každý samostatně adresovaný záznam má jednoznačný identifikátor vynucený úložištěm. Duplicitní identita může způsobit změnu nebo smazání nesprávného záznamu. *Ověření:* přečti schéma a ověř primární klíč, unikátní identifikátor dokumentu nebo odpovídající mechanismus; v testovací databázi zkus vložit stejný identifikátor podruhé. [Datová omezení][constraints]

- [ ] Když musí být obchodní hodnota jedinečná: jedinečnost platí i při souběžném zápisu. Samotné „nejdřív vyhledej, potom vlož“ může vytvořit duplicity. *Ověření:* najdi unikátní omezení nebo ekvivalentní atomický mechanismus; spusť souběžné pokusy o vytvoření stejné hodnoty a ověř, že vznikl nejvýše jeden platný záznam. Zkontroluj požadované chování pro prázdné hodnoty a velikost písmen. [Datová omezení][constraints], [Izolace transakcí][isolation]

- [ ] Když data obsahují odkazy na jiné záznamy: vazby nemohou zůstat v nepovoleném stavu. Smazání rodiče nesmí nečekaně vytvořit sirotky ani odstranit navázaná data. *Ověření:* přečti cizí klíče nebo odpovídající serverový mechanismus; v testovacím prostředí zkus neexistující odkaz a smazání rodiče a porovnej výsledek s požadovaným chováním. [Datová omezení][constraints]

- [ ] Když aplikace ukládá peněžní částky: používá přesnou reprezentaci s určenou měnou a pravidly zaokrouhlení. Binární floating point není vhodný pro částky vyžadující přesné účtování. *Ověření:* projdi datové typy i převody mezi API, aplikací a databází; otestuj součet desetinných částek a hranice zaokrouhlení podle pravidel projektu. [Číselné typy][numeric]

- [ ] Když aplikace ukládá datum nebo čas: model rozlišuje kalendářní datum, místní čas a konkrétní okamžik. Nesprávná interpretace posouvá termíny při převodu časových pásem. *Ověření:* přečti typy a serializaci; podle významu hodnoty otestuj její uložení a načtení, převody mezi pásmy a změnu letního času. U budoucí místní události ověř zachování potřebného časového pásma. [Datum a čas][datetime]

- [ ] Když několik databázových změn tvoří jednu nedělitelnou operaci: selhání nezanechá částečný výsledek. Například převod nesmí odečíst hodnotu bez odpovídajícího připsání. *Ověření:* najdi transakční hranici nebo odpovídající mechanismus; v testu vyvolej chybu mezi zápisy a následným čtením ověř zachování původního konzistentního stavu. [Transakce][transactions]

- [ ] Když souběžné požadavky mění stejný omezený zdroj: neporuší jeho pravidla. Jde například o poslední volné místo, zůstatek nebo současnou editaci záznamu. *Ověření:* přečti použití atomických podmínek, verzování, zámků nebo izolace; spusť konkurenční požadavky a ověř konečný stav i reakci na konflikt. Samotná existence transakce nestačí. [Izolace transakcí][isolation]

## Přístupová pravidla

- [ ] Každá tabulka nebo kolekce má určené povolené operace pro jednotlivé role a nepovolený přístup se standardně zamítá. Totéž platí pro nově přidaná úložiště dat. *Ověření:* získej seznam ze skutečného schématu a porovnej jej s oprávněními, politikami nebo serverovou autorizací; neklasifikované úložiště a chybějící pravidlo označ jako nález. [Autorizace][authorization], [Izolace zákazníků][tenants]

- [ ] Bez přihlášení jsou dostupná pouze výslovně veřejná data a operace. Skrytá stránka ani veřejný klientský klíč nejsou přístupovým pravidlem. *Ověření:* bez session a s veřejnými klientskými údaji otestuj dostupné datové API včetně detailů, seznamů a exportů; pokusy o zápis prováděj nad testovacími daty. [Autorizace][authorization]

- [ ] Běžný provoz aplikace používá databázová oprávnění omezená na potřebné operace. Nemá administrátorský přístup ani právo měnit schéma, pokud to jeho funkce nevyžaduje. *Ověření:* zjisti skutečnou identitu provozního připojení a její efektivní oprávnění; odděl ji od identity pro migrace a správu. Když se izolace opírá o databázové politiky, ověř, že je provozní identita neobchází. [Zabezpečení databáze][dbsecurity], [Izolace zákazníků][tenants]

## Prostředí a testovací data

- [ ] Testovací datové sady neobsahují identifikovatelné osobní údaje z produkce. Použij syntetická nebo skutečně anonymizovaná data; pouhé nahrazení jména nemusí zabránit identifikaci. *Ověření:* projdi původ fixtures, seedů, dumpů a příloh; zkontroluj anonymizační postup a výsledek včetně volného textu. Neukládej zjištěné osobní údaje do reportu. [Testovací data][cnil]

- [ ] Když projekt používá vývojové seedy: běžné produkční nasazení je nespouští nad produkční databází. Potřebná počáteční provozní data mají samostatný postup. *Ověření:* přečti příkazy nasazení a podmínky seedovacích skriptů; nad dostupným provozním inventářem ověř známé vývojové účty a označení ukázkových dat. [Vývojové seedy][seedfiles], [Zabezpečení databáze][dbsecurity]

## Verzované migrace a nasazení

- [ ] Změny schématu jsou verzované a reprodukovatelné z repozitáře. Patří sem také indexy, omezení, databázové funkce a přístupové politiky, které projekt používá. *Ověření:* porovnej migrační soubory nebo verzované deklarace s aktuálním schématem; ruční změna bez odpovídajícího záznamu je nález. [Verzované migrace][versioned]

- [ ] Když projekt používá verzované migrace: již nasazené migrace se zpětně nepřepisují. Oprava probíhá novou migrací, aby různá prostředí neskončila pod stejnou verzí s jiným stavem. *Ověření:* porovnej historii nasazení a kontrolní součty s repozitářem; prohlédni změny již aplikovaných migračních souborů. [Verzované migrace][versioned]

- [ ] Když výpadek nebo ztráta dat stojí peníze nebo zákazníky a projekt používá verzované migrace: skutečné schéma databáze odpovídá očekávanému stavu nasazené verze. Úspěšný záznam v historii sám neodhalí pozdější ruční zásah. *Ověření:* přečti stav migrací a porovnej normalizovaný export schématu s očekávaným stavem stejné verze; nevysvětlený rozdíl označ jako nález. [Historie migrací][history], [Odchylky schématu][drift]

- [ ] Projekt umí vytvořit použitelnou databázi z prázdného prostředí. Nesmí záviset na zapomenutém ručním kroku původního autora. *Ověření:* v dočasné databázi proveď dokumentovaný instalační postup včetně potřebných výchozích dat a spusť kontrolní čtení i zápis. [Verzované migrace][versioned], [Testování migrací][migrationtests]

- [ ] Když nasazení mění schéma nebo převádí existující data: upgrade z aktuálně nasazené verze je vyzkoušený nad reprezentativními testovacími daty. Úspěšné vytvoření prázdné databáze neověří převod starých záznamů. *Ověření:* v odděleném prostředí připrav předchozí schéma a syntetická data s relevantními vazbami a hraničními hodnotami; aplikuj upgrade a porovnej očekávané výsledky. Objem dat přizpůsob riziku změny. [Testování migrací][migrationtests], [Migrační pipeline][migrationpipeline]

- [ ] Když během nasazení běží stará a nová verze aplikace současně: obě fungují s přechodným schématem. Odstranění nebo přejmenování používaného pole může rozbít stále běžící procesy. *Ověření:* přečti pořadí nasazení včetně workerů; otestuj obě verze nad přechodným schématem. U destruktivní změny ověř rozdělení na rozšíření, přechod a pozdější odstranění. [Migrace bez výpadku][zerodowntime]

- [ ] Když výpadek nebo ztráta dat stojí peníze nebo zákazníky a migrace zasahuje používaná data: její zamykání a doba běhu se vejdou do určeného provozního limitu. Limit může odpovídat plánované odstávce, pokud ji projekt připouští. *Ověření:* na reprezentativní testovací databázi změř migraci při souběžném provozu; zkontroluj čekání na zámky, přepis tabulek a nastavené timeouty. [Bezpečnost migrací][migrationstyle]

- [ ] Když migrace převádí velký objem dat po dávkách: po přerušení může bezpečně pokračovat. Opakování dokončené dávky nesmí data poškodit ani zduplikovat. *Ověření:* přečti evidenci postupu a podmínky zápisu; během testu proces přeruš a spusť znovu, potom ověř výsledná data. [Dávkové migrace][batched]

- [ ] Když nová funkce závisí na převedených datech: aktivuje se až po ověření úplnosti převodu. Dokončený deploy nemusí znamenat dokončený backfill. *Ověření:* najdi podmínku aktivace a kontrolní dotazy; ověř počet nepřevedených záznamů a požadované invarianty, nejen stav jobu „hotovo“. [Dávkové migrace][batched]

- [ ] Když migrace může ztratit data nebo změnit jejich význam: má před nasazením ověřený postup zotavení. Návrat aplikace ani metoda `down` nemusí původní data obnovit. *Ověření:* přečti plán opravy vpřed, návratu nebo obnovy; v odděleném prostředí vyzkoušej zvolený postup a ověř jeho dopad na zápisy vzniklé po migraci. [Zotavení po migraci][migrationstyle]

## Zálohy a ověřená obnova

- [ ] Když výpadek nebo ztráta dat stojí peníze nebo zákazníky: produkční data mají stanovenou maximální přípustnou ztrátu dat a dobu obnovy. RPO určuje, k jakému bodu v čase se data musí obnovit, RTO přípustnou dobu zotavení. *Ověření:* najdi vlastníkem potvrzené časové hodnoty a rozsah dat, pro který platí; pokud chybí, dej jejich určení mezi otázky. [RPO][rpo], [RTO][rto]

- [ ] Zálohování pravidelně vytváří obnovitelné kopie produkčních dat. Zapnutá volba v konfiguraci nestačí. *Ověření:* přes CLI, API nebo provozní záznamy zjisti poslední úspěšné zálohy, jejich stáří a retenci; porovnej je s potřebami projektu a hledej mezery v historii. Když má projekt stanovené RPO, ověř jeho splnění. [Zálohování][backup], [RPO][rpo]

- [ ] Postup obnovy pokrývá všechny součásti potřebné k použitelným datům. Samotný export tabulek nemusí obsahovat role, oprávnění, externí soubory nebo potřebné šifrovací klíče. *Ověření:* porovnej inventář dat a závislostí s obsahem záloh a postupem jejich opětovného vytvoření; u nahraných souborů ověř obnovu skutečného obsahu a vazeb na záznamy. [Rozsah databázového dumpu][dump], [Obnova systému][cisa]

- [ ] Obnovitelná kopie přežije smazání nebo kompromitaci běžného produkčního prostředí. Replika, na kterou se okamžitě přenese smazání, tuto ochranu sama nezajišťuje. *Ověření:* zkontroluj oddělení úložiště a oprávnění, případně offline nebo neměnnou kopii; ověř, zda identita aplikace může odstranit také všechny zálohy. [Ochrana záloh][cisa]

- [ ] Zálohy jsou chráněné před neoprávněným čtením. Obsahují stejně citlivá data jako původní databáze. *Ověření:* přečti oprávnění úložiště, nastavení šifrování a správu klíčů; ověř, že dump není veřejně dostupný ani součástí repozitáře nebo veřejného buildu. [Zabezpečení databáze][dbsecurity], [Ochrana záloh][cisa]

- [ ] Obnova ze zálohy má úspěšný test, který se pravidelně opakuje a provede znovu po podstatné změně postupu. Důkaz obsahuje skutečně obnovená data a naměřenou dobu. *Ověření:* přečti poslední protokol, nebo v odděleném prostředí proveď obnovu; ověř integritu, přístupová pravidla a hlavní datovou operaci aplikace. Když má projekt stanovené RPO a RTO, porovnej s nimi výsledek. [Testování obnovy][cisa], [RTO][rto]

- [ ] Když projekt slibuje obnovu k určitému okamžiku: tato obnova je skutečně vyzkoušená. Existence snapshotu sama neprokazuje možnost obnovy těsně před chybným zápisem. *Ověření:* v izolovaném testu vytvoř rozlišitelné změny před cílovým okamžikem a po něm; obnov k cíli a ověř přítomnost správných změn i dostupnost potřebné historie. [Obnova k okamžiku][pitr]

## Výkon dotazů a indexy

- [ ] Když výpadek nebo ztráta dat stojí peníze nebo zákazníky: hlavní datové operace splňují určený časový rozpočet při očekávaném objemu a souběhu. Výsledek nad několika ukázkovými záznamy neprokazuje výkon v provozu. *Ověření:* najdi cílové objemy, souběh a časové limity projektu; změř odpovídající dotazy nebo API nad reprezentativními testovacími daty a zaznamenej podmínky včetně stavu cache. [Výkon dotazů][queryperformance]

- [ ] Když projekt drží osobní údaje cizích lidí: indexy odpovídají skutečným drahým dotazům. Samotný počet indexů neprokazuje dobrý výkon a každý další index má náklady při zápisu. *Ověření:* získej nejdražší nebo nejčastější dotazy a jejich plány přes `EXPLAIN` nebo ekvivalent; porovnej filtrování, spojování a řazení s existujícími indexy. Úplný průchod malou tabulkou sám o sobě není chyba. [Indexy][indexes], [Plány dotazů][explain]

- [ ] Když projekt drží osobní údaje cizích lidí: načítání seznamu neprovádí samostatný doplňující dotaz pro každý záznam, pokud lze data účelně načíst hromadně. Tento vzor N+1 zvyšuje počet databázových volání s velikostí seznamu. *Ověření:* zaznamenej dotazy při stejném požadavku nad různě velkými seznamy a vyhledej opakující se dotazy lišící se jen identifikátorem. [Odhalení N+1][nplusone]

- [ ] Když seznam může překročit bezpečný rozsah jednoho požadavku: běžný požadavek má serverem vynucený omezený rozsah výsledků. Stažení celé kolekce a její rozdělení v prohlížeči databázi nechrání. *Ověření:* přečti limit a stránkování v dotazu; zkus chybějící nebo nadměrnou velikost stránky a ověř stabilní pořadí. U rozsáhlých seznamů změř také pozdní stránky. [Stránkování][pagination], [Omezení spotřeby prostředků][api-limits]

- [ ] Když aplikace vytváří databázová spojení z více instancí nebo workerů: jejich souběžný počet respektuje dostupnou kapacitu. Násobení poolů počtem instancí může vyčerpat limit databáze. *Ověření:* porovnej limit spojení s maximálním počtem instancí, workerů a velikostí poolů; zátěžovým testem ověř vracení spojení a chování při vyčerpání kapacity. [Kapacita spojení][connections]

## Zdroje

Zdroje ověřené k 26. 10. 2026. Produktová dokumentace dokládá konkrétní mechanismy a jejich omezení. Položky nevyžadují použití uvedených produktů.

- [OWASP: Database Security Cheat Sheet][dbsecurity] - minimální oprávnění, oddělení prostředí a ochrana záloh.
- [OWASP: Authorization Cheat Sheet][authorization] - výchozí zákaz, ověřování oprávnění a negativní testy.
- [OWASP: Multi-Tenant Security Cheat Sheet][tenants] - izolace zákazníků, pokrytí pravidly a skutečná provozní identita.
- [CNIL: Tester vos applications][cnil] - syntetická a anonymizovaná testovací data.
- [PostgreSQL: Constraints][constraints] - identita, povinné hodnoty, jedinečnost a referenční integrita.
- [PostgreSQL: Numeric Types][numeric] a [Date/Time Types][datetime] - přesnost částek a časová sémantika.
- [PostgreSQL: Transactions][transactions] a [Transaction Isolation][isolation] - atomicita a souběžné změny.
- [Redgate: Versioned migrations][versioned] a [Schema history table][history] - verzování, neměnnost a evidence migrací.
- [GitLab: Testing migrations][migrationtests] a [Database migration pipeline][migrationpipeline] - ověření upgradu a reprezentativního prostředí.
- [GitLab: Avoiding downtime in migrations][zerodowntime] - kompatibilní pořadí změn.
- [GitLab: Migration Style Guide][migrationstyle] - zámky, transakční omezení a zotavení.
- [GitLab: Batched background migrations][batched] - opakovatelné dávky a ověření dokončení.
- [NIST: Recovery Point Objective][rpo] a [Recovery Time Objective][rto] - cíle obnovy.
- [CISA: StopRansomware Guide][cisa] - oddělené chráněné zálohy a pravidelné testování obnovy.
- [PostgreSQL: Backup and Restore][backup], [SQL Dump][dump] a [Continuous Archiving and PITR][pitr] - rozsah záloh a různé způsoby obnovy.
- [GitLab: Query performance guidelines][queryperformance] - měření dotazů a vliv cache.
- [PostgreSQL: Indexes][indexes] a [Using EXPLAIN][explain] - přínosy a náklady indexů, interpretace plánů.
- [GitLab: QueryRecorder][nplusone] a [Pagination guidelines][pagination] - ověření počtu dotazů a omezení výsledků.
- [PostgreSQL: Connections and Authentication][connections] - kapacita databázových spojení.
- [Redgate: Drift analysis][drift] - odchylky skutečného schématu, které historie migrací sama neodhalí.
- [GitLab: Development seed files][seedfiles] - oddělení vývojových seedů.
- [OWASP: API4:2023 Unrestricted Resource Consumption][api-limits] - serverové omezení počtu vracených záznamů.

[dbsecurity]: https://cheatsheetseries.owasp.org/cheatsheets/Database_Security_Cheat_Sheet.html
[authorization]: https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
[tenants]: https://cheatsheetseries.owasp.org/cheatsheets/Multi_Tenant_Security_Cheat_Sheet.html
[cnil]: https://www.cnil.fr/fr/tester-vos-applications
[constraints]: https://www.postgresql.org/docs/current/ddl-constraints.html
[numeric]: https://www.postgresql.org/docs/current/datatype-numeric.html
[datetime]: https://www.postgresql.org/docs/current/datatype-datetime.html
[transactions]: https://www.postgresql.org/docs/current/tutorial-transactions.html
[isolation]: https://www.postgresql.org/docs/16/transaction-iso.html
[versioned]: https://documentation.red-gate.com/fd/versioned-migrations-273973333.html
[history]: https://documentation.red-gate.com/flyway/flyway-concepts/migrations/flyway-schema-history-table
[migrationtests]: https://docs.gitlab.com/development/testing_guide/testing_migrations_guide/
[migrationpipeline]: https://docs.gitlab.com/development/database/database_migration_pipeline/
[zerodowntime]: https://docs.gitlab.com/development/database/avoiding_downtime_in_migrations/
[migrationstyle]: https://docs.gitlab.com/development/migration_style_guide/
[batched]: https://docs.gitlab.com/development/database/batched_background_migrations/
[rpo]: https://csrc.nist.gov/glossary/term/recovery_point_objective
[rto]: https://csrc.nist.gov/glossary/term/Recovery_Time_Objective
[cisa]: https://www.cisa.gov/stopransomware/ransomware-guide
[backup]: https://www.postgresql.org/docs/current/backup.html
[dump]: https://www.postgresql.org/docs/current/backup-dump.html
[pitr]: https://www.postgresql.org/docs/current/continuous-archiving.html
[queryperformance]: https://docs.gitlab.com/development/database/query_performance/
[indexes]: https://www.postgresql.org/docs/current/indexes.html
[explain]: https://www.postgresql.org/docs/current/using-explain.html
[nplusone]: https://docs.gitlab.com/development/database/query_recorder/
[pagination]: https://docs.gitlab.com/development/database/pagination_guidelines/
[connections]: https://www.postgresql.org/docs/17/runtime-config-connection.html
[drift]: https://documentation.red-gate.com/flyway/flyway-concepts/drift-analysis
[seedfiles]: https://docs.gitlab.com/development/development_seed_files/
[api-limits]: https://api-security.owasp.org/editions/2023/en/0xa4-unrestricted-resource-consumption/
