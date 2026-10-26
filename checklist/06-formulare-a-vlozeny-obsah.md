# Formuláře a vložený obsah

**Týká se:** webu s formulářem nebo vloženým obsahem z jiné služby (mapa, video, kalendář, rezervace).

## Formulář

- [ ] Formulář má co nejmíň polí. Každé pole navíc snižuje počet odeslání. Pro projevení zájmu stačí dvě pole, zbytek se doptáš v odpovědi.
- [ ] Každé pole má viditelný popisek. Šedý text uvnitř pole není popisek, po kliknutí zmizí.
- [ ] Pole na e-mail a telefon jsou tak označená, že na mobilu vyskočí správná klávesnice a prohlížeč umí údaje doplnit.
- [ ] Chybové hlášky jsou konkrétní a u pole, ke kterému patří.
- [ ] Je vidět stav: odesílám, odesláno, chyba. Bez toho lidé klikají třikrát.
- [ ] Po odeslání následuje konkrétní další krok, ne obecné „Děkujeme".

## Formulář, který tiše nefunguje

- [ ] Formulář hlásí úspěch, jen když data opravdu dorazila. Agent rád ukáže „Odesláno", i když nic neodešlo.
- [ ] Při chybě se ukáže hláška a náhradní kontakt (e-mail, telefon).
- [ ] Ověřeno odesláním s vypnutým internetem: musí se ukázat chyba, ne úspěch.
- [ ] Ověřeno odesláním z živého webu jako cizí člověk až po doručenou zprávu.

## Kam formulář posílá data

- [ ] Formulář neposílá data z prohlížeče rovnou do cizí služby s přístupovým klíčem nebo adresou webhooku v kódu. Kdokoli si je ze stránky přečte a zneužije. Data jdou přes vlastní server nebo přes formulářovou službu.

## Spam

- [ ] Formulář má ochranu proti spamu, která nesleduje návštěvníky: skryté pole, které vyplní jen bot, a kontrolu, že formulář nebyl odeslán hned po načtení.
- [ ] Ochrana proti botům nepřidává sledovací cookies. Některé CAPTCHA služby je mají a kvůli nim pak potřebuješ cookie lištu.

## Vložený obsah

- [ ] Vložený obsah má popisek pro čtečky, načítá se až při rolování a má pevnou výšku, ať stránka neposkočí.
- [ ] Na mobilu má vložený obsah plnou šířku a nevzniká v něm vodorovné rolování.
- [ ] Vedle vloženého obsahu je přímá alternativa: odkaz „otevřít v novém okně", adresa textem vedle mapy. Pro případ, že se obsah nenačte.
- [ ] Vložený obsah je otestovaný na iPhonu. Safari blokuje cookies z cizích webů a vložené služby se tam chovají jinak.
- [ ] Vložený obsah je vyzkoušený naostro včetně celého řetězce, třeba rezervace až po potvrzovací e-mail.
