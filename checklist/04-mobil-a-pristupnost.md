# Mobil a přístupnost

**Týká se:** každého webu a webové aplikace.

Čísla u položek odkazují na kritéria WCAG 2.2. Úroveň AA zahrnuje také požadavky úrovně A. Doporučení nad rámec AA jsou oddělená. Tento soubor vybírá časté bariéry; jeho splnění samo neprokazuje úplnou shodu s WCAG 2.2 AA. Ta vyžaduje splnění všech použitelných kritérií A a AA na celých stránkách a v celých procesech. [WCAG 2.2, požadavky na shodu](https://www.w3.org/TR/WCAG22/#conformance-reqs).

Kontroluj jednotlivé šablony stránek a hlavní uživatelské procesy. Zahrň mobilní navigaci, otevřené dialogy, chybové stavy a všechny nabízené barevné režimy. U nálezu ulož URL, stav stránky, dotčený prvek a důkaz. Nedostupné ověření označ „Ověř ručně“.

## Mobil, zvětšení a rozložení

- [ ] Web neblokuje zvětšení obsahu. Zákaz zoomu zhoršuje čitelnost lidem se slabším zrakem. [WCAG 1.4.4 AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html). *Ověření:* zkontroluj viewport a obsluhu dotykových událostí; hledej zejména `user-scalable=no`, omezující `maximum-scale` a blokování gesta pro přiblížení.

- [ ] Při šířce 320 CSS px se běžný obsah přeskupí bez ztráty informací a funkcí a bez nutnosti rolovat ve dvou směrech. Výjimka platí pro části vyžadující dvourozměrné rozložení, například mapy a datové tabulky, ne automaticky pro celou stránku. [WCAG 1.4.10 AA](https://www.w3.org/WAI/WCAG22/Understanding/reflow.html). *Ověření (prohlížeč):* projdi stránku při šířce 320 CSS px a při 400% zoomu z výchozího viewportu širokého 1280 CSS px; zkontroluj také otevřené menu a dialogy. Samotné `overflow-x: hidden` není důkaz splnění.

- [ ] Text lze zvětšit na 200 % bez ztráty obsahu a funkcí. Požadavek se vztahuje i na text tlačítek a popisků; výjimkou jsou titulky a obrázky textu. [WCAG 1.4.4 AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html). *Ověření (prohlížeč):* zvětšuj obsah postupně až na 200 % a ověř ořezávání, překrývání a dostupnost ovládání.

- [ ] Obsah zůstane použitelný po uživatelské změně rozestupů textu. Testovací hodnoty jsou výška řádku 1,5násobku velikosti písma, mezera za odstavcem 2násobku, rozestup písmen 0,12násobku a slov 0,16násobku; nejsou to povinné výchozí styly. [WCAG 1.4.12 AA](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing.html). *Ověření (prohlížeč):* aplikuj všechny čtyři hodnoty současně uživatelským stylesheetem nebo bookmarkletem; zkontroluj text, menu, tlačítka a dialogy.

- [ ] Web nevyžaduje konkrétní orientaci displeje, pokud není pro danou funkci nezbytná. Telefon může být upevněný a uživatel ho nemusí umět otočit. [WCAG 1.3.4 AA](https://www.w3.org/WAI/WCAG22/Understanding/orientation.html). *Ověření (prohlížeč):* projdi hlavní procesy na výšku i na šířku; zkontroluj také kód vynucující orientaci a překryvy typu „otoč telefon“.

- [ ] Když web obsahuje vstupní pole: hlavní úlohu lze na podporovaném telefonu dokončit i s otevřenou softwarovou klávesnicí. Jde o praktickou kontrolu mobilního použití, kterou emulace zařízení plně nenahradí. [Omezení mobilní emulace](https://developer.chrome.com/docs/devtools/device-mode#limitations). *Ověření (člověk):* na reálném telefonu vyplň formulář včetně posledního pole a dokonči ho; ověř dostupnost potřebných tlačítek a zaznamenej zařízení a prohlížeč.

## Dotykové cíle a gesta

- [ ] Cíle ovládané ukazatelem mají alespoň 24 × 24 CSS px nebo splňují konkrétní výjimku. Výjimky jsou dostatečné rozestupy, vyhovující alternativní ovládání na stejné stránce, odkazy uvnitř vět či omezené řádkováním okolního textu, neupravené ovládání prohlížeče a nezbytná či právně vyžadovaná velikost. [WCAG 2.5.8 AA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html). *Ověření (prohlížeč):* změř skutečné aktivní plochy, nejen ikony. U menších cílů ověř, že kruh o průměru 24 CSS px se středem v jejich bounding boxu neprotíná jiný cíl ani obdobný kruh sousedního malého cíle; jinou použitou výjimku dolož.

- [ ] Když vlastní ovládání používá vícedotykové gesto nebo gesto po určité dráze: stejnou funkci lze provést jedním ukazatelem bez takového gesta, pokud není nezbytné. Typický problém je carousel ovládaný pouze swipem. [WCAG 2.5.1 A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures.html). *Ověření (prohlížeč):* vyzkoušej alternativní tlačítka nebo jiné jednoduché ovládání; nezaměňuj vlastní gesta webu s gesty prohlížeče.

- [ ] Když funkce vyžaduje přetahování: existuje alternativa jedním ukazatelem bez přetahování, pokud není tah nezbytný nebo nejde o neupravené ovládání prohlížeče. Samotná alternativa klávesnicí tento požadavek neplní. [WCAG 2.5.7 AA](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements.html). *Ověření (prohlížeč):* změň pořadí položek, hodnotu slideru nebo umístění objektu pomocí kliknutí či klepnutí bez držení a tažení.

- [ ] Akce ukazatelem splňují pravidla zrušení nechtěného stisku. Běžné řešení spouští akci až při uvolnění; jiné řešení musí splnit některou z alternativ kritéria. [WCAG 2.5.2 A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-cancellation.html). *Ověření (prohlížeč):* stiskni běžné tlačítko, přesuň ukazatel mimo něj a uvolni; akce se nemá provést. U obsluhy `pointerdown`, `mousedown` a `touchstart` ověř případné vrácení účinku nebo doloženou nezbytnost.

## Kontrast a barvy

- [ ] Text má kontrast alespoň 4,5:1; velký text alespoň 3:1. Velký text je alespoň 18 pt, tedy 24 CSS px, nebo tučný alespoň 14 pt, přibližně 18,67 CSS px; platí výjimky pro logotypy, neaktivní prvky a další případy uvedené v kritériu. [WCAG 1.4.3 AA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html). *Ověření (prohlížeč):* kontrast vypočítej z výsledných barev včetně průhlednosti; zkontroluj placeholdery, chybové texty, nabízené motivy a nejméně kontrastní pozadí pod textem přes fotografii či gradient. Výsledek nezaokrouhluj nahoru.

- [ ] Vizuální informace potřebné k rozpoznání ovládacích prvků, jejich stavů a významových částí grafiky mají kontrast alespoň 3:1 vůči sousedním barvám. Ne každý dekorativní rámeček musí tento práh splnit; výjimku mají také neaktivní prvky a neupravený vzhled ovládání prohlížeče. [WCAG 1.4.11 AA](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html). *Ověření (prohlížeč):* přeměř potřebné hranice polí, významové ikony, značky výběru a vlastní indikátory fokusu v relevantních stavech.

- [ ] Barva není jediný prostředek předání informace. Chyba, dostupnost, vybraná položka nebo význam dat musí být rozpoznatelné i jinak. [WCAG 1.4.1 A](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html). *Ověření (prohlížeč):* zkontroluj chybové a vybrané stavy, legendy grafů a odkazy v textu; ověř další rozlišení textem, tvarem, vzorem či jiným odpovídajícím znakem.

## Obrázky, struktura a jazyk

- [ ] Když netextový obsah předává informaci: má textovou alternativu se stejným účelem. U funkčního obrázku alternativa vyjadřuje akci či cíl; složitý graf potřebuje dostupné vysvětlení podstatných informací, ne pouze název. [WCAG 1.1.1 A](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html). *Ověření (člověk):* porovnej obrázky, SVG, canvas a významová pozadí s jejich dostupnými alternativami; zkontroluj zachování informace a účelu v kontextu stránky.

- [ ] Když je grafika čistě dekorativní: asistivní technologie ji mohou ignorovat. Zbytečné popisky zahlcují čtení stránky. [WCAG 1.1.1 A](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content.html). *Ověření:* u dekorativních `<img>` ověř `alt=""`; u ostatních způsobů vložení ověř odpovídající skrytí před asistivní technologií. Neschovávej tím významový obsah ani ovládací prvek.

- [ ] Běžný text není nahrazen obrázkem textu, pokud lze stejné prezentace dosáhnout skutečným textem. Výjimkou je nezbytná prezentace, například logo, nebo uživatelsky přizpůsobitelný obrázek textu. [WCAG 1.4.5 AA](https://www.w3.org/WAI/WCAG22/Understanding/images-of-text.html). *Ověření:* porovnej texty v obrázcích a exportovaných SVG s obsahem dokumentu; hledej zejména nadpisy, nabídky a tlačítka uložená jako grafika.

- [ ] Nadpisy v kódu vyjadřují skutečnou hierarchii obsahu. Vizuálně výrazný odstavec nenahrazuje sémantický nadpis a úroveň nadpisu se nevolí podle velikosti písma. [WCAG 1.3.1 A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html), [WAI: nadpisy](https://www.w3.org/WAI/tutorials/page-structure/headings/). *Ověření:* vypiš nadpisy a jejich úrovně z výsledného dokumentu a porovnej je s členěním stránky; návrat například z `h4` na `h2` při ukončení podsekce není chyba.

- [ ] Když obsah tvoří seznam: jeho struktura je dostupná i programově. Ručně vložené odrážky v samostatných blocích vztah položek nezaručují. [WCAG 1.3.1 A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html). *Ověření:* zkontroluj sémantiku seznamů ve výsledném dokumentu, včetně seznamů generovaných komponentami.

- [ ] Když stránka obsahuje datovou tabulku: vztahy buněk a jejich záhlaví jsou programově určitelné. Samotné tučné písmo v prvním řádku nestačí. [WCAG 1.3.1 A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships.html). *Ověření:* zkontroluj záhlaví a jejich vazby na datové buňky; u složitých tabulek ověř přiřazení víceúrovňových záhlaví.

- [ ] Pořadí obsahu v dokumentu zachovává význam. Vizuální přeskládání pomocí CSS nesmí vytvořit nesrozumitelné pořadí pro čtečku. [WCAG 1.3.2 A](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence.html). *Ověření (prohlížeč):* porovnej pořadí v DOMu a accessibility tree s obsahem na mobilu i desktopu; kontroluj zejména kroky návodu a přiřazení popisků.

- [ ] Výchozí jazyk stránky je správně programově určený. Čtečka podle něj může zvolit výslovnost. [WCAG 3.1.1 A](https://www.w3.org/WAI/WCAG22/Understanding/language-of-page.html). *Ověření:* zkontroluj platný atribut `lang` kořenového dokumentu a jeho shodu s jazykem každé lokalizované varianty.

- [ ] Když část obsahu používá jiný jazyk: změna je programově označená. Výjimkou jsou vlastní jména, technické termíny, neurčitelný jazyk a výrazy převzaté do okolního jazyka. [WCAG 3.1.2 AA](https://www.w3.org/WAI/WCAG22/Understanding/language-of-parts.html). *Ověření:* porovnej cizojazyčné pasáže s atributy `lang`; nevyžaduj označení každého anglického technického termínu.

- [ ] Účel odkazu je určitelný z jeho textu nebo programově dostupného kontextu. Vizuálně blízký nadpis nemusí být dostatečně přiřazený. [WCAG 2.4.4 A](https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context.html). *Ověření:* vypiš odkazy s jejich dostupnými názvy a kontextem; prověř opakované názvy jako „Více“ nebo „Zde“ vedoucí na různé cíle.

## Ovládací prvky a čtečky obrazovky

- [ ] Každý ovládací prvek má programově dostupný název popisující jeho účel. Platí to i pro samostatné ikony a tlačítka pro zavření. [WCAG 4.1.2 A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html). *Ověření (prohlížeč):* spusť axe a zkontroluj vypočtené názvy v accessibility tree; samotná přítomnost atributu `aria-label` není důkaz správného výsledku.

- [ ] Role ovládacího prvku odpovídá jeho funkci. Pro běžné akce preferuj nativní tlačítko a pro navigaci odkaz s cílem; vlastní implementace musí poskytovat odpovídající sémantiku i chování. [WCAG 4.1.2 A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html), [WAI APG: role je závazek](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/). *Ověření:* projdi vlastní klikací prvky a porovnej jejich funkci, výslednou roli a obsluhu klávesnice; samotné `role="button"` klávesnicové ovládání nepřidává.

- [ ] Když prvek mění stav nebo hodnotu: změna je dostupná asistivním technologiím. Typicky jde o rozbalené menu, zaškrtnutí, vybranou záložku nebo hodnotu slideru. [WCAG 4.1.2 A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value.html). *Ověření (prohlížeč):* měň stav prvku a sleduj odpovídající vlastnosti v accessibility tree; nestačí neměnný atribut přidaný při načtení.

- [ ] Když má ovládací prvek viditelný textový popisek: jeho dostupný název tento text obsahuje. Jinak může selhat hlasové ovládání podle viditelného názvu. [WCAG 2.5.3 A](https://www.w3.org/WAI/WCAG22/Understanding/label-in-name.html). *Ověření (prohlížeč):* porovnej viditelný text s vypočteným accessible name; prověř zejména přepisování názvu pomocí ARIA.

- [ ] Když se bez přesunu fokusu objeví stavová zpráva: je programově rozpoznatelná tak, aby ji čtečka mohla oznámit. Týká se například výsledku akce, čekání nebo počtu nalezených výsledků. [WCAG 4.1.3 AA](https://www.w3.org/WAI/WCAG22/Understanding/status-messages.html). *Ověření (prohlížeč):* vyvolej zprávu a zkontroluj odpovídající živou oblast či roli a její aktualizaci; nepřidávej oznamování celé měnící se stránky.

## Klávesnice a fokus

- [ ] Všechny funkce mají ovládání klávesnicí bez požadavku na přesné načasování stisků. Výjimkou jsou funkce, jejichž podstata závisí na dráze pohybu, například volné kreslení. [WCAG 2.1.1 A](https://www.w3.org/WAI/WCAG22/Understanding/keyboard.html). *Ověření (prohlížeč):* dokonči hlavní procesy bez myši; používej Tab, Shift+Tab a klávesy odpovídající typu prvku, včetně šipek u složených komponent. Kontroluj skutečný výsledek akce.

- [ ] Z každé komponenty lze odejít klávesnicí. Nestandardní způsob odchodu musí být předem vysvětlený. [WCAG 2.1.2 A](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap.html). *Ověření (prohlížeč):* vstup do menu, editorů a vložených komponent a znovu je opusť; modální dialog není past, pokud ho lze klávesnicí zavřít.

- [ ] Pořadí fokusu zachovává význam a ovladatelnost. Nemusí přesně kopírovat vizuální souřadnice, ale nesmí rozbíjet návaznost úlohy. [WCAG 2.4.3 A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html). *Ověření (prohlížeč):* zaznamenej průchod Tabem a Shift+Tabem na mobilním i desktopovém rozložení; prověř vlastní přesuny fokusu a kladné hodnoty `tabindex`.

- [ ] Fokus klávesnice je viditelný po celou dobu, kdy ho prvek má. Vypnutí výchozího outline vyžaduje funkční náhradu. [WCAG 2.4.7 AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html). *Ověření (prohlížeč):* projdi všechny typy ovládání klávesnicí a ověř, že indikátor nezmizí po animaci ani v jiném barevném režimu.

- [ ] Prvek přijímající fokus není úplně zakrytý obsahem vytvořeným webem. Minimum AA připouští částečné zakrytí; úplná viditelnost je lepší výsledek, ale přísnější požadavek. [WCAG 2.4.11 AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html). *Ověření (prohlížeč):* projdi stránku s přilepenou hlavičkou, cookie lištou a chatem také při zvětšení. U obsahu otevřeného uživatelem ověř možnost odkrýt prvek bez posunu fokusu.

- [ ] Když se na více stránkách opakují bloky obsahu: existuje mechanismus jejich přeskočení. Praktické řešení je odkaz „Přeskočit na obsah“, dostupný na začátku průchodu klávesnicí. [WCAG 2.4.1 A](https://www.w3.org/WAI/WCAG22/Understanding/bypass-blocks.html). *Ověření (prohlížeč):* mechanismus aktivuj; u skip odkazu ověř viditelnost při fokusu a pokračování klávesnicové navigace v cílové části, ne pouze posunutí obrazu.

- [ ] Samotné získání fokusu nevyvolává změnu kontextu. Tabování nesmí samo odeslat formulář, otevřít nové okno nebo přesunout fokus jinam. [WCAG 3.2.1 A](https://www.w3.org/WAI/WCAG22/Understanding/on-focus.html). *Ověření (prohlížeč):* projdi ovládání bez aktivace a sleduj navigaci, odesílání a přesuny fokusu.

- [ ] Když web používá zkratky tvořené pouze tisknutelnými znaky: lze je vypnout, přemapovat s netisknutelnou klávesou nebo fungují jen při fokusu příslušné komponenty. Týká se i sekvencí znaků. [WCAG 2.1.4 A](https://www.w3.org/WAI/WCAG22/Understanding/character-key-shortcuts.html). *Ověření:* zkontroluj obsluhu klávesových událostí a podmínky aktivace; ověř dostupnost alespoň jedné uvedené možnosti.

## Menu, dialogy a dočasný obsah

- [ ] Když je menu nebo panel zavřený: jeho nedostupné ovládání nezůstává v pořadí fokusu. Pouhé odsunutí mimo obrazovku ho z navigace nevyřadí. [WCAG 2.4.3 A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order.html). *Ověření (prohlížeč):* zavři panel a projdi okolí Tabem v obou směrech; zkontroluj také stav po změně breakpointu.

- [ ] Když je otevřený modální dialog: fokus se přesune dovnitř a průchod Tabem zůstává v dialogu. Obsah pod skutečně modálním dialogem není dostupný k ovládání. Jde o doporučený vzor WAI APG. [WAI APG: modální dialog](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/). *Ověření (prohlížeč):* otevři dialog klávesnicí a projdi ho Tabem i Shift+Tabem; ověř vhodný počáteční fokus a neaktivní pozadí.

- [ ] Když je otevřený modální dialog: lze ho zavřít klávesnicí; doporučený vzor používá Escape. Tlačítko zavření musí mít dostupný název. [WAI APG: modální dialog](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/). *Ověření (prohlížeč):* vyzkoušej Escape a aktivaci ovládání pro zavření bez myši.

- [ ] Když se modální dialog zavře: fokus se vrátí na vyvolávající prvek nebo na logické pokračování úlohy. Nesmí se ztratit v odstraněném obsahu. [WAI APG: modální dialog](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/). *Ověření (prohlížeč):* zavři dialog všemi dostupnými způsoby a ověř následný fokus; zohledni odstranění vyvolávajícího prvku.

- [ ] Když hover nebo fokus zobrazí další obsah zakrývající či nahrazující původní obsah: lze ho zavřít bez přesunu ukazatele nebo fokusu. Výjimkou je hlášení vstupní chyby a neupravené chování prohlížeče. [WCAG 1.4.13 AA](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html). *Ověření (prohlížeč):* otevři vlastní tooltip či submenu a zkus ho zavřít například Escapem při zachování ukazatele a fokusu.

- [ ] Když hover zobrazí další obsah: lze na tento obsah přesunout ukazatel, aniž zmizí. To umožňuje přečíst větší tooltip nebo použít jeho ovládání. [WCAG 1.4.13 AA](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html). *Ověření (prohlížeč):* přejeď ze spouštěče na zobrazený obsah včetně případné mezery mezi nimi.

- [ ] Když hover nebo fokus zobrazí další obsah: obsah nezmizí pouze kvůli uplynutí času. Zůstává do odstranění hoveru či fokusu, zavření uživatelem nebo zneplatnění informace; výjimkou je neupravené chování prohlížeče. [WCAG 1.4.13 AA](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html). *Ověření (prohlížeč):* ponech hover či fokus aktivní a ověř časovače skrývání.

## Pohyb, aktualizace a zvuk

- [ ] Když se pohybující, blikající nebo posouvající obsah spustí automaticky, trvá déle než 5 sekund a běží souběžně s jiným obsahem: lze ho pozastavit, zastavit nebo skrýt, pokud není nezbytný. [WCAG 2.2.2 A](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html). *Ověření (prohlížeč):* zkontroluj carousel, běžící text a další animovaný obsah; ověř, že ovládání funguje i klávesnicí.

- [ ] Když se informace automaticky aktualizují souběžně s jiným obsahem: lze aktualizace pozastavit, zastavit, skrýt nebo nastavit jejich frekvenci, pokud nejsou nezbytné. Pro tuto část kritéria neplatí výjimka do 5 sekund. [WCAG 2.2.2 A](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html). *Ověření (prohlížeč):* prověř automaticky měněné zprávy a výsledky a vyzkoušej dostupné ovládání aktualizací.

- [ ] Obsah neobsahuje více než 3 záblesky v libovolném intervalu jedné sekundy, pokud není prokázané splnění prahů obecného a červeného záblesku. Pouhé upozornění před blikáním požadavek nenahrazuje. [WCAG 2.3.1 A](https://www.w3.org/WAI/WCAG22/Understanding/three-flashes-or-below-threshold.html). *Ověření:* zkontroluj animace a média; při podezření analyzuj záznam podle definice prahů. Bez doloženého měření výjimku neuznávej.

- [ ] Když se zvuk spustí automaticky na déle než 3 sekundy: lze ho pozastavit, zastavit nebo ovládat jeho hlasitost nezávisle na systémové hlasitosti. Automatický zvuk může překrýt hlas čtečky. [WCAG 1.4.2 A](https://www.w3.org/WAI/WCAG22/Understanding/audio-control.html). *Ověření (prohlížeč):* otevři stránku v novém kontextu a prověř vlastní i vložené přehrávače; ověř dostupné ovládání.

## Doporučení nad rámec AA

Následující položky vyhodnocuj odděleně od požadavků AA.

- [ ] Když web používá pohybové animace vyvolané interakcí: nezbytné animace jsou odlišeny a ostatní lze vypnout, například respektováním `prefers-reduced-motion: reduce`. Kritérium pro vypnutí těchto animací je úrovně AAA; konkrétní media query je jedna z technik. [WCAG 2.3.3 AAA](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html), [technika C39](https://www.w3.org/WAI/WCAG22/Techniques/css/C39). *Ověření (prohlížeč):* zapni omezení pohybu a vyzkoušej scroll, navigaci a otevírání komponent; ověř také animace řízené skriptem a dostupnost obsahu po jejich vypnutí.

- [ ] Hlavní dotykové ovládání má jako doporučený cíl alespoň 44 × 44 CSS px. Jde o přísnější velikost odvozenou z AAA, nikoli o minimum AA. [WCAG 2.5.5 AAA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html). *Ověření (prohlížeč):* změř aktivní plochy hlavních akcí a často používaných ikon; menší vyhovující cíl neoznačuj za porušení AA.

## Jak kontrolovat s agentem

- [ ] Automatická kontrola nezanechala nevyřešené potvrzené nálezy použitelných kritérií A a AA. Kontrola musí zahrnout i obsah zobrazený až po interakci. [Dokumentace axe](https://www.deque.com/axe/core-documentation/), [testování přístupnosti v Playwright](https://playwright.dev/docs/accessibility-testing). *Ověření:* spusť axe přes API nebo automatizovaný prohlížeč v relevantních stavech; ulož verzi nástroje, nastavení, `violations`, URL a selektory. Nálezy označené jen jako best practice posuzuj odděleně.

- [ ] Nejednoznačné výsledky automatické kontroly mají samostatné vyhodnocení. `incomplete` ani „needs review“ neznamená splnění nebo potvrzenou chybu. [Dokumentace výsledků axe](https://www.deque.com/de/axe/core-documentation/api-documentation/). *Ověření:* projdi tyto výsledky a u každého dolož rozhodnutí nebo napiš konkrétní úlohu do „Ověř ručně“.

- [ ] Hlavní uživatelské úlohy lze dokončit pomocí skutečné čtečky obrazovky. Accessibility tree ani vysoké automatické skóre tento výsledek neprokazují. [WAI APG: podpora prohlížečů a asistivních technologií](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/). *Ověření (člověk):* ve zvolené relevantní kombinaci čtečky a prohlížeče najdi hlavní obsah, použij navigaci, otevři a zavři dialog a dokonči hlavní úlohu včetně chybového a úspěšného stavu; zaznamenej kombinaci a konkrétní bariéry. Pro mobilní publikum zahrň mobilní čtečku.

## Zdroje

- [WCAG 2.2](https://www.w3.org/TR/WCAG22/) - normativní požadavky, úrovně a pravidla shody; konkrétní kritéria jsou propojená přímo u položek.
- [Understanding WCAG 2.2](https://www.w3.org/WAI/WCAG22/Understanding/) - výklad kritérií, výjimky a testovací souvislosti.
- [WAI: struktura stránky a nadpisy](https://www.w3.org/WAI/tutorials/page-structure/headings/).
- [WAI ARIA APG: zásady použití a omezení podpory](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/).
- [WAI ARIA APG: modální dialog](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/).
- [W3C: technika C39 pro omezení pohybu](https://www.w3.org/WAI/WCAG22/Techniques/css/C39).
- [axe-core](https://github.com/dequelabs/axe-core), [dokumentace API](https://www.deque.com/de/axe/core-documentation/api-documentation/).
- [Playwright: testování přístupnosti](https://playwright.dev/docs/accessibility-testing).
- [Chrome DevTools: mobilní emulace a její omezení](https://developer.chrome.com/docs/devtools/device-mode).
