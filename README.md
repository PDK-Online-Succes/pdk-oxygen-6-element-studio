# pdk-oxygen-6-element-studio

Eigen bibliotheek met elementen voor Oxygen 6 (Element Studio). Elk element staat in een eigen map onder `elements/` en heeft een eigen `README.md` met uitleg. De repository is de bron van waarheid; de site krijgt een kopie.

## Een element installeren op een site

1. Maak in de builder een leeg element aan (Element Studio, `Ctrl+Alt+E`, New element, opslaglocatie "PDK Elementen"). De API kan geen elementen aanmaken.
2. Schrijf de bestanden `element.php`, `html.twig`, `css.twig` en `default.css` uit de elementmap naar dat element, via `pdk-theme-options/list-oxygen-elements`, `read-oxygen-element-file` en `write-oxygen-element-file`.
3. Controleer in de builder en op de front-end dat het element rendert.

Meer regels staan in [CLAUDE.md](CLAUDE.md).

## Elementen

| Element | Slug | Wat het doet | Docs |
| --- | --- | --- | --- |
| Before After | `PdkElements\BeforeAfter` | Vergelijkt een voor- en na-afbeelding met een versleepbare scheidingslijn; ook met het toetsenbord te bedienen. | [README](elements/Before_After/README.md) |
| Fotogalerij | `PdkElements\Fotogalerij` | Raster van foto's uit de mediabibliotheek; een klik opent de grote foto in een lightbox (GLightbox uit de Libraries-map). | [README](elements/Fotogalerij/README.md) |
| Video Placeholder | `PdkElements\VideoPlaceholder` | HTML5-, YouTube- of Vimeo-video met eigen placeholder-afbeelding en play-knop; de speler laadt pas na een klik. | [README](elements/Video_Placeholder/README.md) |
