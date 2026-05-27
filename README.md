# Programmerings-dokumentation

## Kort beskrivelse af projektet
Skriv kort, hvad dit projekt handler om.

Eksempel på ting du kan beskrive:

* Hvad er formålet med projektet?
* Hvilke teknologier har du brugt?
* Hvad kan brugeren gøre på siden?
* Hvilken type data arbejder projektet med?

> Formålet med dette projekt er at overskueliggøre Spilcaféens udvalg af spil for dens gæster. Løsningen er en listeside med simpel filtrering samt en detaljeside for hvert spil. 

> I løsningen gør jeg brug af HTML, CSS og JavaScript. HTML har jeg brugt til at opbygge strukturen på siden, og CSS har jeg brugt til styling, grid-layout og visuel interaktivitet. JavaScript-koden henter, viser og filtrerer spil fra en JSON-fil med data for brætspil.

> Brugeren kan søge efter specifikke spiltitler, filtrere efter genre og sortere listen alfabetisk eller efter udgivelsesår. Når brugeren klikker på et spil åbnes detaljesiden.


## Fil- og mappestruktur
Beskriv, hvordan du har organiseret dit projekt i filer og mapper.

Du kan for eksempel forklare:

* Hvad indeholder din `html`-fil?
* Hvad bruges din `css`-mappe til?
* Hvad bruges din `js`-mappe til?
* Hvor ligger dine billeder?
* Hvorfor har du valgt denne struktur?

> Mit projekt er organiseret således:
> * `index.html` indeholder sidens struktur, opdelt i header og main. Derudover opdelt i et semantisk `<form>`-element indeholdende `input` og `select` felter, en `section` til spillisten samt en `dialog` til et spils detaljeside.
> * `app.css` indeholder ekstern styling, layout og visuel interaktivitet. Jeg har lavet ekstern styling for at holde styling adskilt fra HTML og JS. Filen bruger CSS-variabler til farver, skrifttyper og -størrelser samt CSS Grid til grid-layoutet.
> * `app.js` indhenter data fra en ´JSON´-fil, håndterer filtrering og sortering samt opdaterer HTML'en gennem DOM-manipulation.
> * `img`-mappen bruger jeg til at strukturere mit eneste billede (logo), som er en `.webp`-fil så indlæsningstiden optimeres. 



## Validering af CSS
Beskriv, hvordan du har valideret din CSS.

Skriv for eksempel:

* Hvilken CSS-fil har du valideret?
* Hvilket værktøj har du brugt?
* Fik du fejl eller advarsler?
* Hvordan rettede du eventuelle fejl?

> Jeg har valideret ´app.css` vha. W3School's CSS Validation Service. 



## Validering af HTML

Beskriv, hvordan du har valideret din HTML.

Skriv for eksempel:

* Hvilken HTML-fil har du valideret?
* Hvilket værktøj har du brugt?
* Fik du fejl eller advarsler?
* Hvordan rettede du eventuelle fejl?

> Jeg har valideret ´index.html` vha. W3School's Markup Validation Service. 



## JavaScript datastruktur

Beskriv den datastruktur, du har brugt i JavaScript.

Du kan for eksempel forklare:

* Hvilken type data arbejder du med? 
* Har du brugt et array? 
* Indeholder arrayet objekter? 
* Hvilke properties findes i hvert objekt? 
* Hvorfor passer denne datastruktur til dit projekt?

>> Jeg arbejder med data hentet fra en JSON-fil. I JavaScript har jeg gemt dataene i et array (`allGames`). Arrayet indeholder objekter fra JSON-filen, som er hentet og gemt i variablen `data`. Hvert objekt repræsenterer et spil, og har properties'ne: 
* id
* title
* description
* image
* genre
* playtime
* players
* language
* rating
* age
* difficulty
* location
* shelf
* available
* rules

> I et array med objekter kan jeg bruge `filter` og `sort` til at gennemløbe dataene/spillene og vise dem ud fra brugerens filtrering/sortering.


## Eksempel på JavaScript kode
Vælg et vigtigt stykke JavaScript-kode fra dit projekt.

Det kan for eksempel være kode, der:

* viser data i DOM’en
* filtrerer data
* søger i data
* reagerer på brugerinput
* bruger en funktion
* bruger forEach metoden

```
function applyFiltersAndSort() {
  const selectedGenre = genreSelect.value;
  const searchValue = searchInput.value.trim().toLowerCase();
  const sortOption = sortSelect.value;

  let filteredGames = allGames.filter((game) => {
    const genres = Array.isArray(game.genre)
      ? game.genre
      : [game.genre];

    const matchesGenre =
      selectedGenre === "all" || genres.includes(selectedGenre);

    const matchesSearch = game.title
      .toLowerCase()
      .includes(searchValue);

    return matchesGenre && matchesSearch;
  });

  if (sortOption === "title") {
    filteredGames.sort((a, b) =>
      a.title.localeCompare(b.title)
    );
  } else if (sortOption === "year") {
    filteredGames.sort((a, b) => b.year - a.year);
  }

  showGames(filteredGames);
}
```

## Hvad gør koden?
Forklar med dine egne ord, hvad koden gør.

Skriv for eksempel:

* Hvad sker der først?
* Hvilke data bruges?
* Hvilken funktion bliver kaldt?
* Hvordan påvirker koden HTML-siden?
* Hvorfor er koden vigtig for projektet?

> 