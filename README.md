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


## Abschlussversion: Datenschutz und Impressum

Neue Seiten: `impressum.html`, `datenschutz.html`. Beide sind von jeder Seite im Footer erreichbar. **Wichtig: Die orange markierten Platzhalter müssen vor einem regulären öffentlichen Betrieb durch die echten Betreiberangaben ersetzt werden.** Die Datenschutzhinweise sind ein Ausgangspunkt und müssen anhand der echten Verhältnisse geprüft werden. Insbesondere öffentliche Spielernamen, Ergebnisse und die Übertragung beim Google-Sheets-Abruf müssen berücksichtigt werden.

Die Logik für Tabellen, Punkte und Spieltage wurde gegenüber der zuvor getesteten Version nicht geändert. Externe Google-Fonts wurden entfernt; Schriftarten sind jetzt lokal verfügbare Systemschriften.

### Vor Übergabe / Veröffentlichung prüfen

- Betreiberangaben vollständig und rechtlich passend ausgefüllt; optional rechtlich prüfen lassen.
- Spieler über die öffentliche Veröffentlichung ihrer Namen/Ergebnisse informieren; Rechtsgrundlage prüfen.
- Alle Unterseiten, Tabellen, Spieltage und mobile Navigation erneut prüfen.
- Website, GitHub-Repository und Google Sheet mit dem tatsächlichen Betreiber abstimmen.
- Keine persönlichen Zugangsdaten, privaten Sheet-URLs oder Secrets im Repository hinterlegen.
- Bei neuen Funktionen (Formulare, Analytics, eingebettete Dienste) Datenschutzhinweise erneut prüfen.

### Pflege

- `app.js`: Google-Sheets-ID, Berechnungen, Seiteninhalte und Navigation.
- `style.css`: Farben, Abstände, Mobilansicht.
- `logo.png`: Logo links oben.
- HTML-Dateien: jeweiliger Seiten-Einstieg; sie verwenden gemeinsame Styles und Funktionen.

**Keine Garantie für rechtliche Vollständigkeit:** Angaben zum Betreiber und besondere Pflichten hängen vom realen Betrieb ab.


## Version 3 – fünf Ligen und Regeln
- **Fünf** Ligen (Werte `1`, `2`, `3`, `4`, `5` in Google Sheets Spalte D); keine zusätzlichen Tabellenblätter erforderlich.
- Neue 5. Liga erscheint auch ohne Einträge; zunächst ist die Tabelle entsprechend leer.
- Ligapunkte: **3 für einen Sieg**, 0 für eine Niederlage; ein Unentschieden ist im regulären First-to-6-Format nicht möglich.
- Sichtbare Footer-Links zu `impressum.html` und `datenschutz.html` auf jeder Seite. Vor öffentlichem Regelbetrieb müssen deren Platzhalter mit den tatsächlichen Betreiberangaben befüllt und geprüft werden.
- Die Autodarts-Regeln stehen in `regeln.html` (HTML-Container); der Text wird in der `staticPage()`-Funktion in `app.js` eingefügt. Discord-Kanalnamen, die in der Vorlage fehlten, sind entsprechend als offen markiert.
- Zur Veröffentlichung **den INHALT dieses Ordners** ins Hauptverzeichnis des GitHub-Repositories kopieren, nicht den Ordner selbst. Danach GitHub Desktop → Commit → Push.

## Wartung
- Ligazahl: in `app.js` die Stellen `[1,2,3,4,5]` und `/^[1-5]$/` konsistent anpassen.
- Punktevergabe: `a.pts+=3` bzw. `b.pts+=3` in `table()`.
- Google-Sheets-ID steht am Anfang der Datei `app.js` in `SHEET_ID`.
- Impressum und Datenschutztexte werden über `legalPage()` in `app.js` angezeigt; die beiden HTML-Seiten sind über Footer-Links erreichbar.

## Discord
Der offizielle Discord-Einladungslink ist in `app.js` auf der Startseite und im Footer eingebunden: https://discord.gg/5jw43pMMqU. Beim Ändern des Einladungslinks beide Stellen aktualisieren.
