# Vibecoders web app checklist

Veřejný checklist pro weby a aplikace postavené s AI agentem. Je psaný hlavně pro agenta: ten podle `AUDIT.md` prochází projekt a soubory v `checklist/` používá jako kontrolní seznam. Lidé ho ručně neprocházejí, čtou až report agenta. Přesnost a ověřitelnost má proto přednost před čtivostí. Tenhle soubor platí pro práci na samotném checklistu.

## Struktura

- `README.md` je rozcestník pro lidi s tabulkou kategorií.
- `AUDIT.md` je postup pro agenta, který kontroluje projekt.
- `checklist/NN-slug.md` je jedna kategorie. Nová kategorie dostane další číslo a řádek v tabulce v `README.md`.
- Každá kategorie končí sekcí `## Zdroje`. Nové číslo nebo pravidlo v položce má mít zdroj tam.

## Formát položky

```
- [ ] [veřejná] Krátké tvrzení, které jde ověřit. Proč na tom záleží, nejvýš dvě věty. *Ověření:* jak to agent zkontroluje.
```

- **Úroveň** v hranatých závorkách na začátku položky je nejnižší úroveň projektu, od které položka platí. Platí pro ni a všechny vyšší. Rozhoduje to, co se stane, když se věc pokazí, ne počet řádků kódu. Když váháš, dej nižší úroveň jen tehdy, když by chybějící věc i na ní způsobila reálnou škodu.

| Úroveň | Co to je | Když se to pokazí |
| --- | --- | --- |
| `web` | prezentační web, landing page, blog, případně kontaktní formulář nebo vložená rezervace. Bez uživatelských účtů. | nefunguje web nebo formulář |
| `malá` | aplikace s přihlášením nebo daty pro známé uživatele: autor, rodina, firma, desítky lidí. Bez plateb od cizích lidí. | výpadek na pár hodin nevadí, data se obnoví ze zálohy |
| `veřejná` | registrují se cizí lidé, aplikace drží jejich osobní data nebo přijímá platby | únik dat, ztráta peněz, právní problém |
| `velká` | mnoho uživatelů nebo tým, časté vydávání, výpadek stojí peníze nebo zákazníky | ztráta tržeb a zákazníků |

- **Ověření** popisuje, jak položku zkontroluje agent, který projekt audituje. Přednost má způsob, který agent spustí sám: příkaz, API měřicího nástroje, čtení kódu. Když potřebuje prohlížeč, napiš *Ověření (prohlížeč):*. Když to bez člověka nejde (účet pod přihlášením, reálný telefon, úsudek), napiš *Ověření (člověk):* a co přesně má člověk udělat.

- **Jedna položka, jedna ověřitelná věc.** „Web je rychlý" není položka, „LCP pod 2,5 s" je.
- **Podmíněná položka** začíná „Když…" („Když aplikace přijímá platby: …").
- **Každý soubor** má pod nadpisem řádek `**Týká se:**`, podle kterého agent kategorii vybírá nebo přeskakuje.
- **Práh pro rozhodnutí.** Kde existuje uznávaná hodnota, uveď ji. Běžnou praxi uveď jako orientační hodnotu.
- **Čísla a pravidla, která se mění** (limity služeb, ceny, pravidla Googlu), mají u sebe datum, k jakému platí.
- **Obecně, bez vazby na technologii.** Žádné konkrétní frameworky, hostingy, databáze ani služby. Položka popisuje, čeho chceš dosáhnout, ne jak to udělat v konkrétním nástroji. Výjimka jsou platformy, kde lidé reálně hledají (Google, Seznam).
- **Nástroje na měření a kontrolu jmenovat můžeš** (PageSpeed Insights, Lighthouse, test bezpečnostních hlaviček a podobně). Nezávisí na stacku a agent jimi položku ověří.

## Psaní

- Čeština, tykání, krátké věty, konkrétní čísla. Anglické termíny (agent, prompt, CDN) se nepřekládají.
- Nikdy dlouhá pomlčka (em dash ani en dash), jen spojovník „-". Rozsahy psát „2 až 6".
- České uvozovky „…".
- Bez marketingových slov (revoluční, průlomový, game-changer).

## Co sem nepatří

- **Míň je líp.** Nedoplňuj položky „pro úplnost". Každá položka musí mít důvod, proč ji lidé reálně zapomínají nebo dělají špatně.
- Nic interního: klientské projekty, interní adresy, odkazy do privátních rep Deeplink HQ.
- Top vychytávky, které nechceme dávat ven, patří do privátního repa, ne sem.
- Znaky vibe coded vzhledu do hloubky budou mít vlastní repo. Tady v `02-vzhled.md` zůstává jen základ.
