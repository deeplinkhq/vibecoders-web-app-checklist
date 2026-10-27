# Na co myslet, když stavíš web nebo aplikaci s AI

Lidský výtah z checklistu. Ten je psaný pro agenta, tady jsou stejné principy pro člověka: co řešit, v jakém pořadí a proč. Podrobnosti a způsob ověření najde agent v `checklist/`.

## 1. Jak velké to je

Všechno ostatní se odvíjí od toho, co se stane, když se něco pokazí. Ne od toho, kolik to má stránek.

| Co stavíš | Příklad | Když se to pokazí |
| --- | --- | --- |
| **Web** | prezentace, landing page, blog, kontaktní formulář | nefunguje web nebo nedorazí zpráva |
| **Malá aplikace** | přihlášení a data pro lidi, které znáš: pro sebe, rodinu, firmu | pár hodin výpadku nevadí, data obnovíš ze zálohy |
| **Aplikace pro veřejnost** | registrují se cizí lidé, jsou tam jejich osobní údaje nebo platby | únik dat, ztráta peněz, problém se zákonem |
| **Velký provoz** | hodně uživatelů, tým, výpadek stojí peníze | přicházíš o tržby a zákazníky |

Čím výš, tím víc věcí musíš řešit. Migrace bez výpadku nebo pohotovost v noci jsou pro velký provoz. U webu by to byla ztráta času.

## 2. Vyber cestu podle velikosti

- **Web:** čisté HTML a hosting. Nejjednodušší, nejrychlejší, skoro nic se nerozbije.
- **Malá aplikace:** hotová platforma, která ti dá databázi, přihlášení a hosting v jednom. Nestav si všechno sám.
- **Aplikace pro veřejnost a víc:** plný postup. Zadání, testy, oddělený vývoj a ostrý provoz, vědomé vydávání nových verzí.
- **Nevymýšlej kolo.** E-shop s fyzickým zbožím, rezervace nebo newsletter mají hotové služby. Vibe coduj to, co jinde nekoupíš.

## 3. Připrav agentovi půdu

Agent udělá to, co je v zadání, a nic víc. Tohle platí už u nejmenšího webu.

- **Zadání (PRD):** co web dělá, pro koho, co v první verzi je a co v ní schválně není.
- **Instrukce pro agenta** v projektu (`AGENTS.md` nebo `CLAUDE.md`): pravidla, která nejsou vidět z kódu. Krátké a aktuální.
- **Skilly na opakovanou práci:** psaní zadání, testy, nasazení, u aplikace migrace databáze. Ať to agent pokaždé dělá stejně.
- **Definice hotovo:** kdy je změna hotová. Třeba: je vidět na zkušební adrese, funguje na mobilu, testy prošly.
- **Agent nesahá na ostrý provoz** a nevidí ostré klíče a data.
- **Kontrolu nech na agentovi a nástrojích.** Kód číst nemusíš, ale chtěj po agentovi, ať ti srozumitelně řekne, co změnil a co ověřil.

## 4. Co řešit u každého webu

### Obsah a vzhled

- Jeden cíl a jedno hlavní tlačítko. Do pěti sekund musí být jasné, co to je, pro koho a co mám udělat.
- Cena, kdo za tím stojí, odpovědi na námitky. Žádné vymyšlené recenze ani čísla.
- Design system jako soubor, ať agent nevymýšlí vzhled pokaždé znovu.

### Rychlost a obrázky

- Žádné fotky v originále z foťáku. Zmenšit na velikost, ve které se zobrazují, a uložit v moderním formátu (WebP, AVIF).
- Úvodní obrázek se načte hned, ostatní až při rolování. Obrázky mají zadané rozměry, ať stránka neposkakuje.
- Fonty jen v řezech, které používáš, a s českou diakritikou.
- Změř to: PageSpeed Insights nebo Lighthouse. Agent to umí spustit sám.

### Mobil a přístupnost

- Funguje na telefonu od nejmenší šířky, nikde nejezdí stránka do stran.
- **Každý obrázek má popisek (alt text).** Popisuje, co obrázek sděluje. Dekorativní obrázek má popisek prázdný.
- Dostatečný kontrast textu, tlačítka dost velká na prst.
- Web jde projít klávesnicí a je vidět, kde zrovna jsi.

### SEO a sdílení

- Každá stránka má vlastní titulek a popis. Nikde nezůstal „Document" ze šablony.
- Web nezakazuje vyhledávače (žádný zapomenutý `noindex`), má mapu stránek.
- Pěkný náhled při sdílení na sítích (obrázek a text).
- Web je v Search Console u Googlu a přidaný i do Seznamu.

### AI vyhledávání a agenti

- Odpovědi jsou přímo na stránce, ne v PDF nebo za formulářem. Konkrétní čísla, ceny, jména.
- Stejný popis firmy na webu i ve všech profilech.
- Rozhodni vědomě, které AI roboty pustíš. Zákaz trénovacích robotů nezablokuje citace v AI vyhledávání.
- Web jde přečíst i bez JavaScriptu, ať se v něm vyzná i AI agent.

### Formuláře

- Co nejmíň polí, každé s popiskem.
- Úspěch se ukáže, jen když zpráva opravdu dorazila. Vyzkoušej to naostro až do schránky.
- Ochrana proti spamu, která nesleduje návštěvníky.
- Vložená mapa nebo rezervace má vedle sebe náhradní odkaz, kdyby se nenačetla.

### Právo a analytika

- Bez sledovacích cookies nepotřebuješ cookie lištu. S nimi musí být souhlas předem a „odmítnout" stejně snadné jako „souhlasit".
- U formuláře věta o tom, k čemu údaje jsou, a odkaz na zásady zpracování. Zaškrtávátko „souhlasím" u kontaktního formuláře nepatří.
- Podnikatel má v patičce jméno, sídlo, IČO a e-mail.
- Analytika: buď s cookies a lištou, nebo bez cookies a bez lišty.

### Bezpečnost

- **Žádný klíč ani heslo v kódu, který běží v prohlížeči, ani v gitu.** Co je ve stránce, vidí každý. Když klíč unikne, vyměň ho.
- HTTPS a základní bezpečnostní hlavičky.
- Dvoufázové přihlášení na všech účtech kolem webu: doména, hosting, repozitář, e-mail.
- Knihovny, které agent přidá, opravdu existují. AI si občas vymýšlí názvy balíčků.

### Doména a spuštění

- Jedna adresa webu, ostatní varianty (s www, bez www, adresa od hostingu) přesměrované na ni.
- Při přesunu domény nezapomeň na záznamy pro e-mail, jinak ti přestane chodit pošta.
- Vlastní stránka 404 a favicon.
- Před spuštěním: všechny odkazy fungují, žádný výplňový text, formulář vyzkoušený naostro, web otevřený na skutečném telefonu.

### Provoz

- Hlídání dostupnosti, které ti napíše, když web spadne.
- Hlídání, kdy vyprší certifikát a doména.
- Rozpočet a upozornění u placených služeb.

## 5. Navíc u aplikace s přihlášením

### Aplikace

- Přihlášení, odhlášení a reset hesla fungují a jsou vyzkoušené naostro, včetně odkazu v e-mailu.
- **Oprávnění se kontrolují na serveru.** Přihlášený člověk se nedostane k cizím datům tím, že v adrese změní číslo.
- Když něco selže, uživatel vidí srozumitelnou hlášku, ne bílou stránku.

### Databáze

- **Ke každé tabulce je nastavené, kdo smí co číst a měnit.** Bez toho si kdokoli přečte celou databázi, třeba všechny e-maily z čekací listiny.
- **Migrace:** změny databáze jdou přes verzované migrace v gitu, ne klikáním v administraci.
- Oddělená databáze pro vývoj a pro ostrý provoz. Testovací data nekončí v ostrém provozu.
- **Zálohy a aspoň jednou vyzkoušená obnova.** Záloha, kterou jsi nikdy neobnovil, není záloha.

### Nasazení a testy

- Vývoj a ostrý provoz jsou oddělené, nová verze jde ven až po vyzkoušení.
- Víš, jak rychle vrátit předchozí verzi.
- Hlavní cesty (registrace, přihlášení, hlavní akce) mají automatický test a agent ho pouští po každé změně.
- Agent nesmí test „opravit" tím, že ho smaže nebo oslabí.
- Chyby z ostrého provozu se zaznamenávají a chodí o nich upozornění.

### AI funkce v aplikaci

- Klíč k modelu je jen na serveru, nikdy v prohlížeči.
- Limit útraty u poskytovatele a limit požadavků na uživatele. Jinak ti jeden bot vyčerpá rozpočet za noc.
- Model nesmí udělat nic, co by uživatel sám nesměl.
- Chatbot, který neví, to přizná. Nevymýšlí si ceny ani podmínky.

## 6. Navíc u aplikace pro veřejnost

- Platby: zaplaceno je až po potvrzení od platební brány, stejná platba se nezaúčtuje dvakrát, vývoj běží v testovacím režimu.
- Ochrana proti zneužití: limity pokusů o přihlášení, ochrana registrace proti botům, dvoufázové přihlášení pro adminy.
- Práva lidí podle GDPR: smazání účtu i z navázaných služeb, odpověď na žádost do měsíce, únik dat hlásíš do 72 hodin.
- Postup pro případ, že web spadne nebo unikne klíč, a jak dát vědět uživatelům.

## 7. Velký provoz

Až když máš hodně uživatelů nebo tým: migrace bez výpadku, formální cíle obnovy po havárii, pohotovost a zástupy, výkonnostní rozpočty při zátěži. Většiny studentů se to netýká a je v pořádku to neřešit.

## Jak to použít s agentem

Spusť agenta ve složce projektu a napiš:

```
Projdi můj projekt podle checklistu z https://github.com/deeplinkhq/vibecoders-web-app-checklist.
Postup je v AUDIT.md. Nic neopravuj, jen vypiš nálezy a zeptej se na to, co nevíš.
```

Agent určí, jak velký projekt je, projde jen to, co se ho týká, a na konci ti řekne, co musíš zkontrolovat sám (účty, telefon, schránku). Opravuj po částech a po každém kole nech kontrolu zopakovat.
