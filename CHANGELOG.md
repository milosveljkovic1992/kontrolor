# Izmene

Sve značajne izmene igre Kontrolor beleže se u ovom fajlu. Brojevi verzija prate pravila opisana u odeljku „Verzionisanje“ u README.md.

## [Neobjavljeno]

### Dodato
- Link „← Sve igre“ iznad zaglavlja, ka krovnoj aplikaciji Izborni dan (https://izborni-dan.netlify.app/).
- Ikonica u tabu pregledača (favicon): glasačka kutija sa listićem, ugrađena u `index.html` kao SVG.
- Slika za deljenje na društvenim mrežama (`og-image.png`, 1200 × 630) i Open Graph i Twitter meta tagovi.

### Promenjeno
- Slika za deljenje se u `og:image` i `twitter:image` navodi punom adresom (https://kontrolor.netlify.app/og-image.png), a dodat je i `og:url`.
- Meta opis stranice: „Član si biračkog odbora na dan izbora. Kroz 21 situaciju, od primopredaje materijala do zapisnika, odluči šta je ispravno i saznaj zašto.“

## [1.0.0] - 2026-10-13

### Dodato
- Igra sa 21 situacijom tokom izbornog dana, od primopredaje materijala do potpisivanja zapisnika.
- Tri merača: zakonitost, red na biračkom mestu i poverenje birača.
- Objašnjenje i pravilo posle svake odluke, zapisnik o radu i ocena na kraju igre.
- Mešanje redosleda opcija u svakoj partiji.
- Podešavanja za objavu na Netlify (`netlify.toml`) sa bezbednosnim zaglavljima.
- Oznaka verzije u `<meta name="version">`.
