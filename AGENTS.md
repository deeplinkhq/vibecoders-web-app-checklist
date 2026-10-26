# Vibecoders web app checklist

Veřejný checklist pro weby a aplikace postavené s AI agentem. Čtou ho lidé i agenti: agent podle `AUDIT.md` prochází cizí projekty a soubory v `checklist/` používá jako kontrolní seznam. Tenhle soubor platí pro práci na samotném checklistu.

## Struktura

- `README.md` je rozcestník pro lidi s tabulkou kategorií.
- `AUDIT.md` je postup pro agenta, který kontroluje projekt.
- `checklist/NN-slug.md` je jedna kategorie. Nová kategorie dostane další číslo a řádek v tabulce v `README.md`.
- Každá kategorie končí sekcí `## Zdroje`. Nové číslo nebo pravidlo v položce má mít zdroj tam.

## Formát položky

```
- [ ] Krátké tvrzení, které jde ověřit. Proč na tom záleží, nejvýš dvě věty. *Ověření:* jak to agent zkontroluje.
```

- **Ověření** popisuje, jak položku zkontroluje agent, který projekt audituje. Přednost má způsob, který agent spustí sám: příkaz, API měřicího nástroje, čtení kódu. Když potřebuje prohlížeč, napiš *Ověření (prohlížeč):*. Když to bez člověka nejde (účet pod přihlášením, reálný telefon, úsudek), napiš *Ověření (člověk):* a co přesně má člověk udělat.

- **Jedna položka, jedna ověřitelná věc.** „Web je rychlý" není položka, „LCP pod 2,5 s" je.
- **Podmíněná položka** začíná „Když…" („Když aplikace přijímá platby: …").
- **Každý soubor** má pod nadpisem řádek `**Týká se:**`, podle kterého agent kategorii vybírá nebo přeskakuje.
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
