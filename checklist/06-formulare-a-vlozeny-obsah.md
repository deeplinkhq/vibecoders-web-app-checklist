# Formuláře a vložený obsah

**Týká se:** webu s formulářem nebo vloženým obsahem třetí strany (mapa, video, kalendář, rezervace).

## Formulář

- [ ] Formulář má co nejmíň polí. Orientačně: 1 pole 13,4 % konverze, 3 pole 10,1 %, 5 polí 7,8 %, 9 polí 3,6 %. Pro zájem stačí dvě pole, zbytek se doptáš v odpovědi.
- [ ] Každé pole má viditelný `<label for="…">`. Placeholder není popisek. Chybí na 48 % domovských stránek.
- [ ] Pole mají správný `type` (`email`, `tel`) a `autocomplete`, na mobilu pak vyskočí správná klávesnice.
- [ ] Chybové hlášky jsou textové, konkrétní, u pole a navázané přes `aria-describedby`.
- [ ] Je vidět stav: odesílám, odesláno, chyba. Bez toho lidé klikají třikrát. Potvrzení má `role="status"`, ať ho přečte i čtečka.
- [ ] Po odeslání následuje konkrétní další krok, ne obecné „Děkujeme".

## Formulář, který tiše nefunguje

- [ ] Kód kontroluje odpověď serveru (`if (!res.ok)`), nemá prázdný `catch` ani `mode: "no-cors"`. Agent rád ukáže „Odesláno", i když nic neodešlo.
- [ ] Při chybě se ukáže hláška a náhradní kontakt (e-mail, telefon).
- [ ] Ověřeno odesláním s vypnutou sítí: musí se ukázat chyba, ne úspěch.
- [ ] Ověřeno odesláním z živého webu jako cizí člověk až po doručenou zprávu.

## Kam formulář posílá data

- [ ] Formulář neposílá data přímo z prohlížeče na webhook (Discord, Slack, Make, n8n). Adresa webhooku je přístupový klíč bez hesla a kdokoli ji může zneužít. Podrobnosti v [Bezpečnosti](08-bezpecnost.md).
- [ ] Data jdou přes serverovou funkci (klíč v proměnné prostředí, kontrola `Origin`, limit počtu odeslání), nebo přes formulářovou službu (Web3Forms 250 odeslání měsíčně zdarma, Formspree 50, stav 8/2026).

## Spam

- [ ] Formulář má ochranu bez sledování: skryté pole (honeypot) a kontrolu, že nebyl odeslán dřív než 3 sekundy po načtení.
- [ ] Žádná reCAPTCHA. Je to skript Googlu, kvůli kterému potřebuješ cookie lištu. Když spam nepoleví, Cloudflare Turnstile.

## Vložený obsah (iframe)

- [ ] Každý iframe má `title`. Bez něj čtečka přečte jen „rámec".
- [ ] Iframe níž na stránce má `loading="lazy"`. Bývá to nejtěžší prvek celé stránky.
- [ ] Iframe má pevnou výšku nebo `aspect-ratio`, ať stránka po načtení neposkočí.
- [ ] Na mobilu má plnou šířku a dost výšky, jinak vznikne vnitřní vodorovné rolování.
- [ ] Vedle iframu je přímá alternativa: odkaz „otevřít v novém okně", adresa textem vedle mapy. Pro případ, že se obsah nenačte.
- [ ] Vložený obsah je otestovaný na reálném iPhonu. Safari blokuje cookies třetích stran a vložený obsah se pak chová jinak než na tvém počítači.
- [ ] Vložený obsah je vyzkoušený naostro včetně celého řetězce, třeba rezervace až po potvrzovací e-mail.
