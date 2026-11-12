# Before After

## Wat het doet

Vergelijkt twee afbeeldingen (voor en na) die op elkaar liggen. Een scheidingslijn met een greep laat links (of boven) de voor-afbeelding zien en rechts (of onder) de na-afbeelding. De bezoeker verschuift de lijn door te slepen met muis of vinger, of met de pijltjestoetsen.

## Wanneer gebruiken

- Om een verschil tussen twee afbeeldingen van hetzelfde onderwerp te tonen: een verbouwing, een behandeling, een bewerkte foto.
- Werkt het best met twee afbeeldingen met dezelfde verhouding en dezelfde uitsnede.
- Gebruik twee losse Image-elementen als de afbeeldingen naast elkaar moeten staan.

## Instellingen

Content:

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Before Image | Voor-afbeelding uit de mediabibliotheek (ondersteunt dynamic data) | leeg |
| Before Alt Text | Eigen alt-tekst; leeg gebruikt de alt-tekst uit de mediabibliotheek | leeg |
| After Image | Na-afbeelding uit de mediabibliotheek (ondersteunt dynamic data) | leeg |
| After Alt Text | Eigen alt-tekst; leeg gebruikt de alt-tekst uit de mediabibliotheek | leeg |
| Orientation | Horizontal (voor links, na rechts) of Vertical (voor boven, na onder) | Horizontal |
| Start Position (%) | Positie van de lijn bij het laden, 0 tot 100, gemeten vanaf links (of boven) | 50 |
| Show Labels | Toont de labels in de hoeken | aan |
| Before Label, After Label | Tekst van de labels | Voor, Na |
| Custom Handle Icon | Eigen icoon in de greep in plaats van de twee pijltjes | twee pijltjes |
| Slider Label | `aria-label` van de schuifregelaar voor schermlezers | Vergelijk voor en na |

Design (alle instellingen kunnen een globale variabele gebruiken via de variabelenkiezer in de builder):

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Divider, Line Color | Kleur van de lijn, en van de greep als Handle Background Color leeg is | `#fff` |
| Line Thickness | Dikte van de lijn | 2px |
| Handle Size | Breedte en hoogte van de greep (per breakpoint) | 44px |
| Handle Border Radius | Afronding van de greep | 50% |
| Handle Background Color | Achtergrondkleur van de greep | de lijnkleur |
| Icon Color | Kleur van het icoon in de greep | `#222` |
| Labels, Text Color | Tekstkleur van de labels | `#fff` |
| Labels, Background Color | Achtergrond van de labels | `rgba(0, 0, 0, .6)` |

De standaardwaarden staan in de CSS en verschijnen dus niet ingevuld in de velden. Een leeg veld gebruikt de standaardwaarde.

## Gedrag en privacy

- Beide afbeeldingen liggen in één vak; de hoogste bepaalt de hoogte, de andere wordt passend bijgesneden (`object-fit: cover`). De voor-afbeelding wordt afgesneden met `clip-path` op de positie uit de CSS-variabele `--pos`.
- Slepen werkt op het hele element (pointer events), niet alleen op de greep. Op een touchscreen verschuift de lijn pas bij bewegen, zodat scrollen over het element de lijn niet laat springen: horizontaal blijft verticaal scrollen werken, verticaal blijft horizontaal scrollen werken.
- Toetsenbord: een echte, onzichtbare `<input type="range">` met `aria-label` krijgt de focus. Pijltjestoetsen, Home, End, Page Up en Page Down verschuiven de lijn; de greep krijgt dan een zichtbare focusring. In verticale stand schuift pijl omhoog de lijn omhoog.
- Eén klein script zonder externe bibliotheken, via de dependencies van het element. Het luistert op `document`, dus meerdere elementen op één pagina werken los van elkaar, ook elementen die later worden geladen.
- Afbeeldingen krijgen `loading="lazy"`, `decoding="async"`, `width`/`height` en `srcset`/`sizes` uit de mediabibliotheek.
- Beveiliging: alle editorwaarden worden geescaped. Een afbeeldings-URL wordt alleen gebruikt als hij met `http://` of `https://` begint of een pad is dat met één `/` gevolgd door een letter, cijfer of `-_.~%` begint; anders wordt de afbeelding weggelaten. De startpositie moet een getal zijn (anders 50) en wordt op 100 afgekapt.
- Geen verzoeken naar derden; er wordt niets opgeslagen.
- Lege staat: in de builder toont het element grijze vlakken met "Kies een voor-afbeelding" en "Kies een na-afbeelding". Op de site wordt zonder afbeeldingen niets getoond; met één afbeelding blijft de andere kant een leeg grijs vlak.

## Beperkingen

- In de builder werkt slepen niet (het script draait alleen op de front-end); de lijn staat daar op de startpositie.
- JavaScript is vereist om te verschuiven; zonder JavaScript blijft de lijn op de startpositie staan.
- Met het toetsenbord gaat de lijn in stappen van 1%; slepen is traploos.
- De labels zijn `aria-hidden`: schermlezers krijgen de alt-teksten en het Slider Label. Zet dus een goede alt-tekst bij beide afbeeldingen.
- Het eigen icoon wordt niet gedraaid in verticale stand (de standaard pijltjes wel).
- Geen eigen verhouding: twee afbeeldingen met verschillende verhoudingen worden bijgesneden.
- De variabelenkiezer staat aan via `enableVariables` in `designControls()` van `element.php`. **Opslaan in Element Studio haalt dit weg:** de generator van Oxygen 6.2.1 schrijft deze optie niet weg. Bewerk dit element daarom alleen via de repository, of zet `element.php` daarna opnieuw uit de repository op de site.

## Installatie

1. Maak in de builder (Element Studio, `Ctrl+Alt+E`) een nieuw element `Before After` met opslaglocatie "PDK Elementen". De API kan geen elementen aanmaken.
2. Zet de inhoud van de vier bestanden in `elements/Before_After/` (`element.php`, `html.twig`, `css.twig`, `default.css`) in het nieuwe element, via `pdk-theme-options/list-oxygen-elements`, `read-oxygen-element-file` en `write-oxygen-element-file`. `README.md` blijft alleen in de repository.
3. Controleer op de site dat het element rendert, in de builder en op de front-end: `element.php` wordt bij opslaan op syntaxis gecontroleerd, Twig niet.

## Versie/compatibiliteit

Ontwikkeld tegen Oxygen 6.2.1 (Element Studio), WordPress 7.1.4, PHP 8.5.12. Browsers: elk recent browser met pointer events, `setPointerCapture`, CSS `clip-path: inset()`, `grid`, `aspect-ratio` en de losse CSS-eigenschappen `translate` en `rotate`.
