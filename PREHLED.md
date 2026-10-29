# Na co myslet, když stavíš web nebo aplikaci s AI

Lidský výtah z checklistu. Ten je psaný pro agenta, tady jsou stejné principy pro člověka: co řešit, v jakém pořadí a proč. Podrobnosti a způsob ověření najde agent v `checklist/`.

## 1. Jak velký je tvůj projekt?

Všechno ostatní se odvíjí od toho, co se stane, když se něco pokazí. Ne od toho, kolik to má stránek.

| Co stavíš | Příklad | Když se to pokazí |
| --- | --- | --- |
| **Web** | prezentace, landing page, blog, kontaktní formulář | nefunguje web nebo nedorazí zpráva |
| **Malá aplikace** | přihlášení a data pro lidi, které znáš: pro sebe, rodinu, firmu | pár hodin výpadku nevadí, data obnovíš ze zálohy |
| **Aplikace pro veřejnost** | registrují se cizí lidé, jsou tam jejich osobní údaje nebo platby | únik dat, ztráta peněz, problém se zákonem |
| **Velký provoz** | hodně uživatelů, tým, výpadek stojí peníze | přicházíš o tržby a zákazníky |

Čím výš, tím víc věcí musíš řešit. Migrace bez výpadku nebo pohotovost v noci jsou pro velký provoz. U webu by to byla ztráta času.

## 2. Vyber cestu podle velikosti

- **Web:** statické stránky a hosting. Nejjednodušší, nejrychlejší, skoro nic se nerozbije.
- **Malá aplikace:** hotová platforma, která ti dá databázi, přihlášení a hosting v jednom, například Macaly nebo Lovable. Nestav si všechno sám.
- **Aplikace pro veřejnost nebo víc uživatelů:** plný postup. Zadání, testy, oddělený vývoj a ostrý provoz, vědomé vydávání nových verzí.
- **Velký provoz:** bez zkušeného vývojáře v týmu do toho nejdi. Samotný vibe coding na to nestačí.

**Nevymýšlej kolo.** E-shop s fyzickým zbožím, rezervace nebo newsletter mají hotové služby. Vibe coduj to, co jinde nekoupíš. Vlastní řešení ti dá přesně to, co chceš, ale taky starost o výpadky, údržbu a bezpečnost.

## 3. Připrav agentovi půdu

Agent udělá to, co je v zadání, a nic víc. Tohle platí už u nejmenšího webu.

- **Zadání (PRD):** co web dělá, pro koho, co v první verzi je a co v ní schválně není.
- **Instrukce pro agenta** v projektu (`AGENTS.md` nebo `CLAUDE.md`): základní pravidla a kontext projektu, které nejsou vidět z kódu.
- **Skilly na opakovanou práci:** psaní zadání, testy, nasazení, u aplikace migrace databáze. Ať to agent pokaždé dělá stejně.
- **Definice hotovo:** kdy je změna hotová. Třeba: je vidět na zkušební adrese, funguje na mobilu, testy prošly.
- **Kontrolu nech na agentovi a nástrojích.** Kód číst nemusíš, ale chtěj po agentovi, ať ti srozumitelně řekne, co změnil a co ověřil.

## 4. Co řešit u každého webu

### Obsah a vzhled

- Jeden cíl a jedno hlavní tlačítko. Na první pohled musí být jasné, co to je, pro koho a co mám udělat.
- Cena, kdo za tím stojí, odpovědi na námitky. Žádné vymyšlené recenze ani čísla.
- Žádné vyskakovací okno, které hned po příchodu zakryje obsah. Cookie lišta je výjimka.
- Telefon a e-mail jdou na mobilu otevřít jedním klepnutím.
- Ceny a data v českém formátu: `1 234,50 Kč`, `29. 10. 2026`.
- Design system jako soubor, ať agent nevymýšlí vzhled pokaždé znovu.

### Rychlost a obrázky

- Žádné fotky v originále z foťáku. Zmenšit na velikost, ve které se zobrazují, a uložit v moderním formátu (WebP nebo AVIF).
- Úvodní obrázek se načte hned, ostatní až při rolování. Obrázky mají zadané rozměry, ať stránka neposkakuje.
- Nadpis a hlavní obsah nečekají na animaci. Obsah, který se objeví až při rolování nebo po skriptu, zpomaluje web a bez JavaScriptu zůstane neviditelný.
- Místo animovaných GIFů video. Video na pozadí je zmenšené a nebrzdí zbytek stránky.
- Fonty jen v řezech, které používáš, a s českou diakritikou.
- Změř to: PageSpeed Insights nebo Lighthouse. Agent to umí spustit sám.

### Mobil a přístupnost

- Funguje na telefonu od nejmenší šířky, nikde nejezdí stránka do stran.
- **Každý obrázek má popisek (alt text).** Popisuje, co obrázek sděluje. Dekorativní obrázek má popisek prázdný.
- Dostatečný kontrast textu, tlačítka dost velká na prst. Kontrast ověříš třeba v [Color Contrast Checker](https://accessibleweb.com/color-contrast-checker/).
- Web jde projít klávesnicí a je vidět, kde zrovna jsi.
- Rolování funguje normálně. Stránka nepřeskakuje po sekcích a nepřebírá kolečko myši.

### SEO a sdílení

- Každá stránka má vlastní titulek a popis. Nikde nezůstal „Document“ ze šablony.
- Web nezakazuje vyhledávače (žádný zapomenutý `noindex`). Větší nebo nový web má mapu stránek.
- Pěkný náhled při sdílení na sítích, obrázek a text (Open Graph). Náhled ověříš třeba na [opengraph.xyz](https://www.opengraph.xyz/).
- Web je v Search Console u Googlu a přidaný i do Seznamu.

### AI vyhledávání a agenti (GEO)

- Odpovědi jsou přímo na stránce, ne v PDF nebo za formulářem. Konkrétní čísla, ceny, jména.
- Stejný popis firmy na webu i ve všech profilech.
- Rozhodni vědomě, které AI roboty v `robots.txt` pustíš. Zákaz trénovacích robotů nezablokuje citace v AI vyhledávání.
- Web jde přečíst i bez JavaScriptu. Řada AI robotů JavaScript nespouští.
- Když chceš jít dál: `llms.txt` jako rozcestník pro AI nebo verze stránek v Markdownu. Musí ale říkat totéž co web.

### Formuláře

- Co nejmíň polí, každé s popiskem.
- Úspěch se ukáže, jen když zpráva opravdu dorazila. Vyzkoušej to naostro až do schránky.
- Ochrana proti spamu, kterou kontroluje server a která nesleduje návštěvníky.
- Vložená mapa nebo rezervace má vedle sebe náhradní odkaz, kdyby se nenačetla.

### Když web něco ukládá

Stačí formulář nebo čekací listina, která zapisuje do databáze.

- **Ke každé tabulce je nastavené, kdo smí co číst a měnit.** Bez toho si kdokoli přečte celou databázi, třeba všechny e-maily z čekací listiny.
- **Zálohy a aspoň jednou vyzkoušená obnova.** Záloha, kterou jsi nikdy neobnovil, není záloha.

### Právo a analytika

- Bez sledování nepotřebuješ cookie lištu. Se sledováním musí být souhlas předem a „odmítnout“ stejně snadné jako „souhlasit“. „Bez cookies“ v popisu analytiky ještě neznamená bez souhlasu. Rozhoduje, co nástroj skutečně dělá.
- U formuláře věta o tom, k čemu údaje jsou, a odkaz na zásady zpracování. Zaškrtávátko „souhlasím“ u kontaktního formuláře nepatří.
- I web s kontaktním formulářem zpracovává osobní údaje. Musíš umět odpovědět na žádost o výmaz nebo přehled údajů do měsíce.
- Podnikatel má v patičce nebo jinde na webu jméno, sídlo, IČO.

### Bezpečnost

- **Žádný klíč ani heslo v kódu, který běží v prohlížeči, ani v gitu.** Co je ve stránce, vidí každý. Když klíč unikne, vyměň ho.
- Web běží jen přes HTTPS a adresy s HTTP na něj přesměrují.
- Dvoufázové přihlášení na všech účtech kolem webu: doména, hosting, repozitář, e-mail.

### Doména a spuštění

- Jedna adresa webu, ostatní varianty (s www, bez www, adresa od hostingu) přesměrované na ni.
- Při přesunu domény nezapomeň na záznamy pro e-mail, jinak ti přestane chodit pošta.
- Vlastní stránka 404 a favicon.
- Před spuštěním: všechny odkazy fungují, žádný výplňový text ani vymyšlený telefon, formulář vyzkoušený naostro, web otevřený na skutečném telefonu.

### Provoz

- Hlídání dostupnosti, které ti napíše, když web spadne.
- Hlídání, kdy vyprší certifikát a doména.
- Rozpočet a upozornění u placených služeb.

## 5. Navíc u aplikace s přihlášením

### Aplikace

- Přihlášení, odhlášení a reset hesla fungují a jsou vyzkoušené naostro, včetně odkazu v e-mailu.
- Heslo jde vložit ze schránky a vyplnit správcem hesel.
- **Oprávnění se kontrolují na serveru.** Přihlášený člověk se nedostane k cizím datům tím, že v adrese změní číslo.
- Dvoufázové přihlášení pro administrátory. Převzatý admin účet škodí i v malé aplikaci.
- Když vyprší přihlášení, rozepsaný text nezmizí.
- Když něco selže, uživatel vidí srozumitelnou hlášku, ne bílou stránku.
- Počty se skloňují česky: 1 položka, 2 položky, 5 položek.

### Databáze

- Změny databáze jsou verzované a jdou zopakovat, ne ruční klikání v administraci. Hotová platforma to často řeší sama.
- Oddělená databáze pro vývoj a pro ostrý provoz. Testovací data nekončí v ostrém provozu.

### Nasazení a testy

- Vývoj a ostrý provoz jsou oddělené, nová verze jde ven až po vyzkoušení.
- Víš, jak rychle vrátit předchozí verzi.
- Vlastní výpočty a pravidla mají automatické testy a agent je pouští po každé změně.
- Agent nesmí test „opravit“ tím, že ho smaže nebo oslabí.
- Chyby z ostrého provozu se zaznamenávají a chodí o nich upozornění.

## 6. Když aplikace volá AI model

- **Limit útraty.** Každý uživatel má kvótu a celý projekt pevný rozpočtový strop. Upozornění e-mailem nestačí, otevřená AI funkce ti může přes noc vyrobit velký účet.
- Limit velikosti vstupu i výstupu a časový limit každého volání.
- V promptu nejsou žádné klíče ani hesla.
- Obsah od uživatele nebo z načtených stránek nemůže modelu přepsat instrukce (prompt injection). Model dostane jen nástroje a data, které na úkol potřebuje.
- Výstup modelu se nespouští jako kód ani příkaz a v HTML se zobrazí bezpečně.
- Když model nemá podklady, umí to přiznat, místo aby si vymýšlel.

## 7. Navíc u aplikace pro veřejnost

- Platby: zaplaceno je až po potvrzení od platební brány, stejná platba se nezaúčtuje dvakrát, vývoj běží v testovacím režimu.
- Ochrana proti zneužití: limity pokusů o přihlášení, ochrana registrace proti botům.
- Hlavní cesty (registrace, přihlášení, hlavní akce) mají automatický test přes uživatelské rozhraní.
- Práva lidí podle GDPR: smazání účtu i z navázaných služeb. Únik dat, který může lidem ublížit, hlásíš úřadu do 72 hodin.
- Postup pro případ, že web spadne nebo unikne klíč, a jak dát vědět uživatelům.

## 8. Velký provoz

Až když máš hodně uživatelů nebo tým: migrace bez výpadku, formální cíle obnovy po havárii, pohotovost a zástupy, výkonnostní rozpočty při zátěži. Tady už potřebuješ zkušeného vývojáře, samotný vibe coding nestačí.

## Jak to použít s agentem

Spusť agenta ve složce projektu a napiš:

```
Projdi můj projekt podle checklistu z https://github.com/deeplinkhq/vibecoders-web-app-checklist.
Postup je v AUDIT.md. Nic neopravuj, jen vypiš nálezy a zeptej se na to, co nevíš.
```

Agent zjistí, co projekt má (přihlášení, data, osobní údaje cizích lidí, platby, tým), projde jen to, co se ho týká, a na konci ti řekne, co musíš zkontrolovat sám (účty, telefon, schránku). Opravuj po částech a po každém kole nech kontrolu zopakovat.
