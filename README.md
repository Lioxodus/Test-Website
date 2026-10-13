# Future Oche League – kostenlose GitHub-Pages-Version

## Hochladen

Alle Dateien aus diesem Ordner **direkt in das Stammverzeichnis** deines GitHub-Repositories legen. Wichtig: `index.html` muss direkt oben liegen (nicht in einem Unterordner). Bei GitHub Settings → Pages → Deploy from a branch → `main` / `(root)`.

## Google Sheets

Die Website ist mit dieser Tabellen-ID vorbereitet:
`1ErtkV6jN19yiBiKr7o4zxcgZYEWMcscXVXxk0NdTMw8`

**Wichtig:** Die derzeitige Verbindung liest CSV aus dem **ersten Tabellenblatt (gid=0)**. Falls deine Sheet-Daten in einem anderen Tab liegen, in `app.js` den `gid=0`-Wert auf die ID dieses Tabellenblatts ändern (sie steht im Google-Sheets-Link nach `#gid=`). Stelle das Blatt für lesenden Zugriff bereit. Nur Daten, die öffentlich sichtbar sein dürfen, dort ablegen. Wenn Sheets den CSV-Zugriff nicht erlaubt, das betreffende Blatt alternativ unter Datei → Teilen → Im Web veröffentlichen als CSV veröffentlichen und dessen CSV-URL in `app.js` als `CSV_URL` eintragen. Die öffentliche URL kann von jedem abgerufen werden.

Eine Tabelle, Spalten **A–I** exakt:
`Spieltag | Zeitraum | Plattform | Liga | Spieler A | Spieler B | Leg A | Leg B | Status`

`Plattform=Autodarts`, `Liga=1,2,3,4`. Ein Match zählt nur bei `Status=Gespielt` oder `Bestätigt`, gültigen ungleichen Zahlen als Leg-Ergebnis und mindestens einem gewonnenen Leg. **Keine** automatische Ergebnisübermittlung oder Admin-Logins implementiert; Verwaltung erfolgt ausschließlich direkt in Google Sheets.

Die Tabelle wird dynamisch aus eingetragenen Begegnungen aufgebaut. Zwei Punkte je Sieg, danach Sortierung nach Siegen, Leg-Differenz und gewonnenen Legs. Alle Begegnungen (auch offene) führen zum Eintrag der beteiligten Spieler in der Tabelle.

## Inhalte

`index.html`, `tabellen.html`, `spieltage.html`, `ergebnisse.html`, `turniere.html`, `news.html`, `regeln.html`: eigene HTML-Seiten. `app.js`: Datenanbindung, Navigation und Tabellenrechnung. `style.css`: responsives Layout. `logo.png`: Original-Logo.

Turniere und News sind vorerst Informationsseiten ohne erfundene Daten. Derzeit kein Formular, keine Spielerprofile, keine Benutzerkonten. Für die spätere Übergabe muss der neue Betreiber Zugriff auf das Google Sheet und Repository erhalten; keine Passwörter in die Website schreiben.
