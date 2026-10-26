# Bezpečnost

**Týká se:** každého webu. Podmíněné položky vybírej podle funkcí, včetně formulářů, veřejných API a integrací bez přihlášení.

Kontroluj nasazenou verzi i kód. U zamítnutého požadavku ověř, že nevrátil chráněná data ani neprovedl změnu. Testy měnící data prováděj na testovacím prostředí s testovacími účty. Do reportu nevkládej hodnoty tajemství.

### Tajné klíče a přístupové údaje

Pravidla vycházejí z [OWASP Secrets Management](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html). Oddělení přihlašovacích údajů prostředí doporučuje také [OWASP A02:2025](https://top10.owasp.org/2025/A02_2025-Security_Misconfiguration/).

- [ ] Ve veřejných souborech a odpovědích nejsou tajné klíče ani přístupové údaje. Veřejný identifikátor nebo klíč určený výrobcem pro prohlížeč není sám o sobě tajemství. *Ověření:* prohledej výsledné HTML, JavaScript, source mapy a síťové odpovědi; účel nalezených klíčů ověř v dokumentaci jejich vydavatele.

- [ ] Repozitář ani dostupná historie Gitu neobsahují použitelná tajemství. Smazání souboru z aktuální verze neodstraní jeho historii. *Ověření:* spusť Gitleaks nad pracovními soubory i historií všech dostupných větví s redakcí hodnot; zkontroluj výjimky skeneru a úplnost historie.

- [ ] Když aplikace potřebuje tajemství: získává je za běhu z neveřejné konfigurace nebo úložiště tajemství. Nejsou zapsaná ve zdrojovém kódu ani ve veřejném instalačním balíčku. *Ověření:* projdi načítání konfigurace, definice nasazení a výsledné artefakty.

- [ ] Když používáš více prostředí: produkční tajemství nejsou použitá ve vývoji ani testech. Kompromitovaný testovací projekt nesmí otevřít produkci. *Ověření:* porovnej identifikátory přístupových údajů a jejich cílová prostředí bez vypisování hodnot.

- [ ] Když aplikace používá klíč nebo servisní účet: jeho oprávnění odpovídají potřebným operacím. Klíč pro čtení nepotřebuje správu účtů ani mazání dat. *Ověření:* porovnej skutečné volání služeb s přidělenými rolemi a scopes; nedostupná nastavení vypiš k ručnímu ověření.

- [ ] Když chybí povinné tajemství: aplikace neaktivuje dotčenou funkci s výchozím nebo prázdným klíčem. Nemusí kvůli tomu přestat fungovat nesouvisející části. *Ověření:* v testovacím prostředí odeber příslušné nastavení a ověř bezpečné odmítnutí funkce.

- [ ] Když tajemství uniklo: původní přístupový údaj je zneplatněný. Nahrazení hodnoty v kódu samo nestačí. *Ověření:* zkontroluj záznam o revokaci a nasazení náhrady; bez přístupu k vydavateli označ stav „Ověř ručně“.

### Závislosti a dodavatelský řetězec

Podkladem jsou [OWASP Software Supply Chain Security](https://cheatsheetseries.owasp.org/cheatsheets/Software_Supply_Chain_Security_Cheat_Sheet.html), [Vulnerable Dependency Management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html) a [CI/CD Security](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html).

- [ ] Když projekt používá cizí balíčky: jejich názvy a původ odpovídají zamýšleným knihovnám. Existence balíčku ani vysoký počet stažení samy nepotvrzují jeho důvěryhodnost. *Ověření:* porovnej manifest a registry s instalačními pokyny oficiálního projektu; prověř neobvyklé změny vydavatele nebo zdroje.

- [ ] Když se instalují závislosti: build používá uzamčené verze včetně tranzitivních závislostí. Instalace nesmí potichu přepsat lockfile nebo stáhnout jinou verzi. *Ověření:* zkontroluj lockfile, dostupné kontrolní součty a příkaz instalace v nasazení; ověř režim odmítající nesoulad manifestu a lockfilu.

- [ ] Když projekt používá závislosti: známé zranitelnosti mají vyhodnocený dopad na aplikaci i build. Potvrzeně zneužitelný nález má opravu nebo ověřenou mitigaci. *Ověření:* spusť OSV-Scanner nebo odpovídající SCA nástroj a u nálezů zkontroluj dotčenou verzi, podmínky zneužití a evidované výjimky.

- [ ] Když projekt používá runtime nebo knihovny: bezpečnostní aktualizace použitých verzí jsou dostupné. Opuštěná kritická komponenta vyžaduje náhradu nebo doloženou údržbu. *Ověření:* porovnej nasazené verze s oficiálními informacemi o podpoře a bezpečnostními advisories; uveď datum kontroly.

- [ ] Když projekt používá CI/CD: nedůvěryhodný příspěvek nemůže získat produkční tajemství ani oprávnění k nasazení. Rizikem jsou také změny build skriptů a konfigurace pipeline. *Ověření:* projdi spouštěcí události, hranice důvěry, oprávnění jobů a dostupnost tajemství pro externí příspěvky.

- [ ] Když stránka načítá neměnný skript nebo stylesheet z cizího originu: ověřuje jeho integritu pomocí SRI nebo používá vlastní prověřenou kopii. U průběžně měněných integrací musí být výjimka konkrétně zdůvodněná. *Ověření:* projdi externí zdroje, atributy `integrity` a případně `crossorigin`; porovnej hash se skutečným obsahem. Podklad: [OWASP Third Party JavaScript Management](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Javascript_Management_Cheat_Sheet.html).

### HTTPS

Pravidla odpovídají [OWASP Transport Layer Security](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html), stav 10/2026.

- [ ] Veřejné adresy fungují přes HTTPS s důvěryhodným certifikátem pro správný hostname. Neplatný certifikát není přijatelný ani na přesměrovávající HTTPS adrese. *Ověření:* zkontroluj jednotlivé hostname pomocí `curl` bez `-k` a TLS skeneru, včetně platnosti a řetězce certifikátu.

- [ ] HTTP neposkytuje přihlášení ani chráněná data. Běžné webové adresy přesměruje na HTTPS; citlivé API může nešifrované spojení odmítnout. *Ověření:* přes `curl` zkontroluj HTTP varianty a konfiguraci endpointů; neposílej při testu skutečné přístupové údaje přes HTTP.

- [ ] Server nepovoluje SSL ani TLS 1.0 a 1.1. Preferuje TLS 1.3, TLS 1.2 může zůstat kvůli kompatibilitě. *Ověření:* spusť `testssl.sh` nebo SSLyze a zkontroluj povolené protokoly a slabé šifrovací sady.

- [ ] Stránka přes HTTPS nenačítá zdroje přes HTTP. Týká se také požadavků vytvářených JavaScriptem. *Ověření (prohlížeč):* projdi hlavní stránky a funkce; zkontroluj síťové požadavky a hlášení mixed content.

### Bezpečnostní hlavičky

Podkladem jsou [OWASP HTTP Headers](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html), [HSTS](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html) a [Content Security Policy](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

- [ ] HTTPS odpovědi posílají účinnou HSTS politiku. OWASP uvádí dlouhodobou hodnotu `max-age=63072000`; kratší hodnota je vhodná při postupném zavádění, `includeSubDomains` jen při podpoře HTTPS všech dotčených subdomén. *Ověření:* načti hlavičky přes `curl`; ověř kladné `max-age` a zdůvodnění přechodné hodnoty, neposuzuj samotné `preload` jako povinnost.

- [ ] HTML stránky mají vynucovanou CSP omezující spouštění skriptů. Účinná politika nepovoluje libovolný inline JavaScript ani `eval`; potřebný inline kód používá nonce nebo hash. *Ověření:* zkontroluj hlavičku a její direktivy pomocí CSP Evaluatoru; samotná `Content-Security-Policy-Report-Only` neznamená splnění.

- [ ] HTML stránky dovolují vložení do rámu jen zamýšleným originům. Bez požadavku na vložení použij `frame-ancestors 'none'`. *Ověření:* zkontroluj CSP v HTTP hlavičce; přijatelné omezené alternativy jsou `X-Frame-Options: DENY` nebo `SAMEORIGIN`, pokud odpovídají požadavkům projektu.

- [ ] Odpovědi posílají `X-Content-Type-Options: nosniff` se správným `Content-Type`. Prohlížeč nemá hádat spustitelný obsah podle těla odpovědi. *Ověření:* přes `curl` zkontroluj HTML, skripty, styly, API a podmíněně uživatelské soubory.

- [ ] Referrer politika neposílá cestu a query citlivé stránky cizím originům. Použij `strict-origin-when-cross-origin` nebo přísnější politiku; stránky s obnovovacími tokeny mají `no-referrer`. *Ověření:* zkontroluj hlavičky a případná přepsání v HTML; pro obnovovací stránky projdi také načítané cizí zdroje.

### Veřejně dostupné soubory a chyby

Konfiguraci pokrývá [OWASP A02:2025](https://top10.owasp.org/2025/A02_2025-Security_Misconfiguration/), chybové odpovědi [Error Handling](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html) a cache [HTTP Headers](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html).

- [ ] Produkce nezveřejňuje neveřejné konfigurace ani provozní artefakty. Patří sem `.env`, `.git`, zálohy, logy a databázové exporty. *Ověření:* projdi obsah nasazení a cíleně vyžádej odpovídající cesty; kontroluj tělo odpovědi, protože samotný stav `200` může být náhradní HTML stránka.

- [ ] Produkce nezpřístupňuje ladicí a testovací funkce neoprávněným návštěvníkům. Tajná URL není přístupová kontrola. *Ověření:* projdi routy a produkční nastavení debug režimu; vyzkoušej nalezené pomocné endpointy bez oprávnění.

- [ ] Produkční chybové odpovědi neobsahují interní technické podrobnosti ani tajemství. Uživatel nesmí dostat stack trace, databázový dotaz nebo výpis konfigurace. *Ověření:* ověř obsluhu výjimek a odpovědi na neplatné požadavky; interní selhání simuluj v testovacím prostředí.

- [ ] Když odpověď obsahuje citlivá data: nesmí ji získat jiný uživatel prostřednictvím cache. Pro obsah, který se nemá ukládat, použij `Cache-Control: no-store`. *Ověření:* prověř cache aplikace i infrastruktury a zopakuj stejnou adresu jako dva uživatelé a anonym; zkontroluj také service worker.

### Účty pro správu webu

Doporučení vycházejí z [NCSC: Protecting your admin accounts](https://www.ncsc.gov.uk/collection/using-online-services-safely/protecting-your-admin-accounts) a [CISA: phishing-resistant MFA](https://www.cisa.gov/sites/default/files/2023-01/fact-sheet-implementing-phishing-resistant-mfa-508c.pdf).

- [ ] Vlastník projektu má vlastní správcovský přístup ke kritickým službám. Provoz nesmí záviset na jediném účtu dodavatele. *Ověření (člověk):* vlastník se přihlásí vlastním účtem ke správě repozitáře, nasazení, domény a dat a zkontroluje svou roli.

- [ ] Účty spravující kritické služby mají zapnuté MFA. Zahrň také e-mail, přes který se obnovuje jejich přístup; preferuj metodu odolnou proti phishingu. *Ověření (člověk):* v nastavení každé služby ověř aktivní MFA a jeho vynucení pro další správce.

- [ ] Vlastník má dostupný bezpečný způsob obnovy správcovských účtů. Záložní faktor nebo recovery kódy nesmí být dostupné jen v účtu, jehož ztrátu mají řešit. *Ověření (člověk):* ověř uložení a dostupnost záložního způsobu bez zveřejnění kódů nebo vypnutí MFA.

- [ ] Přístup ke správě mají jen lidé, kteří ho stále potřebují. Přístupy bývalých spolupracovníků jsou odebrané. *Ověření (člověk):* porovnej seznam uživatelů, rolí a aktivních přístupových tokenů s aktuálními spolupracovníky.

### Přihlášení a obnova účtu

Podkladem jsou [NIST SP 800-63B-4](https://pages.nist.gov/800-63-4/sp800-63b.html), [OWASP Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), [Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html), [Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) a [Multifactor Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html).

- [ ] Když aplikace přijímá hesla: minimum je 15 znaků bez MFA, případně 8 znaků při povinném MFA. Povoluje alespoň 64 znaků a heslo potichu nezkracuje; jde o doporučený základ podle NIST, stav 10/2026. *Ověření:* zkontroluj serverová pravidla a testy hraničních délek.

- [ ] Když si uživatel vybírá heslo: server odmítá běžná a známá kompromitovaná hesla. Povinné velké písmeno a symbol tuhle kontrolu nenahrazují. *Ověření:* projdi kontrolu při registraci a změně hesla a její testy proti používanému blocklistu.

- [ ] Když aplikace ukládá hesla: používá solený adaptivní password hash. OWASP uvádí například Argon2id s 19 MiB paměti, 2 iteracemi a paralelismem 1 nebo jinou uvedenou odpovídající konfigurací, stav 10/2026. *Ověření:* zkontroluj algoritmus a parametry; prostý text, vratné šifrování a samotný rychlý hash nevyhovují.

- [ ] Když aplikace ověřuje přihlášení nebo obnovu účtu: server omezuje neúspěšné pokusy. Ochrana účtu nesmí záviset pouze na IP adrese útočníka. *Ověření:* najdi nastavený limit, časové okno a reakci po překročení; v testu ověř vynucení také při změně zdrojové IP.

- [ ] Když aplikace nabízí přihlášení nebo reset hesla: odpovědi neprozrazují existenci účtu. Rozdíl může být v textu, HTTP stavu i zjevně odlišném zpracování požadavku. *Ověření:* porovnej odpovědi a větvení kódu pro existující a neexistující testovací účet.

- [ ] Když aplikace má administrátorské nebo jiné vysoce privilegované účty: vyžaduje pro ně MFA. Alternativní přihlašovací cesta nesmí druhý faktor obejít. *Ověření:* projdi všechny způsoby přihlášení a zkus přístup k privilegované funkci před dokončením MFA.

- [ ] Když uživatel mění heslo, přihlašovací e-mail nebo MFA: aplikace vyžaduje opětovné ověření identity. Samotná dlouho otevřená relace nestačí. *Ověření:* zavolej příslušný endpoint bez nového ověření a zkontroluj ochranu i mimo uživatelské rozhraní.

- [ ] Když aplikace používá obnovovací nebo přihlašovací token: token je nepředvídatelný a časově omezený. Univerzální doba platnosti neexistuje, musí být zvolená podle účelu a rizika. *Ověření:* zkontroluj kryptografický generátor, vazbu tokenu na účet a účel a serverové odmítnutí po expiraci.

- [ ] Když aplikace používá jednorázový obnovovací nebo přihlašovací token: po úspěšném použití ho nelze použít znovu. *Ověření:* zopakuj použití stejného testovacího tokenu; zkontroluj atomické zneplatnění také při souběžných požadavcích.

### Relace a autentizační tokeny

Pravidla relací vycházejí z [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html). Uložení v prohlížeči řeší [HTML5 Security](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html), validaci JWT [REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html) a federované přihlášení [OAuth2](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html).

- [ ] Když přihlášení používá cookies: autentizační cookie má `Secure`, `HttpOnly` a explicitní `SameSite`. Běžně použij `Lax` nebo `Strict`; `None` potřebuje zdůvodněný cross-site scénář a `Secure`. *Ověření:* zkontroluj všechny odpovědi `Set-Cookie`, včetně obnovy přihlášení.

- [ ] Když prohlížeč uchovává přihlašovací údaje: dlouhodobé autentizační tokeny nejsou v `localStorage` ani `sessionStorage`. JavaScript stejného originu je odtud může přečíst. *Ověření:* prohledej práci s Web Storage a cestu uložení access a refresh tokenů.

- [ ] Když se uživatel přihlásí nebo zvýší oprávnění: aplikace obnoví identifikátor relace. Předem známá relace nesmí získat nová oprávnění. *Ověření:* porovnej relaci před a po přihlášení a vyzkoušej původní identifikátor.

- [ ] Když aplikace má přihlášení: server vynucuje konečnou dobu platnosti relace a pravidla neaktivity. Hodnoty odpovídají citlivosti aplikace. *Ověření:* zkontroluj timeouty a v testu ověř odmítnutí expirované relace bez závislosti na časovači v prohlížeči.

- [ ] Když se uživatel odhlásí: původní relace přestane poskytovat chráněný přístup. Vymazání cookie nebo tlačítka v prohlížeči nestačí. *Ověření:* po odhlášení zopakuj chráněný požadavek s původním cookie nebo tokenem; zahrň refresh token.

- [ ] Když API přijímá JWT: ověřuje podpis a očekávané claims, nestačí token dekódovat. Kontroluje důvěryhodného vydavatele, příjemce, expiraci a případné `nbf`; povolený algoritmus určuje konfigurace serveru. *Ověření:* otestuj token s pozměněným obsahem, cizím vydavatelem či příjemcem, po expiraci a s nepovoleným algoritmem.

- [ ] Když přihlášení používá OAuth/OIDC: přijatá odpověď je navázaná na zahájený přihlašovací tok. Používá Authorization Code s PKCE a odpovídající kontrolu `state` či OIDC `nonce`. *Ověření:* projdi konfiguraci knihovny, přesné povolené redirect URI a testy odmítnutí podvržené nebo opakované odpovědi.

### Autorizace

Podkladem jsou [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html), [Mass Assignment](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html) a [A10:2025](https://top10.owasp.org/2025/A10_2025-Mishandling_of_Exceptional_Conditions/).

- [ ] Když aplikace poskytuje neveřejná data nebo akce: server kontroluje oprávnění při každém požadavku. Skryté tlačítko, klientský redirect ani CORS nejsou autorizace. *Ověření:* sestav seznam chráněných endpointů a zavolej je přímo bez přihlášení.

- [ ] Když aplikace odděluje data uživatelů nebo organizací: změna identifikátoru neumožní přístup k cizímu objektu. Platí pro čtení, změnu, mazání, export i soubory. *Ověření:* použij dva testovací účty a zaměň ID v cestě, query i těle požadavku; u organizací ověř také hranici tenantů.

- [ ] Když aplikace rozlišuje role: nižší role nemůže provést privilegovanou operaci. Server odvozuje roli z důvěryhodného zdroje. *Ověření:* s běžným účtem přímo zavolej administrátorské endpointy a pozměň klientské údaje o roli.

- [ ] Když endpoint ukládá objekt z uživatelských dat: přijímá jen pole, která smí volající měnit. Hromadné přiřazení nesmí změnit vlastníka, roli nebo stav zaplacení. *Ověření:* zkontroluj seznam povolených polí a přidej do testovacího požadavku citlivé pole.

- [ ] Když nelze ověřit identitu nebo oprávnění: chráněná operace se neprovede. Výjimka nebo nedostupná ověřovací služba nesmí přístup povolit. *Ověření:* projdi chybové větve a v testu simuluj selhání ověření.

### Vstupy a ochrana proti zneužití

Podkladem jsou [OWASP Input Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html), [SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html), [XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) a [CSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html).

- [ ] Když aplikace přijímá vstup: server ověřuje jeho strukturu a povolené hodnoty před použitím. Kontroluje i rozsahy, délky a vnořené položky. *Ověření:* obejdi formulář a odešli chybějící pole, nesprávný typ a hodnoty mimo povolené hranice.

- [ ] Když vstup ovlivňuje databázový dotaz: data se předávají odděleně od struktury dotazu. Dynamické názvy polí a řazení vybírá server z povoleného seznamu. *Ověření:* projdi konstrukci dotazů, včetně raw dotazů a uložených procedur; hledej skládání příkazů z nedůvěryhodného vstupu.

- [ ] Když aplikace zobrazuje nedůvěryhodný obsah: vložená hodnota se nemůže stát spustitelným kódem. Ochrana odpovídá HTML, atributovému, URL nebo jinému výstupnímu kontextu. *Ověření:* projdi výstupní místa, vypnuté escapování a nebezpečné DOM operace; použij testy pro příslušné kontexty.

- [ ] Když aplikace dovoluje uživatelské HTML nebo rich text: obsah prochází udržovaným sanitizérem. Regulární výraz ani samotná CSP nejsou náhrada. *Ověření:* zkontroluj sanitizaci po převodu do HTML a testy zakázaných elementů, atributů a URL schémat.

- [ ] Když prohlížeč automaticky přikládá autentizaci: změnové požadavky mají serverovou ochranu proti CSRF. Samotné `SameSite` není plnohodnotná náhrada. *Ověření:* prověř tokenovou ochranu nebo odpovídající kontrolu původu a Fetch Metadata; otestuj požadavek z cizího originu.

- [ ] Když endpoint mění data: změnu nelze vyvolat metodou `GET`. Otevření odkazu nebo přednačtení stránky nemá provést změnu. *Ověření:* projdi routy a ověř změnové endpointy pomocí `GET` bez provedení operace.

- [ ] Když API zpřístupňuje neveřejné odpovědi jinému originu: CORS povoluje pouze zamýšlené originy. Nepřebírá libovolnou hodnotu `Origin`. *Ověření:* přes `curl` porovnej odpovědi a preflight pro povolený a cizí origin; veřejná API posuzuj podle zamýšlené dostupnosti. Podklad: [OWASP REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html).

- [ ] Když veřejná funkce spotřebovává omezené nebo placené zdroje: server vynucuje kvótu nebo rate limit. Týká se například registrací, e-mailů, exportů a náročných výpočtů. *Ověření:* zkontroluj limit a jeho rozsah; v testovacím prostředí ověř odmítnutí nad limitem. Podklad: [OWASP A10:2025](https://top10.owasp.org/2025/A10_2025-Mishandling_of_Exceptional_Conditions/).

### Podmíněné integrační a souborové funkce

- [ ] Když server načítá URL ovlivněnou uživatelem: požadavek nemůže zasáhnout nepovolené interní adresy ani metadata infrastruktury. Kontrola zahrnuje IPv4, IPv6, DNS a přesměrování. *Ověření:* projdi validaci cíle a síťová omezení; v izolovaném testu ověř odmítnutí interního cíle i redirectu na něj. Podklad: [OWASP SSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html).

- [ ] Když uživatel nahrává soubory: server přijímá pouze povolené typy ověřené podle obsahu. Přípona ani klientský `Content-Type` nestačí. *Ověření:* odešli soubor s jiným obsahem, než tvrdí název a MIME typ; zkontroluj validátor a nastavení parseru.

- [ ] Když uživatel nahrává soubory: server vynucuje limit velikosti před nákladným zpracováním. Při rozbalování nebo dekódování omezuje také výslednou velikost. *Ověření:* najdi nakonfigurované limity a otestuj jejich překročení v testovacím prostředí.

- [ ] Když aplikace ukládá uživatelské soubory: uživatelský název nemůže určit cestu mimo přidělené úložiště. Nesmí přepsat cizí ani systémový soubor. *Ověření:* projdi generování cest a otestuj názvy s `../`, absolutní cestou a kolizí.

- [ ] Když aplikace poskytuje uživatelské soubory: nepovažuje jejich obsah za důvěryhodný kód aplikace. Aktivní obsah odmítá, bezpečně převádí nebo odděluje od originu aplikace. *Ověření:* zkontroluj způsob servírování, MIME typy a `Content-Disposition`; ověř zacházení s HTML a SVG. Podkladem souborových kontrol je [OWASP File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html).

- [ ] Když aplikace přijímá webhook: ověřuje jeho pravost před provedením akce. Neznámá URL ani IP adresa samy nepotvrzují odesílatele. *Ověření:* zkontroluj ověření podpisu nebo autentizace podle protokolu odesílatele; požadavek bez důkazu nebo s pozměněným tělem nesmí provést změnu. Podklad: [OWASP Webhook Security](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html).

- [ ] Když aplikace přesměrovává podle uživatelského vstupu: cílová adresa odpovídá povolenému seznamu nebo bezpečně ověřené místní cestě. Jinak může důvěryhodná doména sloužit k phishingu. *Ověření:* otestuj absolutní cizí URL, adresu začínající `//` a jejich zakódované varianty. Podklad: [OWASP Unvalidated Redirects](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html).

- [ ] Když aplikace spouští systémový příkaz s nedůvěryhodným vstupem: vstup nemůže změnit příkaz ani přidat nepovolený argument. Preferuj knihovní API před shellem. *Ověření:* projdi spouštění procesů, oddělení argumentů a jejich povolené hodnoty; otestuj manipulaci v izolovaném prostředí. Podklad: [OWASP OS Command Injection Defense](https://cheatsheetseries.owasp.org/cheatsheets/OS_Command_Injection_Defense_Cheat_Sheet.html).

## Zdroje

- [OWASP ASVS 5.0.0](https://asvs.owasp.org/downloads/) - ověřitelné bezpečnostní požadavky; stabilní verze ověřena k 10/2026.
- [OWASP Top 10:2025](https://top10.owasp.org/2025/) - mapa rizik, nikoli certifikace bezpečnosti.
- [OWASP Secrets Management](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html) - ukládání, oprávnění a revokace tajemství.
- [OWASP Software Supply Chain Security](https://cheatsheetseries.owasp.org/cheatsheets/Software_Supply_Chain_Security_Cheat_Sheet.html), [CI/CD Security](https://cheatsheetseries.owasp.org/cheatsheets/CI_CD_Security_Cheat_Sheet.html) a [Vulnerable Dependency Management](https://cheatsheetseries.owasp.org/cheatsheets/Vulnerable_Dependency_Management_Cheat_Sheet.html).
- [OWASP Third Party JavaScript Management](https://cheatsheetseries.owasp.org/cheatsheets/Third_Party_Javascript_Management_Cheat_Sheet.html) - externí skripty a integrita.
- [OWASP Transport Layer Security](https://cheatsheetseries.owasp.org/cheatsheets/Transport_Layer_Security_Cheat_Sheet.html), [HTTP Headers](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Headers_Cheat_Sheet.html), [HSTS](https://cheatsheetseries.owasp.org/cheatsheets/HTTP_Strict_Transport_Security_Cheat_Sheet.html) a [CSP](https://cheatsheetseries.owasp.org/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).
- [OWASP Error Handling](https://cheatsheetseries.owasp.org/cheatsheets/Error_Handling_Cheat_Sheet.html) a [A10:2025](https://top10.owasp.org/2025/A10_2025-Mishandling_of_Exceptional_Conditions/) - chyby a bezpečné selhání.
- [NCSC: Protecting your admin accounts](https://www.ncsc.gov.uk/collection/using-online-services-safely/protecting-your-admin-accounts) a [CISA: Implementing Phishing-Resistant MFA](https://www.cisa.gov/sites/default/files/2023-01/fact-sheet-implementing-phishing-resistant-mfa-508c.pdf).
- [NIST SP 800-63B-4](https://pages.nist.gov/800-63-4/sp800-63b.html) - zejména sekce 3.1.1 o heslech.
- [OWASP Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html), [Password Storage](https://cheatsheetseries.owasp.org/cheatsheets/Password_Storage_Cheat_Sheet.html), [Forgot Password](https://cheatsheetseries.owasp.org/cheatsheets/Forgot_Password_Cheat_Sheet.html) a [Multifactor Authentication](https://cheatsheetseries.owasp.org/cheatsheets/Multifactor_Authentication_Cheat_Sheet.html).
- [OWASP Session Management](https://cheatsheetseries.owasp.org/cheatsheets/Session_Management_Cheat_Sheet.html), [HTML5 Security](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html), [REST Security](https://cheatsheetseries.owasp.org/cheatsheets/REST_Security_Cheat_Sheet.html) a [OAuth2](https://cheatsheetseries.owasp.org/cheatsheets/OAuth2_Cheat_Sheet.html).
- [OWASP Authorization](https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html) a [Mass Assignment](https://cheatsheetseries.owasp.org/cheatsheets/Mass_Assignment_Cheat_Sheet.html).
- [OWASP Input Validation](https://cheatsheetseries.owasp.org/cheatsheets/Input_Validation_Cheat_Sheet.html), [SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html), [XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html) a [CSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html).
- [OWASP SSRF Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Server_Side_Request_Forgery_Prevention_Cheat_Sheet.html), [File Upload](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html), [Webhook Security](https://cheatsheetseries.owasp.org/cheatsheets/Webhook_Security_Cheat_Sheet.html), [Unvalidated Redirects](https://cheatsheetseries.owasp.org/cheatsheets/Unvalidated_Redirects_and_Forwards_Cheat_Sheet.html) a [OS Command Injection Defense](https://cheatsheetseries.owasp.org/cheatsheets/OS_Command_Injection_Defense_Cheat_Sheet.html).
