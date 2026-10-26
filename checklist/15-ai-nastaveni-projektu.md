# AI nastavení projektu

**Týká se:** každého projektu, ve kterém AI agent vytváří nebo mění kód, konfiguraci či dokumentaci. Platí i pro web bez AI funkcí.

Při auditu rozlišuj napsaná pravidla, skutečně načtené instrukce a technicky vynucená omezení. Aktivní zkoušky dělej v odděleném testovacím prostředí bez produkčních přístupů. Když nemáš potřebný přístup nebo bezpečné prostředí, uveď „Ověř ručně“.

Názvy souborů jsou příklady. Použij formát podporovaný konkrétním agentem a verzí. Chování nástrojů a zdroje ověřeny k 26. 10. 2026.

## Instrukce pro agenta

- [ ] Projektové instrukce jsou verzované spolu s projektem. Agent se k trvalým pravidlům dostane i v nové konverzaci a na jiném počítači. *Ověření:* najdi `AGENTS.md`, `CLAUDE.md`, pravidla editoru nebo jejich podporovaný ekvivalent a přes `git ls-files` ověř, že potřebné soubory patří do repozitáře. [Dokumentace pravidel](https://cursor.com/docs/rules).

- [ ] Používaný agent skutečně načítá instrukce platné pro upravovanou část projektu. Název souboru sám nestačí; načítání může změnit nadřazená konfigurace, lokální nastavení nebo limit velikosti. *Ověření:* zjisti verzi a aktivní konfiguraci agenta; v diagnostice nebo záznamu nové relace ověř načtené soubory z kořene i relevantního podadresáře. Ruční vložení souboru do promptu není důkaz automatického načítání. [Codex](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [Claude Code](https://code.claude.com/docs/en/memory).

- [ ] Aktivní instrukce si pro stejnou oblast neodporují. Když sdílíš pravidla mezi více agenty, je určený jejich hlavní zdroj a způsob přenosu změn. *Ověření:* porovnej projektová, nadřazená a dostupná uživatelská pravidla; zkontroluj importy, symlinky a generované kopie. Rozdíly specifické pro jednotlivé agenty musí být výslovné. [Údržba instrukcí](https://code.claude.com/docs/en/memory).

- [ ] Instrukce uvádějí projektová omezení, která z kódu nejsou zřejmá. Typicky jde o kompatibilitu veřejného API, vlastnictví dat nebo zákaz změn určité části systému. *Ověření:* porovnej instrukce s platnými rozhodnutími a významnými opravami v historii; pravidla musí říkat, kdy platí a jaký postup je přípustný. [Pravidla pro review](https://developers.openai.com/blog/custom-code-review-rules-for-codex).

- [ ] Agent má dohledatelné funkční příkazy pro přípravu projektu, spuštění a jeho kontroly. Postup nesmí záviset na nevysvětleném nastavení autorova počítače. *Ověření:* porovnej dokumentované příkazy se skripty, požadovanými verzemi nástrojů a CI; v čistém testovacím prostředí ověř příkazy potřebné pro danou změnu. [Doporučení pro práci agenta](https://code.claude.com/docs/en/best-practices).

- [ ] Instrukce odkazují na současné soubory a postupy. Po změně příkazů, architektury nebo způsobu nasazování je součástí změny i úprava dotčených instrukcí. *Ověření:* ověř existenci odkazovaných cest a příkazů a porovnej je s posledními souvisejícími změnami; hledej i pravidla pro již odstraněné části projektu. [Audit instrukcí](https://code.claude.com/docs/en/memory).

## Zadání a zapsaná rozhodnutí

- [ ] Aktuální práce má dohledatelné zadání s cílem a hranicemi rozsahu. Pro malou opravu může stačit issue; pro novou aplikaci nebo větší funkci použij PRD či obdobnou specifikaci. *Ověření:* najdi zadání propojené s rozpracovanou změnou a ověř, že popisuje řešený problém, cílového uživatele, požadovaný výsledek a co do změny nepatří. [Specifikace podle rozsahu práce](https://github.com/github/spec-kit/blob/main/docs/guides/agentic-sdlc.md).

- [ ] Požadované chování má ověřitelná akceptační kritéria. „Funguje přihlášení“ nestačí; musí být poznat očekávaný výsledek úspěšného i relevantního chybového scénáře. *Ověření:* ke každému požadavku měnícímu chování najdi vstup nebo výchozí stav, akci a pozorovatelný výsledek; neurčité výrazy musí mít rozhodovací kritérium. [Šablona specifikace](https://github.com/github/spec-kit/blob/main/templates/spec-template.md).

- [ ] Nevyřešené otázky v zadání jsou označené jako otázky nebo předpoklady. Agent si nesmí domyslet schválení rozhodnutí, které mění rozsah, přístup k datům nebo nevratné chování. *Ověření:* projdi otevřené otázky a jejich vypořádání; u rozhodnutí, na kterých implementace závisí, dohledávej odpověď oprávněného člověka. [Vyjasnění požadavků](https://github.github.com/spec-kit/reference/agentic-sdd.html).

- [ ] Když projekt obsahuje zásadní nebo obtížně vratné rozhodnutí: jeho důvod je zapsaný mimo historii chatu. Záznam rozlišuje navržené, přijaté a nahrazené rozhodnutí. *Ověření:* najdi ADR nebo obdobný záznam s kontextem, zvažovanými možnostmi, rozhodnutím a důsledky; nahrazené rozhodnutí musí odkazovat na nové. [Záznamy rozhodnutí](https://learn.microsoft.com/en-us/azure/well-architected/architect-role/architecture-decision-record).

## Definice „hotovo“

- [ ] Projekt má zapsanou definici „hotovo“ s požadovanými důkazy. Rozlišuje kontroly podle dopadu změny, například test logiky, kontrolu rozhraní v prohlížeči nebo ověření změny dat. *Ověření:* najdi definici v instrukcích nebo odkazovaném postupu a ověř, že podle ní lze rozhodnout o dokončení konkrétní změny; samotné prohlášení agenta není důkaz. [Ověřování výsledku](https://code.claude.com/docs/en/best-practices).

- [ ] Závěrečný report agenta rozlišuje provedené a neprovedené ověření. Úspěšný build nedokazuje funkční uživatelskou cestu ani správné nasazení. *Ověření:* u poslední dokončené změny porovnej report s výstupy kontrol, testovanou revizí a prostředím; přeskočené nebo zablokované kontroly musí být výslovně uvedené. [Dokládání výsledků práce](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

## Skilly a opakovatelné postupy

- [ ] Když se určitá práce opakuje: agent má dostupný udržovaný postup místo závislosti na starém chatu. Může jít o psaní PRD, testování, audit nebo přípravu nasazení; samostatný skill není povinný. *Ověření:* porovnej opakované úlohy v historii projektu s dostupnými postupy; postup musí mít vymezené použití, potřebné vstupy, kroky a očekávaný výstup. [Opakovatelné pracovní postupy](https://docs.github.com/en/copilot/tutorials/roll-out-at-scale/enable-developers/drive-team-agentic-adoption).

- [ ] Když projekt používá skilly: používaný agent je dokáže najít a správně vybrat. Přítomnost `SKILL.md` v libovolné složce nestačí. *Ověření:* ověř umístění a metadata podle dokumentace dané verze; v katalogu nebo záznamu běhu zkontroluj dostupnost a na odpovídajícím i nesouvisejícím zadání ověř výběr skillu. [Formát Agent Skills](https://agentskills.io/specification), [použití skillů](https://learn.chatgpt.com/docs/build-skills).

- [ ] Když se tým spoléhá na skill nebo automatizovaný postup: existuje zkouška jeho výsledku. Nestačí, že agent zavolal požadovaný nástroj. *Ověření:* na reprezentativním vstupu v testovacím prostředí porovnej vzniklý výstup s předem určeným očekáváním; po podstatné změně postupu zkoušku zopakuj. [Ověřování postupů](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

- [ ] Když agent připravuje migraci nebo nasazení: postup obsahuje kontrolní bod před změnou cílového prostředí. V něm je určený cíl, očekávaný dopad, ověření výsledku a způsob obnovy při selhání. *Ověření:* projdi postup a dostupný záznam zkoušky mimo produkci; u nevratných kroků musí být uvedená omezení obnovy a požadované schválení před provedením. [Řízení rizikových akcí](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

## Oprávnění a ochrana dat

- [ ] Pravidla určují hranice samostatné práce agenta. Musí být jasné, které operace jsou povolené a které vyžadují výslovné schválení, zejména nevratné změny dat, publikování a změny oprávnění. *Ověření:* porovnej instrukce a nastavení schvalování; u rizikové operace musí být schválení vztažené ke konkrétní akci a cíli. [Hranice autonomie](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

- [ ] Skutečná oprávnění agenta odpovídají jeho úloze. Audit má mít přístup pro čtení; vývojová práce nemá automaticky znamenat přístup ke všem souborům, síti a připojeným službám. *Ověření:* prověř aktivní sandbox, oprávnění nástrojů, připojené účty a možnosti spuštění mimo omezení; nezaměňuj omezení terminálu za omezení MCP, aplikací nebo prohlížeče. [Sandbox a schvalování](https://learn.chatgpt.com/docs/agent-approvals-security).

- [ ] Když projekt má produkční prostředí: běžné vývojové prostředí agenta nemá produkční přístupy. Výjimka pro konkrétní provozní úlohu má omezený rozsah a dobu platnosti. *Ověření:* zkontroluj identity a oprávnění používaná terminálem, nástroji a připojenými službami; dostupnost produkce neposuzuj jen podle souboru s proměnnými prostředí. [Izolace vývojového agenta](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

- [ ] Agent nemůže získat nepotřebné tajné klíče alternativní cestou. Vynechání souboru z indexování nestačí, když jej může přečíst terminál nebo připojený nástroj. *Ověření:* prověř přístupové cesty přes soubory, zděděné prostředí procesů, úložiště přihlašovacích údajů a nástroje; omezení zkoušej na neškodném testovacím souboru, skutečné hodnoty klíčů nevypisuj. [Rozsah oprávnění souborových nástrojů](https://code.claude.com/docs/en/permissions), [správa tajných klíčů](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).

- [ ] Když agent používá externí skilly, pluginy nebo MCP servery: jejich původ a požadovaná oprávnění jsou zkontrolované. Mohou přidat spustitelný kód i instrukce ovlivňující další práci. *Ověření:* porovnej aktivní rozšíření se schváleným seznamem; dohledávej zdroj, používanou verzi a oprávnění a projdi změny při aktualizaci. [Bezpečnost nástrojů a MCP](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

- [ ] Postup pro práci s externím obsahem nepovažuje nalezené instrukce za nové oprávnění. Obsah issue, webu, logu nebo cizího repozitáře může obsahovat prompt injection. *Ověření:* zkontroluj pravidla pro nedůvěryhodné vstupy a na neškodném testovacím scénáři ověř, že vložený požadavek na rozšíření přístupu neobejde schvalování ani technická omezení. [Prompt injection a hranice oprávnění](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

## Větve a review

- [ ] Implementační změna vzniká v pracovní větvi oddělené od větve používané pro produkční vydání. U souběžné práce musí být oddělené i měněné pracovní soubory, například pomocí worktrees. *Ověření:* přes `git branch --show-current`, `git status --short` a případně `git worktree list` porovnej aktuální práci s postupem vydávání a souběžnými úlohami. [Práce v tematických větvích](https://git-scm.com/docs/gitworkflows).

- [ ] Před začleněním změny proběhne lidské review celého výsledného diffu. AI review může pomoci, odpovědnost za přijetí změny má konkrétní člověk. *Ověření (člověk):* vlastník nebo pověřený reviewer projde všechny změněné soubory vůči zadání a zaznamená rozhodnutí u konkrétní revize; zkontroluje i změny mimo původně očekávaný rozsah. [Review AI kódu](https://docs.github.com/en/copilot/tutorials/review-ai-generated-code).

- [ ] Když změna upravuje instrukce, skilly, oprávnění, hooky nebo CI: tato část má výslovné review. Agent si tak nemůže nenápadně oslabit pravidla pro další práci. *Ověření:* porovnej změněné soubory s pravidly review a dostupným schválením; ověř, že schválení zahrnuje aktuální podobu těchto souborů. [Ochrana instrukcí agenta](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

- [ ] Když agent maže test, vypíná kontrolu nebo oslabuje assertion: změna má doložený důvod a samostatně posouzený dopad. Zelený výsledek nesmí vzniknout odstraněním požadavku, který má stále platit. *Ověření:* projdi diff testů a konfigurace kontrol, včetně nových mocků, výjimek a ignorovaných chyb; porovnej je s akceptačními kritérii a review. [Oslabování testů](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

## Automatické kontroly a hooky

- [ ] Povinné automatické kontroly skutečně ověřují požadované vlastnosti a při porušení selžou. Typicky jde o build, kontrolu typů, lint, testy nebo bezpečnostní sken podle projektu. *Ověření:* projdi spouštěné příkazy a jejich chybové kódy; v testovací kopii vlož známou chybu a ověř selhání příslušné kontroly. [Automatické ověřování kódu](https://docs.github.com/en/copilot/tutorials/review-ai-generated-code).

- [ ] Když repozitář slouží k produkčním vydáním: povinné kontroly blokují začlenění nevyhovující změny na serveru. Lokální hook ani pokyn v instrukcích tuto ochranu nenahrazuje. *Ověření:* přes API správce repozitáře přečti ochranu cílové větve, požadované kontroly a výjimky pro účet agenta; u poslední změny ověř výsledky pro začleňovanou revizi a skutečné spuštění kontrol. Přeskočený job nemusí znamenat provedenou kontrolu. [Ochrana větví](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches), [stavy kontrol](https://docs.github.com/en/pull-requests/reference/status-checks).

- [ ] Když projekt používá hook jako ochrannou podmínku: hook prokazatelně zabrání chráněné akci před jejím provedením. Chyba nebo timeout ochranné kontroly nesmí tiše povolit pokračování. *Ověření:* ověř aktivaci, událost, filtry a chování při chybě; v testovacím prostředí vyzkoušej povolený i zakázaný případ a selhání hooku. Rozlišuj hooky agenta a Git hooky; jejich aktivace a možnosti obejití se liší. [Hooky agenta](https://code.claude.com/docs/en/hooks-guide), [Git hooky](https://git-scm.com/docs/githooks).

## Zdroje

Dokumentace nástrojů popisuje jejich konkrétní implementace. Položky výše z nich odvozují společné kontrolní cíle, nikoli jednotnou konfiguraci všech agentů.

- [OpenAI: Custom instructions with AGENTS.md](https://learn.chatgpt.com/docs/agent-configuration/agents-md) - načítání, rozsah, přednost a diagnostika instrukcí.
- [Anthropic: How Claude remembers your project](https://code.claude.com/docs/en/memory) - projektové instrukce, konflikty, importy a údržba.
- [Cursor: Rules](https://cursor.com/docs/rules) - verzovaná a podmíněně načítaná pravidla.
- [OpenAI: Custom Code Review rules for Codex](https://developers.openai.com/blog/custom-code-review-rules-for-codex) - konkrétní projektová pravidla a jejich rozsah.
- [Anthropic: Best practices for Claude Code](https://code.claude.com/docs/en/best-practices) - ověřitelné výsledky a pracovní postup.
- [GitHub Spec Kit: Agentic SDLC](https://github.com/github/spec-kit/blob/main/docs/guides/agentic-sdlc.md), [šablona specifikace](https://github.com/github/spec-kit/blob/main/templates/spec-template.md) a [Agentic SDD](https://github.github.com/spec-kit/reference/agentic-sdd.html) - přiměřená specifikace, akceptační kritéria a otevřené otázky.
- [Microsoft: Architecture decision record](https://learn.microsoft.com/en-us/azure/well-architected/architect-role/architecture-decision-record) - důvody a životní cyklus zásadních rozhodnutí.
- [OpenAI: Iterating Development Workflows with Codex](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex) - evidence, rozsah práce a opakovatelné postupy.
- [Agent Skills: Specification](https://agentskills.io/specification) a [OpenAI: Build skills](https://learn.chatgpt.com/docs/build-skills) - formát, výběr a ověřování skillů.
- [GitHub: Driving team adoption of agentic GitHub Copilot](https://docs.github.com/en/copilot/tutorials/roll-out-at-scale/enable-developers/drive-team-agentic-adoption) - dokumentované pracovní postupy a jejich vyhodnocování.
- [OWASP: AI Agent Security](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html) - nejmenší oprávnění, schvalování a nedůvěryhodné vstupy.
- [OWASP: Secure Coding with AI](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html) - produkční přístupy, rozšíření, změny instrukcí a oslabování testů.
- [OWASP: Secrets Management](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html) - omezení přístupu k tajným klíčům.
- [OpenAI: Agent approvals & security](https://learn.chatgpt.com/docs/agent-approvals-security) a [Anthropic: Configure permissions](https://code.claude.com/docs/en/permissions) - skutečný rozsah technických omezení.
- [Git: gitworkflows](https://git-scm.com/docs/gitworkflows) a [githooks](https://git-scm.com/docs/githooks) - pracovní větve a vlastnosti Git hooků.
- [GitHub: Review AI-generated code](https://docs.github.com/en/copilot/tutorials/review-ai-generated-code) - lidské review a automatické ověřování.
- [GitHub: About protected branches](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches) a [Status checks](https://docs.github.com/en/pull-requests/reference/status-checks) - vynucení kontrol před začleněním.
- [Anthropic: Automate actions with hooks](https://code.claude.com/docs/en/hooks-guide) - události, blokování a chybové stavy hooků.

---
