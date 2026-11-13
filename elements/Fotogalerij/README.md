# Fotogalerij

## Wat het doet

Toont foto's uit de mediabibliotheek in een raster. Een klik op een foto opent de grote versie in een lightbox (GLightbox) waarin de bezoeker door de foto's van die galerij bladert. Optioneel staat er een bijschrift onder elke foto.

## Wanneer gebruiken

- Voor een fotogalerij of portfolio met meerdere foto's in een raster.
- Zet de lightbox uit als de foto's niet groter hoeven te worden geopend.
- Gebruik het Image-element voor een enkele foto.

## Instellingen

Content, Galerij:

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Foto's | Foto's uit de mediabibliotheek (meerdere tegelijk te kiezen); bijschrift en alt-tekst komen uit de mediabibliotheek | leeg |
| Formaat in raster | Thumbnail, Medium, Medium Large, Large of Full | Thumbnail |
| Lightbox uitzetten | Foto's zonder link tonen | uit |
| Bijschriften tonen | Toont het bijschrift onder de foto | uit |

Design, Layout:

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Kolommen | Aantal kolommen (per breakpoint) | 3 (2 onder 480px) |
| Tussenruimte | Ruimte tussen de foto's (per breakpoint) | 10px |
| Vierkant bijsnijden | Snijdt alle foto's bij tot een vierkant | uit |

De standaardwaarden staan in de CSS en verschijnen dus niet ingevuld in de velden. Let op: de standaard van 2 kolommen op telefoons (tot 479px) geldt alleen zolang Kolommen leeg is. Zodra je Kolommen invult, wordt die waarde ook op telefoons gebruikt; stel Kolommen daarom ook in op de kleine breakpoints.

## Gedrag en privacy

- De foto's staan in een lijst (`<ul>`); elke foto met lightbox is een link naar de grote foto (`full`) met het bijschrift in `data-title`.
- De foto wordt met een eigen `<img>` getoond (niet met de Oxygen-afbeeldingsmacro): `alt` is altijd aanwezig (leeg als de mediabibliotheek geen alt-tekst heeft, dus als decoratief beeld), de alt-tekst wordt geescaped, en `width`, `height`, `srcset`, `sizes`, `loading="lazy"` en `decoding="async"` komen erbij.
- Lightbox: [GLightbox](https://github.com/biati-digital/glightbox) 3.3.1 (MIT-licentie). Het element laadt de bibliotheek niet zelf; die komt uit de Libraries-map van PDK Theme Options (zie Installatie). Een klein script via de dependencies van het element luistert op `document` en start GLightbox bij de klik. De laadvolgorde van bibliotheek en script maakt dus niet uit.
- Elke galerij heeft een eigen lightbox: bladeren gaat alleen door de foto's van de galerij waarin is geklikt, ook met meerdere galerijen op één pagina.
- Zonder GLightbox (bibliotheek niet geplaatst, of geen JavaScript) opent een klik gewoon de grote foto. De pagina blijft bruikbaar.
- Beveiliging: alle editorwaarden worden geescaped. Het bijschrift in `data-title` wordt dubbel geescaped, omdat GLightbox de titel als HTML in de lightbox zet: HTML in een bijschrift verschijnt dus als tekst. Kolommen en Tussenruimte worden in de CSS ontdaan van `; { } < > *` en quotes. De URL van de grote foto en van de getoonde foto wordt alleen gebruikt als hij met `http://` of `https://` begint of een pad is dat met één `/` gevolgd door een letter, cijfer of `-_.~%` begint; anders wordt de foto zonder link (of helemaal niet) getoond.
- Geen verzoeken naar derden: GLightbox wordt van de eigen site geladen; er wordt niets opgeslagen.
- Lege staat: zonder foto's toont alleen de builder de melding "Kies foto's onder Content > Galerij."; op de site wordt niets getoond.

## Beperkingen

- In de builder opent de lightbox niet (het script draait alleen op de front-end).
- De lightbox toont alleen foto's, geen video of tekst.
- Bijschriften komen uit de mediabibliotheek; een eigen bijschrift per foto in het element is er niet.
- Foto's met een ongeldige URL (zie Beveiliging) krijgen geen link.

## Installatie

1. Zet GLightbox 3.3.1 (MIT-licentie, project: https://github.com/biati-digital/glightbox) in de Libraries-tab van PDK Theme Options (`wp-content/uploads/pdk-theme-options/libraries/`). Download beide bestanden en zet ze daar neer:
   - https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/js/glightbox.min.js
   - https://cdn.jsdelivr.net/npm/glightbox@3.3.1/dist/css/glightbox.min.css

   De module laadt elk `.js`- en `.css`-bestand uit die map op de front-end.
2. Maak in de builder (Element Studio, `Ctrl+Alt+E`) een nieuw element `Fotogalerij` met opslaglocatie "PDK Elementen". De API kan geen elementen aanmaken.
3. Zet de inhoud van de vier bestanden in `elements/Fotogalerij/` (`element.php`, `html.twig`, `css.twig`, `default.css`) in het nieuwe element, via `pdk-theme-options/list-oxygen-elements`, `read-oxygen-element-file` en `write-oxygen-element-file`. `README.md` blijft alleen in de repository.
4. Controleer op de site dat het element rendert, in de builder en op de front-end, en dat een klik de lightbox opent: `element.php` wordt bij opslaan op syntaxis gecontroleerd, Twig niet.

## Versie/compatibiliteit

Ontwikkeld tegen Oxygen 6.2.1 (Element Studio), WordPress 7.1.4, PHP 8.5.12 en GLightbox 3.3.1. Browsers: elk recent browser met CSS `grid` en `aspect-ratio`.
