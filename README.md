# Programmerings-dokumentation

## Kort beskrivelse af projektet
Formålet med dette projekt er at overskueliggøre Spilcaféens udvalg af spil for dens gæster. Løsningen er en listeside med simpel filtrering samt en detaljeside for hvert spil. 

I løsningen gør jeg brug af HTML, CSS og JavaScript. HTML har jeg brugt til at opbygge strukturen på siden, og CSS har jeg brugt til styling, grid-layout og visuel interaktivitet. JavaScript-koden henter, viser og filtrerer spil fra en JSON-fil med data for brætspil.

Brugeren kan søge efter specifikke spiltitler, filtrere efter genre og sortere listen alfabetisk eller efter udgivelsesår. Når brugeren klikker på et spil åbnes detaljesiden.

## Fil- og mappestruktur
Mit projekt er organiseret således:
* `index.html` indeholder sidens struktur, opdelt i header og main. Derudover opdelt i et semantisk `<form>`-element indeholdende `input` og `select` felter, en `section` til spillisten samt en `dialog` til et spils detaljeside.
* `app.css` indeholder ekstern styling, layout og visuel interaktivitet. Jeg har lavet ekstern styling for at holde styling adskilt fra HTML og JS. Filen bruger CSS-variabler til farver, skrifttyper og -størrelser samt CSS Grid til grid-layoutet.
* `app.js` indhenter data fra en ´JSON´-fil, håndterer filtrering og sortering samt opdaterer HTML'en gennem DOM-manipulation.
* `img`-mappen bruger jeg til at strukturere mit eneste billede (logo), som er en `.webp`-fil så indlæsningstiden optimeres. 

## Validering af CSS
Jeg har valideret ´app.css` vha. W3School's CSS Validation Service. Ingen fejl fundet.

![billede af CSS validering](img/css-validering.png "CSS validering.")

## Validering af HTML
Jeg har valideret ´index.html` vha. W3School's Markup Validation Service. 
Jeg har lavet den fejl at skrive px i width for et billede i HTML, hvor der blot forventes et tal. Det har jeg rettet, så der kun står "80".
![billede af html validering](img/html-validering.png "HTML validering.")

Jeg fik en advarsel om manglende headers i to section-tags. Jeg har valgt at ændre begge til div-tags, da de begge har et layout-mæssigt formål. Den ene er blot en status bar der skal vise, hvor mange resultater der vises, og den anden er blot containeren for spil-griddet.
![endnu et billede af html validering](img/html-validering-div-tags.png "HTML validering af div tags.")
![billede af html div tags](img/html-div-tags.png "HTML billede af div tags.")

Herefter viser validering ingen fejl.
![billede af html godkendt](img/html-godkendt.png "HTML godkendt.")

## JavaScript datastruktur
Jeg arbejder med data hentet fra en JSON-fil. I JavaScript har jeg gemt dataene i et array (`allGames`). Arrayet indeholder objekter fra JSON-filen, som er hentet og gemt i variablen `data`. Hvert objekt repræsenterer et spil, og har properties'ne: 
* id, title, description, image, genre, playtime, players, language, rating, age, difficulty, location, shelf, available, rules.

I et array med objekter kan jeg bruge `filter` og `sort` til at gennemløbe dataene/spillene og vise dem ud fra brugerens filtrering/sortering.

## Eksempel på JavaScript kode
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
### Hvad gør koden?
Dette stykke kode gør det muligt for brugeren at søge efter specifikke titler, sortere og filtrere efter genre. Det gøres med en funktion indeholdende en `filter()`funktionen samt et if- og if else-statement. Funktionen påvirker HTML-siden ved at kalde på showGames funktionen, som udfører DOM-manipulation og viser spil på siden.

1. Funktionen applyFiltersAndSort gemmer først brugerens input (value) fra genre-dropdown (genreSelect), søgebaren (searchInput) og sorteringen (sortSelect) i variabler. 
2. Et nyt array oprettes (filteredGames) og `filter()` gennemgår hvert spil (game) i spildata-arrayet (allGames).
    * `Array.isArray` tjekker om genren for et spil er et array, og hvis den er, bruges den direkte, og hvis den ikke er, laves den om til et array for kun at bruge én datatype.
    * Koden tjekker om brugeren har valgt at se alle genrer (value: 'all'), og hvis det ikke er true, returneres den valgte genre (includes()).
    * Koden tjekker brugerens input i søgebaren for matches med spiltitler, og tilpasser inputtet til at være små bogstaver.
    * Resultaterne af disse tjek returneres i det nye array hvis de matcher både genre og søgeinput.
3. Funktion tjekker om brugeren har valgt at sortere på titelnavn, hvis ja, sorteres spiltitler i arrayet (filteredGames) fra a til b. Hvis brugeren i stedet har valgt at sortere for årstal, sorteres arrayet efter årstal.
4. Til sidst viser funktionen det nye array som søgeresultater for brugeren på siden.

