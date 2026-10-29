# Vibecoders web app checklist

Veřejný checklist pro weby a aplikace postavené s AI agentem. Je psaný hlavně pro agenta: ten podle `AUDIT.md` prochází projekt a soubory v `checklist/` používá jako kontrolní seznam. Lidé ho ručně neprocházejí, čtou až report agenta. Přesnost a ověřitelnost má proto přednost před čtivostí. Tenhle soubor platí pro práci na samotném checklistu.

## Struktura

- `README.md` je rozcestník pro lidi s tabulkou kategorií.
- `AUDIT.md` je postup pro agenta, který kontroluje projekt.
- `checklist/NN-slug.md` je jedna kategorie. Nová kategorie dostane další číslo a řádek v tabulce v `README.md`.
- Každá kategorie končí sekcí `## Zdroje`.
- **Každá položka má u sebe zdroj.** Buď přímý odkaz v textu položky, nebo reference `[Název]`, jejíž adresa je v `## Zdroje` (`[Název]: https://…`). Zdroj musí podložit tvrzení, číslo nebo práh v položce. Společný řádek „Podklad:“ pod víc položkami ani obecný seznam v `## Zdroje` nestačí.

## Formát položky

```
- [ ] Krátké tvrzení, které jde ověřit. Proč na tom záleží, nejvýš dvě věty. [Zdroj] *Ověření:* jak to agent zkontroluje.
- [ ] Když projekt přijímá platby: krátké tvrzení… [Zdroj] *Ověření:* …
```

- **Kdy položka platí, říká jen její podmínka.** Položka bez „Když…“ platí pro každý projekt, i pro jednoduchý prezentační web. Položka s „Když…:“ platí, jen když podmínka sedí. Úrovně projektu ani jiné značky na začátek položky nepiš.
- **Podmínka popisuje vlastnost projektu, kterou agent zjistí sám** z kódu, konfigurace nebo nasazení, případně dotazem. Ne pocit („u větších projektů“). Když něco stojí za to až od určitého rizika, vyjádři to podmínkou. Rozhoduje, co se stane, když se věc pokazí: nepodmiňuj položku, jejíž chybění způsobí reálnou škodu i na jednoduchém webu.
- **Opakované podmínky piš stejnými slovy**, ať je agent vyhodnotí jednou pro celý projekt:

| Podmínka | Kdy sedí |
| --- | --- |
| „Když projekt má přihlášení:“ | uživatelské účty, i jen pro autora nebo pár známých lidí |
| „Když projekt ukládá data:“ | databáze, nahrané soubory nebo jiná data, o která nesmí přijít |
| „Když projekt zpracovává osobní údaje:“ | jakékoli osobní údaje, i jen jméno a e-mail z kontaktního formuláře; tuhle podmínku použij u povinností z GDPR |
| „Když projekt drží osobní údaje cizích lidí:“ | registrují se nebo data zadávají lidé, které provozovatel nezná |
| „Když projekt přijímá platby:“ | jakékoli placení, i přes externí platební bránu |
| „Když na projektu pracuje víc lidí nebo se nasazuje často:“ | tým, víc vývojářů nebo agentů, nasazení víckrát týdně |
| „Když výpadek nebo ztráta dat stojí peníze nebo zákazníky:“ | provoz, na kterém závisí tržby nebo smluvní závazky |

- Podmínky jdou spojovat („Když projekt má přihlášení a ukládá data:“). Konkrétnější podmínku („Když aplikace přijímá webhook:“) piš volně, jen ať jde ověřit.

- **Ověření** popisuje, jak položku zkontroluje agent, který projekt audituje. Přednost má způsob, který agent spustí sám: příkaz, API měřicího nástroje, čtení kódu. Když potřebuje prohlížeč, napiš *Ověření (prohlížeč):*. Když to bez člověka nejde (účet pod přihlášením, reálný telefon, úsudek), napiš *Ověření (člověk):* a co přesně má člověk udělat.

- **Jedna položka, jedna ověřitelná věc.** „Web je rychlý" není položka, „LCP pod 2,5 s" je.
- **Každý soubor** má pod nadpisem řádek `**Týká se:**`, podle kterého agent kategorii vybírá nebo přeskakuje.
- **Práh pro rozhodnutí.** Kde existuje uznávaná hodnota, uveď ji. Běžnou praxi uveď jako orientační hodnotu.
- **Čísla a pravidla, která se mění** (limity služeb, ceny, pravidla Googlu), mají u sebe datum, k jakému platí.
- **Žádná kontrola kódu člověkem.** Checklist je pro vibe codery, kteří kód nečtou. Kód, diff a konfiguraci kontroluje agent a automatické nástroje. *Ověření (člověk)* patří jen k věcem mimo kód: účty a nastavení služeb, reálný telefon, doručená pošta, právní podklady, test s uživatelem.
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
