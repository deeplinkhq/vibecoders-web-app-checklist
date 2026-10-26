# Formuláře a vložený obsah

**Týká se:** webu s formulářem nebo vloženým obsahem třetí strany (mapa, video, kalendář, rezervace).

## Formulář

- [ ] **FORM-1** Formulář má co nejmíň polí. Orientačně: 1 pole 13,4 % konverze, 3 pole 10,1 %, 5 polí 7,8 %, 9 polí 3,6 %. Pro zájem stačí dvě pole, zbytek se doptáš v odpovědi.
- [ ] **FORM-2** Každé pole má viditelný `<label for="…">`. Placeholder není popisek. Chybí na 48 % domovských stránek.
- [ ] **FORM-3** Pole mají správný `type` (`email`, `tel`) a `autocomplete`, na mobilu pak vyskočí správná klávesnice.
- [ ] **FORM-4** Chybové hlášky jsou textové, konkrétní, u pole a navázané přes `aria-describedby`.
- [ ] **FORM-5** Je vidět stav: odesílám, odesláno, chyba. Bez toho lidé klikají třikrát. Potvrzení má `role="status"`, ať ho přečte i čtečka.
- [ ] **FORM-6** Po odeslání následuje konkrétní další krok, ne obecné „Děkujeme".

## Formulář, který tiše nefunguje

- [ ] **FORM-7** Kód kontroluje odpověď serveru (`if (!res.ok)`), nemá prázdný `catch` ani `mode: "no-cors"`. Agent rád ukáže „Odesláno", i když nic neodešlo.
- [ ] **FORM-8** Při chybě se ukáže hláška a náhradní kontakt (e-mail, telefon).
- [ ] **FORM-9** Ověřeno odesláním s vypnutou sítí: musí se ukázat chyba, ne úspěch.
- [ ] **FORM-10** Ověřeno odesláním z živého webu jako cizí člověk až po doručenou zprávu.

## Kam formulář posílá data

- [ ] **FORM-11** Formulář neposílá data přímo z prohlížeče na webhook (Discord, Slack, Make, n8n). Adresa webhooku je přístupový klíč bez hesla a kdokoli ji může zneužít. Podrobnosti v [Bezpečnosti](08-bezpecnost.md).
- [ ] **FORM-12** Data jdou přes serverovou funkci (klíč v proměnné prostředí, kontrola `Origin`, limit počtu odeslání), nebo přes formulářovou službu (Web3Forms 250 odeslání měsíčně zdarma, Formspree 50, stav 8/2026).

## Spam

- [ ] **FORM-13** Formulář má ochranu bez sledování: skryté pole (honeypot) a kontrolu, že nebyl odeslán dřív než 3 sekundy po načtení.
- [ ] **FORM-14** Žádná reCAPTCHA. Je to skript Googlu, kvůli kterému potřebuješ cookie lištu. Když spam nepoleví, Cloudflare Turnstile.

## Vložený obsah (iframe)

- [ ] **FORM-15** Každý iframe má `title`. Bez něj čtečka přečte jen „rámec".
- [ ] **FORM-16** Iframe níž na stránce má `loading="lazy"`. Bývá to nejtěžší prvek celé stránky.
- [ ] **FORM-17** Iframe má pevnou výšku nebo `aspect-ratio`, ať stránka po načtení neposkočí.
- [ ] **FORM-18** Na mobilu má plnou šířku a dost výšky, jinak vznikne vnitřní vodorovné rolování.
- [ ] **FORM-19** Vedle iframu je přímá alternativa: odkaz „otevřít v novém okně", adresa textem vedle mapy. Pro případ, že se obsah nenačte.
- [ ] **FORM-20** Vložený obsah je otestovaný na reálném iPhonu. Safari blokuje cookies třetích stran a vložený obsah se pak chová jinak než na tvém počítači.
- [ ] **FORM-21** Vložený obsah je vyzkoušený naostro včetně celého řetězce, třeba rezervace až po potvrzovací e-mail.
