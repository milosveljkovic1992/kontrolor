# Kontrolor

Tekstualna igra u kojoj si član biračkog odbora na izborima u Srbiji. Kroz izborni dan, od primopredaje materijala u 06:00 do potpisivanja zapisnika u 21:45, rešavaš 21 situaciju na biračkom mestu i biraš šta odbor treba da uradi.

Posle svake odluke igra pokazuje da li je odluka ispravna, delimično ispravna ili pogrešna, zašto je tako i koje pravilo važi.

## Kako se igra

- Svaka situacija ima četiri opcije. Izabrana opcija se „zaokruži“ kao na glasačkom listiću.
- Tri merača prate tvoj rad: **zakonitost**, **red na biračkom mestu** i **poverenje birača**.
- Na kraju dobijaš zapisnik o radu sa svim odlukama, brojem ispravnih odluka i ocenom.
- Redosled opcija se meša u svakoj partiji.

Situacije obuhvataju, između ostalog: kontrolni list, utvrđivanje identiteta birača, proveru UV lampom, glasanje umesto drugog, porodično glasanje, pomagača za slepog birača, neovlašćeno beleženje birača, fotografisanje listića, „bugarski voz“, izbornu tišinu, zatvaranje biračkog mesta, redosled brojanja, važnost listića i primedbe na zapisnik.

## Struktura projekta

```
index.html     cela aplikacija (HTML, CSS i JavaScript u jednom fajlu)
og-image.png   slika za deljenje na društvenim mrežama (1200 × 630)
netlify.toml   podešavanja za Netlify (objava i bezbednosna zaglavlja)
CHANGELOG.md   spisak izmena po verzijama
README.md      ovaj fajl
```

Nema zavisnosti ni build koraka. Jedini spoljni resursi su fontovi sa Google Fonts (Bitter, Source Serif 4, IBM Plex Mono).

## Lokalno pokretanje

Otvori `index.html` direktno u pregledaču, ili pokreni lokalni server:

```sh
python3 -m http.server 8000
```

pa otvori http://localhost:8000.

## Objava na Netlify

**Preko Git repozitorijuma (preporučeno)**

1. Postavi projekat na GitHub, GitLab ili Bitbucket.
2. Na Netlify izaberi **Add new site → Import an existing project** i poveži repozitorijum.
3. Build command ostavi prazno, a publish directory je `.`. Ova podešavanja se čitaju iz `netlify.toml`.
4. Pokreni **Deploy**. Svaki novi push na glavnu granu automatski objavljuje novu verziju.

**Preko Netlify CLI**

```sh
npm install -g netlify-cli
netlify login
netlify deploy          # probna objava
netlify deploy --prod   # produkcija
```

**Bez naloga za Git:** prevuci folder projekta na https://app.netlify.com/drop.

## Izmena sadržaja

Sve situacije su u nizu `S` unutar `<script>` bloka u `index.html`. Svaka situacija ima ovaj oblik:

```js
{ t: "07:20",                       // vreme na satu
  title: "Komšija bez lične karte",
  text: "Opis situacije…",
  opts: [
    { x: "Tekst opcije", v: "ok" },                 // ok | part | bad
    { x: "Tekst opcije", v: "bad", f: "Kratko objašnjenje zašto",
      fx: [-8, -10, -8] },                          // opciono: promena merača
    …
  ],
  why: "Pravilo koje se prikazuje posle odgovora." }
```

Ako opcija nema `fx`, koriste se podrazumevane promene merača iz objekta `DEF` (redom: zakonitost, red, poverenje). Ocene na kraju igre zavise od broja bodova i definisane su u funkciji `renderEnd`.

## Verzionisanje

Trenutna verzija je upisana na jednom mestu, u `index.html`:

```html
<meta name="version" content="1.0.0">
```

Broj verzije ima oblik `GLAVNI.SPOREDNI.ISPRAVKA`:

| Izmena | Primer | Nova verzija |
|---|---|---|
| Ispravka teksta, pravila ili greške u kodu | pogrešan rok u objašnjenju | 1.0.0 → 1.0.1 |
| Nove ili izmenjene situacije, nova funkcija | dodata situacija o glasanju van biračkog mesta | 1.0.1 → 1.1.0 |
| Veća promena igre ili usklađivanje sa novim zakonom | igra za lokalne izbore, novi sistem bodovanja | 1.1.0 → 2.0.0 |

Postupak za novu verziju:

1. Promeni `content` u `<meta name="version">`.
2. U `CHANGELOG.md` premesti stavke iz „Neobjavljeno“ pod novi naslov sa brojem verzije i datumom.
3. Napravi commit i Git tag, pa pošalji oba:

```sh
git commit -am "Verzija 1.0.1"
git tag -a v1.0.1 -m "Verzija 1.0.1"
git push && git push --tags
```

## Napomena o tačnosti

Igra je edukativna simulacija sa izmišljenim situacijama. Pravila su pojednostavljena prema Zakonu o izboru narodnih poslanika i uputstvima Republičke izborne komisije i nisu pravni savet. Neke detalje, kao što su postupak kad birač fotografiše listić i sastav odbora koji izlazi na glasanje van biračkog mesta, treba proveriti u važećem uputstvu RIK pre korišćenja igre na obukama. Na stvarnim izborima uvek važe zakon i uputstvo za te izbore.
