# AI funkce v aplikaci

**Týká se:** aplikace, která volá jazykový model (OpenAI, Anthropic a podobně). Únik nebo zneužití klíče se tu platí přímo penězi.

- [ ] Klíč k jazykovému modelu je jen na serveru, nikdy v kódu pro prohlížeč.
- [ ] U poskytovatele je nastavený limit útraty a vypnuté automatické dobíjení kreditu.
- [ ] Každý uživatel má limit počtu požadavků. Bez něj jeden člověk nebo bot vyčerpá rozpočet za noc.
- [ ] Výstup modelu se nevkládá do stránky jako HTML. Model může vrátit cokoli, včetně skriptu, který mu někdo podstrčil.
- [ ] Model nemůže udělat nic, co by uživatel sám dělat nesměl. Když model volá nástroje nebo databázi, má jen práva přihlášeného uživatele.
- [ ] V systémovém promptu nejsou klíče, hesla ani interní údaje. Uživatel ho z modelu dřív nebo později vytáhne.
- [ ] Víš, že text od uživatele (a obsah webů nebo souborů, které model čte) může obsahovat instrukce pro model (prompt injection). Důležitá rozhodnutí nestojí jen na odpovědi modelu.
