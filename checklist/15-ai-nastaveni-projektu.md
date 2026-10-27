# AI nastavení projektu

**Týká se:** každého projektu, ve kterém AI agent vytváří nebo mění kód, konfiguraci či dokumentaci. Platí i pro web bez AI funkcí.

Při auditu rozlišuj napsaná pravidla, skutečně načtené instrukce a technicky vynucená omezení. Aktivní zkoušky dělej v odděleném testovacím prostředí bez produkčních přístupů. Když nemáš potřebný přístup nebo bezpečné prostředí, uveď „Ověř ručně“.

Názvy souborů jsou příklady. Použij formát podporovaný konkrétním agentem a verzí. Dokumentace nástrojů a zdroje zkontrolovány k 27. 10. 2026; skutečné chování ověř v používané verzi.

## Instrukce pro agenta

- [ ] [web] Projektové instrukce jsou verzované spolu s projektem. Agent se k trvalým pravidlům dostane i v nové konverzaci a na jiném počítači. *Ověření:* najdi `AGENTS.md`, `CLAUDE.md`, pravidla editoru nebo jejich podporovaný ekvivalent a přes `git ls-files` ověř, že potřebné soubory patří do repozitáře. [Dokumentace pravidel](https://cursor.com/docs/rules).

- [ ] [web] Používaný agent skutečně načítá instrukce platné pro upravovanou část projektu. Název souboru sám nestačí; načítání může změnit nadřazená konfigurace, lokální nastavení nebo limit velikosti. *Ověření:* zjisti verzi a aktivní konfiguraci agenta; v diagnostice nebo záznamu nové relace ověř načtené soubory z kořene a při práci v relevantním podadresáři i jeho instrukce. Zohledni, zda se načítají při startu, nebo až při práci se soubory. Ruční vložení souboru do promptu není důkaz automatického načítání. [Codex](https://learn.chatgpt.com/docs/agent-configuration/agents-md), [Claude Code](https://code.claude.com/docs/en/memory).

- [ ] [web] Aktivní instrukce nemají nevyřešené rozpory pro stejnou oblast. Když sdílíš pravidla mezi více agenty, je určený jejich hlavní zdroj a způsob přenosu změn. *Ověření:* porovnej projektová, nadřazená a dostupná uživatelská pravidla; zohledni dokumentovanou přednost a rozsah instrukcí daného agenta. Zkontroluj importy, symlinky a generované kopie; záměrné výjimky a rozdíly mezi agenty musí být výslovné. [Údržba instrukcí](https://code.claude.com/docs/en/memory), [přednost instrukcí](https://learn.chatgpt.com/docs/agent-configuration/agents-md).

- [ ] [malá] Když projekt má významná omezení, která z kódu nejsou zřejmá: instrukce je uvádějí. Typicky jde o kompatibilitu veřejného API, vlastnictví dat nebo zákaz změn určité části systému. *Ověření:* porovnej instrukce s platnými rozhodnutími a významnými opravami v historii; pravidla musí říkat, kdy platí a jaký postup je přípustný. [Pravidla pro review](https://developers.openai.com/blog/custom-code-review-rules-for-codex).

- [ ] [web] Agent má dohledatelné funkční příkazy pro přípravu projektu, spuštění a jeho kontroly. Postup nesmí záviset na nevysvětleném nastavení autorova počítače. *Ověření:* porovnej dokumentované příkazy se skripty, požadovanými verzemi nástrojů a CI; v čistém testovacím prostředí ověř příkazy potřebné pro danou změnu. [Doporučení pro práci agenta](https://code.claude.com/docs/en/best-practices).

- [ ] [web] Instrukce odkazují na současné soubory a postupy. Po změně příkazů, architektury nebo způsobu nasazování je součástí změny i úprava dotčených instrukcí. *Ověření:* ověř existenci odkazovaných cest a příkazů a porovnej je s posledními souvisejícími změnami; hledej i pravidla pro již odstraněné části projektu. [Audit instrukcí](https://code.claude.com/docs/en/memory).

## Zadání a zapsaná rozhodnutí

- [ ] [web] Aktuální práce má dohledatelné zadání s cílem a hranicemi rozsahu. Pro malou opravu může stačit uložený prompt nebo issue; rozsah specifikace odpovídá dopadu a složitosti změny. *Ověření:* najdi zadání propojené s rozpracovanou změnou a ověř, že z něj lze určit řešený problém, požadovaný výsledek, koho se změna týká a co do ní nepatří. Samostatné PRD není povinné. [Specifikace podle rozsahu práce](https://github.com/github/spec-kit/blob/main/docs/guides/agentic-sdlc.md).

- [ ] [web] Požadované chování má ověřitelná akceptační kritéria. „Funguje přihlášení“ nestačí; musí být poznat očekávaný výsledek úspěšného i relevantního chybového scénáře. *Ověření:* ke každému požadavku měnícímu chování najdi vstup nebo výchozí stav, akci a pozorovatelný výsledek; neurčité výrazy musí mít rozhodovací kritérium. [Šablona specifikace](https://github.com/github/spec-kit/blob/main/templates/spec-template.md).

- [ ] [web] Nevyřešené otázky v zadání jsou označené jako otázky nebo předpoklady. Předpoklad nenahrazuje potřebné schválení změny rozsahu, přístupu k datům nebo nevratné operace. *Ověření:* projdi otevřené otázky a jejich vypořádání; u rozhodnutí vyžadujících schválení dohledávej odpověď oprávněného člověka. U ostatních předpokladů ověř, že jsou výslovné a neodporují zadání. [Vyjasnění požadavků](https://github.github.com/spec-kit/reference/agentic-sdd.html).

- [ ] [malá] Když projekt obsahuje zásadní nebo obtížně vratné rozhodnutí: jeho důvod je zapsaný mimo historii chatu, například v instrukcích, zadání nebo ADR. Agent v nové konverzaci jinak rozhodnutí snadno zvrátí. *Ověření:* najdi záznam s kontextem, rozhodnutím a důsledky; nahrazené rozhodnutí musí odkazovat na nové. Formální ADR proces není podmínkou. [Záznamy rozhodnutí](https://learn.microsoft.com/en-us/azure/well-architected/architect-role/architecture-decision-record).

## Definice „hotovo“

- [ ] [web] Projekt má zapsanou definici „hotovo“ s požadovanými důkazy. Rozlišuje kontroly podle dopadu změny, například test logiky, kontrolu rozhraní v prohlížeči nebo ověření změny dat. *Ověření:* najdi definici v instrukcích nebo odkazovaném postupu a ověř, že podle ní lze rozhodnout o dokončení konkrétní změny; samotné prohlášení agenta není důkaz. [Ověřování výsledku](https://code.claude.com/docs/en/best-practices).

- [ ] [web] Závěrečný report agenta rozlišuje provedené a neprovedené ověření. Úspěšný build nedokazuje funkční uživatelskou cestu ani správné nasazení. *Ověření:* u poslední dokončené změny porovnej report s výstupy kontrol, testovanou revizí a prostředím; přeskočené nebo zablokované kontroly musí být výslovně uvedené. [Dokládání výsledků práce](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

## Skilly a opakovatelné postupy

- [ ] [web] Když se určitá práce opakuje: agent má dostupný udržovaný postup místo závislosti na starém chatu. Může jít o psaní PRD, testování, audit nebo přípravu nasazení; samostatný skill není povinný. *Ověření:* porovnej opakované úlohy v historii projektu s dostupnými postupy; postup musí mít vymezené použití, potřebné vstupy, kroky a očekávaný výstup. [Opakovatelné pracovní postupy](https://docs.github.com/en/copilot/tutorials/roll-out-at-scale/enable-developers/drive-team-agentic-adoption).

- [ ] [web] Když projekt používá skilly: používaný agent je dokáže najít a spustit určeným způsobem. Přítomnost `SKILL.md` v libovolné složce nestačí; skill může být určený k výslovnému vyvolání nebo k automatickému výběru. *Ověření:* ověř umístění a metadata podle dokumentace dané verze a dostupnost skillu v katalogu nebo záznamu běhu. Vyzkoušej určený způsob vyvolání; pokud se spoléháš na automatický výběr, zkus odpovídající i nesouvisející zadání a zaznamenej, zda se skill načetl. [Formát Agent Skills](https://agentskills.io/specification), [použití skillů](https://learn.chatgpt.com/docs/build-skills).

- [ ] [malá] Když se projekt spoléhá na skill nebo automatizovaný postup: existuje zkouška jeho výsledku. Nestačí, že agent zavolal požadovaný nástroj. *Ověření:* na reprezentativním vstupu v testovacím prostředí porovnej vzniklý výstup s předem určeným očekáváním; po podstatné změně postupu zkoušku zopakuj. [Ověřování postupů](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

- [ ] [malá] Když agent připravuje migraci dat nebo nasazení s rizikem ztráty dat či nevratného dopadu: postup obsahuje kontrolní bod před změnou cílového prostředí. V něm je určený cíl, očekávaný dopad, ověření výsledku a způsob obnovy při selhání. *Ověření:* projdi postup a dostupný záznam zkoušky mimo produkci; u nevratných kroků musí být uvedená omezení obnovy a požadované schválení před provedením. [Řízení rizikových akcí](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

## Oprávnění a ochrana dat

- [ ] [web] Pravidla určují hranice samostatné práce agenta. Musí být jasné, které operace jsou povolené a které vyžadují výslovné schválení, zejména nevratné změny dat, publikování a změny oprávnění. *Ověření:* porovnej instrukce a nastavení schvalování; u rizikové operace musí být schválení vztažené ke konkrétní akci a cíli. [Hranice autonomie](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

- [ ] [web] Skutečná oprávnění agenta odpovídají jeho úloze. Audit sám o sobě neopravňuje měnit kontrolovaný projekt nebo připojené služby; vývojová práce nevyžaduje automaticky přístup ke všem souborům, síti a účtům. *Ověření:* porovnej rozsah úlohy s aktivním sandboxem, oprávněními nástrojů, připojenými účty a možnostmi spuštění mimo omezení. Nezaměňuj omezení terminálu za omezení MCP, aplikací nebo prohlížeče. [Sandbox a schvalování](https://learn.chatgpt.com/docs/agent-approvals-security).

- [ ] [malá] Když projekt má produkční prostředí: běžné vývojové prostředí agenta nemá produkční přístupy. Zákaz v promptu omezení přístupu nenahrazuje a výjimka pro konkrétní provozní úlohu má omezený rozsah a dobu platnosti. *Ověření:* zkontroluj identity a oprávnění používaná terminálem, nástroji včetně databázových a připojenými službami; dostupnost produkce neposuzuj jen podle souboru s proměnnými prostředí. [Izolace vývojového agenta](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

- [ ] [web] Agent nemůže získat nepotřebné tajné klíče alternativní cestou. Vynechání souboru z indexování nestačí, když jej může přečíst terminál nebo připojený nástroj. *Ověření:* prověř přístupové cesty přes soubory, zděděné prostředí procesů, úložiště přihlašovacích údajů a nástroje; omezení zkoušej na neškodném testovacím souboru, skutečné hodnoty klíčů nevypisuj. [Rozsah oprávnění souborových nástrojů](https://code.claude.com/docs/en/permissions), [správa tajných klíčů](https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html).

- [ ] [web] Když agent používá externí skilly, pluginy nebo MCP servery: jejich původ a požadovaná oprávnění jsou zkontrolované. Mohou přidat spustitelný kód i instrukce ovlivňující další práci. *Ověření:* u aktivních rozšíření dohledávej zdroj, používanou verzi a oprávnění; ověř, že jejich použití a přístupy schválil vlastník nebo pověřený správce. Při aktualizaci projdi změny kódu, instrukcí a oprávnění podle dopadu rozšíření. [Bezpečnost nástrojů a MCP](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

- [ ] [web] Postup pro práci s externím obsahem nepovažuje nalezené instrukce za nové oprávnění. Obsah issue, webu, logu nebo cizího repozitáře může obsahovat prompt injection. *Ověření:* zkontroluj pravidla pro nedůvěryhodné vstupy a na neškodném testovacím scénáři ověř, že vložený požadavek na rozšíření přístupu neobejde schvalování ani technická omezení. [Prompt injection a hranice oprávnění](https://cheatsheetseries.owasp.org/cheatsheets/AI_Agent_Security_Cheat_Sheet.html).

## Větve a review

- [ ] [web] Neověřená implementační změna se nedostane automaticky do produkce. Pracovní větev je jedna možnost; přípustná je i práce v hlavní větvi s kontrolami před vydáním. *Ověření:* přes `git branch --show-current`, `git status --short` a konfiguraci vydávání ověř, kdy se změna může dostat do produkce a jaké kontroly tomu předcházejí. U souběžných nezávislých úloh ověř oddělení pracovních souborů, například přes `git worktree list`, nebo doloženou koordinaci společných změn. [Práce v tematických větvích](https://git-scm.com/docs/gitworkflows), [vývoj v hlavní větvi](https://dora.dev/capabilities/trunk-based-development/).

- [ ] [malá] Před začleněním nebo vydáním změny proběhne lidské review celého výsledného diffu. AI review může pomoci, odpovědnost za přijetí změny má konkrétní člověk. *Ověření (člověk):* vlastník nebo pověřený reviewer projde všechny změněné soubory vůči zadání a zaznamená rozhodnutí u konkrétní revize; zkontroluje i změny konfigurace, závislostí a testů a změny mimo původně očekávaný rozsah. Review může proběhnout i průběžně při společné práci, musí ale pokrýt konečnou podobu změny. [Review AI kódu](https://docs.github.com/en/copilot/tutorials/review-ai-generated-code), [průběžné review](https://dora.dev/capabilities/trunk-based-development/).

- [ ] [web] Když změna upravuje instrukce, skilly, oprávnění, hooky nebo CI: tato část má výslovné lidské review. Agent si tak nemůže nenápadně oslabit pravidla pro další práci. *Ověření (člověk):* vlastník nebo pověřený reviewer porovná změny s původními pravidly a schválí jejich konkrétní výslednou podobu. Zkontroluje zejména rozšíření přístupů, odstranění kontrol a změny schvalování; obecné schválení zadání nestačí. [Ochrana instrukcí agenta](https://cheatsheetseries.owasp.org/cheatsheets/Secure_Coding_with_AI_Cheat_Sheet.html).

## Automatické kontroly a hooky

- [ ] [malá] Povinné automatické kontroly skutečně ověřují požadované vlastnosti a při porušení selžou. Typicky jde o build, kontrolu typů, lint, testy nebo bezpečnostní sken podle projektu. *Ověření:* projdi spouštěné příkazy, kontrolované podmínky a přenos chybových kódů do výsledku celé kontroly. U nových, změněných nebo jinak nedoložených kontrol v testovací kopii vlož známou chybu a ověř selhání příslušné kontroly. [Automatické ověřování kódu](https://docs.github.com/en/copilot/tutorials/review-ai-generated-code), [dokládání kontrol](https://developers.openai.com/cookbook/examples/codex/iterating-development-workflows-with-codex).

- [ ] [velká] Když repozitář slouží k produkčním vydáním: povinné kontroly jsou vynucené na serveru před začleněním nebo vydáním změny do produkce. Lokální hook ani pokyn v instrukcích tuto ochranu nenahrazuje. *Ověření:* přes API správce repozitáře nebo systému vydávání přečti ochranu cílové větve či podmínky vydání, požadované kontroly a výjimky pro účet agenta. U poslední změny ověř výsledky pro vydávanou revizi a skutečné spuštění kontrol; přeskočený job nemusí znamenat provedenou kontrolu. [Ochrana větví](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches), [stavy kontrol](https://docs.github.com/en/pull-requests/reference/status-checks), [vývoj v hlavní větvi](https://dora.dev/capabilities/trunk-based-development/).

- [ ] [malá] Když projekt používá hook jako ochrannou podmínku: chráněná akce zůstane zablokovaná i při chybě nebo timeoutu této kontroly. Pokud to hook nezaručuje, musí ochranu vynucovat další nezávislé omezení. *Ověření:* ověř aktivaci, událost, filtry a chování při chybě; v testovacím prostředí vyzkoušej povolený i zakázaný případ a selhání hooku. Zkontroluj možnosti obejití i změny hooku agentem; hook spuštěný až po akci jí nezabrání a obejitelný lokální hook není samostatná bezpečnostní hranice. [Hooky agenta](https://code.claude.com/docs/en/hooks-guide), [Git hooky](https://git-scm.com/docs/githooks).

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
- [DORA: Trunk-based development](https://dora.dev/capabilities/trunk-based-development/) - přípustnost práce v hlavní větvi, malé změny, automatické kontroly a průběžné review.
