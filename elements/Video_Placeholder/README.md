# Video Placeholder

## Wat het doet

Toont een HTML5-, YouTube- of Vimeo-video als een eigen placeholder-afbeelding met een eigen play-knop. De speler bestaat pas nadat de bezoeker klikt: het script vervangt dan de afbeelding en knop door de speler, start het afspelen en zet de focus op de speler. Het element is een uitbreiding op het standaard HTML5 Video-element van Oxygen.

## Wanneer gebruiken

- Als een video een eigen visuele uitstraling moet krijgen (afbeelding, knopkleur, eigen icoon) in plaats van de standaardspeler of het YouTube-/Vimeo-startscherm.
- Als YouTube of Vimeo niet bij het laden van de pagina mag worden aangeroepen (sneller laden, minder verkeer naar derden).
- Gebruik het standaard HTML5 Video-element als je geen placeholder nodig hebt.

## Instellingen

Content:

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Source Type | HTML5, YouTube of Vimeo | HTML5 |
| Video File | Videobestand uit de mediabibliotheek (alleen bij HTML5, ondersteunt dynamic data) | leeg |
| Video URL | Link naar de YouTube- of Vimeo-video (alleen bij YouTube/Vimeo) | leeg |
| Placeholder Image | Afbeelding die het kader vult; de alt-tekst komt uit de mediabibliotheek | leeg (donkere achtergrond) |
| Button Label | Tekst voor `aria-label` van de knop, van de HTML5-video en `title` van de iframe | Video afspelen |
| Custom Play Icon | Eigen icoon in plaats van de standaard driehoek | standaard driehoek |
| Loop, Muted, Controls, Plays Inline | Zoals bij het standaard HTML5 Video-element (alleen bij HTML5) | Controls en Plays Inline aan |

Design (alle instellingen onder Play Button kunnen een globale variabele gebruiken via de variabelenkiezer in de builder):

| Instelling | Wat het doet | Standaard |
| --- | --- | --- |
| Aspect Ratio | Verhouding van het kader (16:9, 4:3, 1:1, 21:9, 3:2, 9:16) | 16:9 |
| Play Button, Size | Breedte en hoogte van de knop; nooit breder dan 40% van het kader, dus kleiner op telefoons | 128px |
| Background Color | Achtergrondkleur van de knop | `var(--green, #669F87)` |
| Hover Background Color | Achtergrondkleur bij hover | iets lichter dan de achtergrondkleur |
| Icon Color | Kleur van het icoon | `#D9D9D9` |
| Icon Size | Grootte van het icoon, in % van het grootste vierkant binnen de cirkel (100% past precies) of px. Blijft altijd binnen dat vierkant | 54% |
| Border Radius | Afronding van de knop | 50% |

De standaardwaarden voor knopgrootte, kleuren en afronding staan in de CSS en verschijnen dus niet ingevuld in de velden. Een leeg veld gebruikt de standaardwaarde.

Geaccepteerde URL-vormen (YouTube en Vimeo: met of zonder `https://`):

- YouTube: `youtube.com/watch?v=`, `youtu.be/`, `youtube.com/embed/`, `youtube.com/shorts/`, `youtube.com/live/`, de `m.`- en `www.`-varianten en `youtube-nocookie.com/embed/`.
- Vimeo: `vimeo.com/<id>`, `vimeo.com/<id>/<hash>` of `vimeo.com/<id>?h=<hash>` (niet-openbare video) en `player.vimeo.com/video/<id>?h=<hash>`.
- HTML5: alleen `http(s)://` of een pad dat met `/` begint.

## Gedrag en privacy

- Click-to-load: in de eerste HTML staat geen `<video>` en gaat er geen verzoek naar YouTube of Vimeo. Pas na de klik wordt de speler aangemaakt en worden bestanden van de videodienst opgehaald.
- YouTube wordt geladen via `youtube-nocookie.com`, Vimeo met `dnt=1`. Dit beperkt tracking vooraf, maar haalt het niet weg: na de klik kunnen YouTube en Vimeo nog steeds gegevens verwerken.
- Beveiliging: de iframe-URL wordt altijd opnieuw opgebouwd uit een gevalideerd video-id en een vaste lijst met toegestane hostnamen. Een door de editor ingevulde URL komt nooit zelf in de iframe terecht. Bij een ongeldige URL blijft de placeholder staan en staat er een `console.warn` in de browserconsole.
- Toegankelijkheid: de knop is een echte `<button>` met `aria-label`, heeft een zichtbare focusring en de hover-animatie volgt `prefers-reduced-motion`.
- HTML5: als `play()` wordt geweigerd door de browser, wordt `controls` ingeschakeld zodat de bezoeker alsnog zelf kan starten.
- In de builder wordt de speler niet vervangen; het script draait alleen op de front-end.
- Icoon: op de site meet het script de echte vorm en legt de kleinste omsluitende cirkel daarvan op het midden van de knop. Lege ruimte in de `viewBox` telt dus niet mee en een driehoek oogt recht. Icon Size geldt voor die omsluitende cirkel, dus een vierkant icoon oogt kleiner dan een driehoek op dezelfde waarde.
- Het hele placeholder-kader is klikbaar (niet alleen de knop) en toont een aanwijzer en de hover-stand van de knop. Toetsenbordgebruikers starten de video via de knop.

## Beperkingen

- Mobiele browsers kunnen autoplay blokkeren; een tweede tik op de speler kan dan nodig zijn.
- Het centreren van een eigen icoon gebeurt alleen op de site, niet in de builder: daar staat het icoon nog volgens zijn eigen `viewBox`. Stroke-breedte telt niet mee, en iconen die later via AJAX worden geladen worden niet gemeten.
- De variabelenkiezer staat aan via `enableVariables` in `designControls()` van `element.php`. Controleer na opslaan in Element Studio of die regel er nog staat: de studio kan dit bestand herschrijven.
- Een `Permissions-Policy`-header met `autoplay=()` of `encrypted-media=()` blokkeert YouTube en Vimeo; zie stap 4 bij Installatie.
- Geen integratie met een cookie-consenttool. De klik geldt niet automatisch als toestemming.
- JavaScript is vereist; zonder JavaScript doet de knop niets.
- Eén klik-script wordt via de dependencies van het element ingevoegd; bij meerdere instanties voorkomt een vlag dat het dubbel wordt gebonden.
- Alleen losse video-URL's; geen afspeellijsten, starttijden of extra embed-parameters.
- Standaard is het icoon `#D9D9D9` op groen (`#669F87`): ongeveer 2,2:1 contrast, onder de 3:1 van WCAG 1.4.11. Dit volgt het ontwerp; pas het aan via Icon Color of Background Color.
- Met Controls uit kan de bezoeker een HTML5-video niet pauzeren, en met Loop aan stopt hij nooit.
- Zonder ingesteld video-bestand of video-URL wordt op de site geen knop getoond (in de builder blijft de knop zichtbaar om te stylen).

## Installatie

1. Maak in de builder (Element Studio, `Ctrl+Alt+E`) een nieuw element `Video Placeholder` met opslaglocatie "PDK Elementen". De API kan geen elementen aanmaken.
2. Zet de inhoud van de vier bestanden in `elements/Video_Placeholder/` (`element.php`, `html.twig`, `css.twig`, `default.css`) in het nieuwe element, via `pdk-theme-options/list-oxygen-elements`, `read-oxygen-element-file` en `write-oxygen-element-file`. `README.md` blijft alleen in de repository.
3. Controleer op de site dat het element rendert: `element.php` wordt bij opslaan op syntaxis gecontroleerd, Twig niet.
4. Controleer de `Permissions-Policy`-header van de site (`curl -sI https://site.nl/ | grep -i permissions-policy`). Staat daarin `autoplay=()` of `encrypted-media=()`, zoals de hostingbeveiliging cPFence instelt, dan geeft Vimeo "Unable to play video" en vraagt YouTube om een extra klik. Het element kan dat niet omzeilen. Voeg dan dit toe aan de eigen PHP-code van de site (`custom-functions.php`). Alleen de eigen site, YouTube en Vimeo krijgen deze twee rechten; de rest van de header blijft gelijk:

   ```php
   // Video-embeds toestaan: cPFence blokkeert autoplay en encrypted-media voor alle iframes.
   add_filter( 'wp_headers', function ( $headers ) {
   	if ( empty( $headers['Permissions-Policy'] ) ) {
   		return $headers;
   	}
   	$allow = '(self "https://www.youtube-nocookie.com" "https://player.vimeo.com")';
   	$headers['Permissions-Policy'] = str_replace(
   		array( 'autoplay=()', 'encrypted-media=()' ),
   		array( "autoplay=$allow", "encrypted-media=$allow" ),
   		$headers['Permissions-Policy']
   	);
   	return $headers;
   }, 20 );
   ```

## Versie/compatibiliteit

Ontwikkeld tegen Oxygen 6.2.1 (Element Studio, builder 6.2.1, de versie op de live site), WordPress 7.1.4, PHP 8.5.12. Browsers: elk recent browser met `URL`, `replaceChildren`, CSS `aspect-ratio`, `grid`, `:has()` en de losse CSS-eigenschap `scale`.
