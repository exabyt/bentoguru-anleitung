# Editierbare Bentoguru-Projekte ohne Connector erstellen

**Prompt zum Kopieren**

> Lies die BentoGuru-Anleitung. Beginne bei Gemini mit HTML (https://bento-guru.b-cdn.net/ki-anleitung.html), sonst mit TXT (https://bento-guru.b-cdn.net/ki-anleitung.txt). Falls du die Anleitung dort nicht lesen kannst, versuche die andere Fassung. Gestalte [mein Thema, Inhalt und gewünschtes Format]. Gib mir das Projekt als .bento-Datei oder als anklickbaren Direktlink, wie gewünscht. Falls ich Dateien oder Bildlinks mitgebe, verwende sie nach Möglichkeit. Wähle die Gestaltung passend zu meiner Idee.

## Ergebnis

Gestalte nach dem Auftrag. Texte bleiben editierbar. Für Typografie, grafische Kompositionen und Pixel Art reichen Text- und Farbkacheln. Baue Pixelmotive direkt aus farbigen Rasterzellen. Wenn der Nutzer später eigene Bilder einsetzen möchte, plane dafür leere Bildkacheln ein. Gibt er Dateien oder direkte Bildlinks mit, verwende sie nach Möglichkeit an der gewünschten Stelle. Wünscht er Bildideen, kannst du passende Bilder generieren oder geeignete Fotos etwa auf Unsplash oder Pexels suchen. Beachte die Nutzungsbedingungen und erforderliche Bildnachweise. Verwende echte, verfügbare Motive und gib jedem separat bearbeitbaren Foto eine eigene Kachel.

- **.bento-Datei:** Verwende die Dateiwerkzeuge deines Chats. Schreibe das Projektobjekt direkt als UTF-8-JSON in eine Datei mit der Endung `.bento` und stelle diese als Download bereit. Dieses Format unterstützt auch eingebettete Bilder. Der Benutzer öffnet die Datei über «Projekt öffnen» oder zieht sie auf den Canvas.
- **Direktlink:** Kodiere das Projekt wie im Python-Beispiel unten und gib den vollständigen, anklickbaren Link mit `https://www.bentoguru.com/#template=GZ1-` aus. Ein rein grafischer Entwurf benötigt keine Bildquelle. Für verlinkte Fotos speichere die direkte öffentliche HTTPS-Bildadresse in `sourceUrl` und lasse `src` leer. Beim Öffnen lädt der Browser die verlinkten Kachel- und Hintergrundbilder automatisch. Für lokale oder generierte Fotos ohne öffentliche URL kannst du im Direktlink Bildkacheln zum späteren Befüllen vorsehen. Wenn der Nutzer die Bilder gleich mitgeliefert möchte, kannst du sie in eine .bento-Datei einbetten.

Unten steht ein vollständiges, importierbares Beispiel. Übernimm die Projektstruktur, ersetze Mustertexte, Farben, Kacheln und Positionen passend zum Auftrag. Dateiformat und Werkzeugparameter des MCP-Connectors unterscheiden sich.

```json
{
  "version": 2, "gridVersion": 1, "name": "Waldnotizen",
  "width": 1200, "height": 1200, "unit": "px", "cols": 4,
  "gap": 20, "radius": 32, "organic": true, "compact": false,
  "background": "#f1ead5", "gradient": false, "color2": "#e3b05e", "angle": 135,
  "shadow": false, "shadowColor": "#19271f", "shadowOpacity": 20,
  "shadowAngle": 145, "shadowDistance": 8, "shadowBlur": 16,
  "tiles": [
    {"id":"titel","type":"text","text":"Waldnotizen","color":"#fff1d3","backgroundColor":"#294f40","fontFamily":"Georgia","fontSize":128,"textAlign":"left","verticalAlign":"bottom","textPadding":38},
    {"id":"nummer","type":"text","text":"Heft 01","color":"#30271b","backgroundColor":"#ecb96b","fontSize":64},
    {"id":"akzent","type":"placeholder","backgroundColor":"#bd6746"}
  ],
  "layout": [
    {"i":"titel","x":0,"y":0,"w":4,"h":3},
    {"i":"nummer","x":0,"y":3,"w":3,"h":1},
    {"i":"akzent","x":3,"y":3,"w":1,"h":1}
  ]
}
```

## Format und Anordnung

- Speichere Breite und Höhe immer als ganze Pixel. Für A4 hochkant bei 300 dpi sind es 2480 × 3508 mit Anzeigeeinheit `"mm"`. Für Druckdokumente Platz für Seitenränder vorsehen. Für Pixelprojekte jede Seite 128–8192 px, höchstens 32 Millionen Pixel.
- Mit `gridVersion:1` zählt `cols` die kurze Seite. Erlaubt sind 4, 5, 8, 9, 16, 17, 24 und 25. Die lange Seite hat entsprechend dem Seitenverhältnis gerundet mehr Zellen (höchstens 256). Bei 1200 × 630 und `cols:4` ergibt das 8 Spalten × 4 Reihen.
- Eindeutige Kachel-IDs. Jede sichtbare Kachel benötigt einen Layout-Eintrag mit derselben ID unter `i`. Koordinaten starten oben links bei 0. Breite und Höhe sind positive ganze Zellzahlen. Rechtecke müssen ins Raster passen und dürfen sich nicht überlappen. Kacheln ohne Position liegen in der Reserve.
- Höchstens 625 Kacheln, davon höchstens 80 vom Typ `image` oder `imageText`. Maximaler Abstand `gap` in px: 0,6 × Minimum aus Breite/(Spalten+1) und Höhe/(Reihen+1).
- `background` ist der Canvas-Hintergrund. Für Verlauf `gradient:true`, zweite Farbe `color2` und Winkel `angle` (0–360). `radius` bestimmt die Ecken in px, `organic` die optische Rundung. Die Schatteneinstellungen aus dem Beispiel gelten projektweit. Farben als sechsstellige Hexwerte angeben, für durchscheinende Flächen ist auch `"transparent"` möglich.

## Druckränder und Beschnitt

Plane bei jedem Druckformat den Seitenrand passend zum Auftrag. Für Rechnungen, Briefe und andere Dokumente eignet sich ein gleichmässiger weisser Rand, bei A4 beispielsweise 10–15 mm. Halte Texte, Tabellen und Logos innerhalb dieser Fläche.

Bei randfüllenden Motiven reichen Hintergrundfarbe oder Hintergrundfoto bis an alle gewünschten Seitenkanten. Wichtige Texte und Logos bleiben mindestens 5 mm innerhalb der Schnittkante. Weise bei der Übergabe auf die Option für 3 mm Beschnitt im JPG-Export hin. Der Editor ergänzt den Beschnitt ausserhalb des Endformats. Alle Kacheln bleiben innerhalb des Rasters. Vermeide schmale, unbeabsichtigte Streifen an der Seitenkante.

Verwende für Druckprojekte `unit:"mm"` oder `unit:"in"`, damit die Druckoption im Export erscheint. Die gespeicherten Werte `width` und `height` bleiben Pixel bei 300 dpi. Ein Millimeter entspricht etwa 11,81 Pixeln. Beispielsweise ergeben 13 mm Sicherheitsabstand etwa 154 Pixel. Ein Vorlagenlink oder eine .bento-Datei enthält den editierbaren Entwurf; der Beschnitt entsteht beim anschliessenden Bildexport.

## Kacheln gestalten

- **Farbfläche:** `type:"placeholder"`, sichtbare Farbe in `backgroundColor`. **Text:** `type:"text"`, Inhalt in `text`, Schriftfarbe in `color`. **Bild:** `type:"image"`. **Bild mit editierbarem Text:** `type:"imageText"`. Jede Kachel kann mit `locked:true` gesperrt werden.
- **Textsatz:** `textAlign` = left/center/right, `verticalAlign` = top/center/bottom. `fontSize` 8–300 px ist die Obergrenze, `fontWeight` 100–1000, `textPadding` 0–300 px pro Seite, `lineHeight` 0.8–3. Der Editor verkleinert den Text, bis er passt. Plane für lange Texte ausreichend Fläche ein.
- **Schriftarten:** Arial, Times New Roman, Courier New, Georgia, Verdana, Tahoma, Trebuchet MS, Impact, Roboto, Open Sans, Lato, Montserrat, Oswald, Raleway, Poppins, Nunito, Merriweather, Inter, Playfair Display, Quicksand, Source Sans Pro, Work Sans, Rubik, Fira Sans, Cabin, Muli, Bebas Neue, PT Sans, Josefin Sans, Ubuntu, Kanit, Barlow, Mukta, Archivo, Manrope, Heebo, Signika, Comic Neue, Indie Flower, Permanent Marker, Pacifico, Amatic SC, Shadows Into Light, Caveat, Architects Daughter, Dancing Script, Lobster, Abril Fatface, Great Vibes, Orbitron, Share Tech Mono, VT323, Major Mono Display, Bungee, Monoton, Audiowide.
- **Einzelne Wörter:** Beispiel für „Heft 01“: `"textRuns":[{"start":5,"end":7,"weight":700,"scale":1.2,"color":"#603123","fontFamily":"Georgia"}]`. Geordnete, überlappungsfreie Bereiche in UTF-16, Ende exklusiv. Relative Grösse `scale` 0.1–4 (10–400 %). Im Bereich heisst die Stärke `weight`.
- **Texthinterlegung** für die Kachel oder einen einzelnen Textbereich: `textBackdrop:true`, `textBackdropColor`, Höhe `textBackdropStrength` 10–200 %, `textBackdropOpacity` 0–100 %, `textBackdropPadding` und `textBackdropRadius` jeweils 0–150 px.
- **Kontur** projektweit oder individuell pro Kachel: `"contour":{"enabled":true,"automatic":false,"color":"#325367","width":3,"opacity":85}`. Breite 0–100 px, Deckkraft 0–100 %. Individuelle Konturen haben Vorrang.
- **Bilddaten:** Verwende echte Bilddateien. Setze `src` auf eine Data-URL mit korrektem MIME-Typ und Base64-Inhalt (PNG, JPEG, WebP, GIF oder AVIF), `name` auf den Bildnamen. Python-Beispiel für ein JPEG: `"data:image/jpeg;base64," + base64.b64encode(Path("foto.jpg").read_bytes()).decode("ascii")`. Mehrere Motive als getrennte Bildkacheln einbauen. Wenn ein Bild fehlt, kennzeichne einen Platzhalter.
- **Bildausschnitt und Wirkung:** `zoom:1` entspricht 100 %, für PNGs bis 0.05 verkleinerbar, maximal 5. `cropX` und `cropY` reichen von 0 bis 1 (Mitte 0.5), `imageRotation` 0–360 Grad, `imageTone` −100 bis +100, `imageGrayscale` 0–100, `imageColorLimit` 0 (Original), 16, 8, 4 oder 2. `imageBackground:true` zeigt die Kachelfarbe hinter transparenten Bildteilen.
- **Hintergrundfoto:** Auf Projektebene `backgroundImage` mit `enabled:true`, `src`, `name` und denselben Ausschnitt- und Wirkungsfeldern setzen. Durch leere Zellen, Kachelabstände und transparente Flächen sichtbar.
- **Bestehende Projekte:** Bewahre beim Bearbeiten IDs, Bilder und nicht angeforderte Eigenschaften. Bei Kalendern gehören auch `calendar.months` (zwölf Monatsinhalte) und gegebenenfalls `calendar.designs` (individuelle Monatsgestaltungen) zum Projekt. Verwende beim Bearbeiten eines vorhandenen Kalenders dessen Rollen, Monatsstruktur und Kachel-IDs.

## Ausgabe mit Python

Das Beispiel erwartet den fertigen Entwurf als Dictionary `project`. Für eine Datei kannst du Bilder in `src` einbetten. Falls du Fotos verlinkst, übernimm ihre öffentlichen HTTPS-Bildadressen einschliesslich der Abfrageparameter. Das Erstellen des Links erfordert keinen Bildabruf. Zum Laden im Editor muss die Bildadresse JPG, PNG oder WebP direkt ausliefern, ohne Anmeldung oder Weiterleitung und mit CORS-Freigabe für den Editor. Es gelten 25 MB und 40 Megapixel je Bild. Bei gesperrtem Browserzugriff kann der Benutzer das Bild als Datei auf der Ablagefläche ablegen. Verwende nur Bilder, die du für deinen Zweck nutzen darfst.

```python
# Optional für den Beispielentwurf oben. Setze nur gewünschte Bildquellen ein.
tile_photo_url = None
background_photo_url = None
if tile_photo_url:
    project["tiles"][2].update(type="image", src="", name="Foto", sourceUrl=tile_photo_url)
if background_photo_url:
    project["backgroundImage"] = {"enabled": True, "src": "", "name": "Hintergrund", "sourceUrl": background_photo_url}
```

```python
import base64
import gzip
import json
from pathlib import Path

payload = json.dumps(project, ensure_ascii=False, separators=(",", ":"), allow_nan=False).encode("utf-8")
Path("entwurf.bento").write_bytes(payload)

# Für einen Direktlink mit öffentlichen Bildquellen oder Bildplätzen:
def contains_image(value):
    if isinstance(value, dict):
        return bool(value.get("src")) or any(contains_image(v) for v in value.values())
    return isinstance(value, list) and any(contains_image(v) for v in value)

if not contains_image(project):
    code = base64.urlsafe_b64encode(gzip.compress(payload)).decode("ascii").rstrip("=")
    print("https://www.bentoguru.com/#template=GZ1-" + code)
```

Prüfe vor der Übergabe die IDs, Rastergrenzen, überlappungsfreie Platzierung, Farben, Texte und Bildquellen. Gib den tatsächlich erzeugten Dateianhang oder den vollständig berechneten, anklickbaren Direktlink aus. Wenn du weder Dateien erzeugen noch Code ausführen kannst, sage das offen. Falls die Anleitung nicht per URL abrufbar ist, bitte den Benutzer, sie als Datei anzuhängen.

Bilddeckkraft: `imageOpacity` steuert nur die Bildebene von Bildkacheln, Bild-&-Text-Kacheln und `backgroundImage`: 0 bis 100 Prozent, Standard 100. Text, Kontur und Kachelfarbe bleiben unverändert.
