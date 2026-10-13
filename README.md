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


## Turniere verwalten (NEU)

**Kein Backend nötig, keine Website-Dateien für neue Turniere ändern.** Innerhalb der **bestehenden Google-Tabelle** zwei zusätzliche Tabellenblätter anlegen; die Blattnamen müssen **genau** `Turniere` und `Turnierspiele` lauten. Die beiliegenden Dateien `Turniere-Vorlage.csv` und `Turnierspiele-Vorlage.csv` enthalten die Spaltenüberschriften. Die Überschriften in Zeile 1 jeweils in eigene Zellen kopieren (nicht als einen einzigen Text).

**Tab `Turniere`:** `ID | Name | Datum | Status | Modus | Teilnehmer | Beschreibung`
- `ID`: kurze eindeutige Kennung, etwa `cup-2026`, nicht nachträglich ändern.
- `Status`: `Geplant`, `Anmeldung`, `Laufend` oder `Abgeschlossen`.
- `Modus`: beispielsweise `K.-o.`. **Der sichtbare Turnierbaum unterstützt derzeit nur K.-o.-Turniere**, keine Gruppenphase.
- `Teilnehmer`: 8, 16 oder 32 (optional 64). Das legt die Zahl der Turnierrunden fest.
- `Datum`: frei lesbare Datumsangabe.

**Tab `Turnierspiele`:** `Turnier ID | Runde | Spiel | Spieler A | Spieler B | Legs A | Legs B | Status`
- `Turnier ID` muss mit der ID im Tab `Turniere` übereinstimmen.
- `Runde`: 1 = Auftaktrunde, 2 = nächste Runde usw. Bei 8 Teilnehmern sind 1, 2, 3 die Runden; 3 ist das Finale.
- `Spiel`: die Matchnummer innerhalb der Runde, beispielsweise 1, 2, 3, 4.
- `Spieler A`, `Spieler B`: Namen. Noch nicht feststehende Spieler leer lassen.
- `Legs A`, `Legs B`: Ergebnis erst nach dem Match eintragen; einseitige Ergebnisse vermeiden.
- `Status`: `Offen` oder `Bestätigt` (auch `Gespielt` wird als bestätigt behandelt). **Nur bestätigte und gültige Ergebnisse werden hervorgehoben.**
- **Weiterkommen:** Nach dem Match trägt die Ligaleitung den Sieger in der nächsten Runde als Spieler A oder Spieler B ein. Die Website verändert keine Daten im Sheet und setzt keine Paarungen automatisch fest. So kann der Host die Begegnungen vollständig kontrollieren.

**Beispiel:** `cup-2026 | Future Cup | 24.10.2026 | Laufend | K.-o. | 8 | Saisonpokal` im Blatt `Turniere`. Im Blatt `Turnierspiele`: `cup-2026 | 1 | 1 | Spieler Eins | Spieler Zwei | 5 | 3 | Bestätigt`. Anschließend weitere Paarungen ergänzen. Die Detailseite ist über den Turnier-Button erreichbar, mit einer URL wie `turnier.html?id=cup-2026`.

Der Browser liest beide Blätter wie die Liga-Tabelle über die öffentlich lesbare Google-Sheets-CSV-Schnittstelle anhand des **Blattnamens** (nicht der gid). Wenn ein Blatt nicht geladen werden kann, erscheint eine verständliche Meldung statt erfundener Inhalte. Prüfe die öffentliche Leseberechtigung und exakte Tabnamen. Google kann bei manchen Freigabekonfigurationen die CSV-Ausgabe einschränken; in diesem Fall müssen die Blätter als CSV veröffentlicht werden und die URLs in `tournamentCSV()` angepasst werden.

### Einfacher Verwaltungsablauf
1. Neues Turnier: Im Tab `Turniere` eine Zeile ergänzen.
2. Auslosung/Spielplan: Im Tab `Turnierspiele` passende Begegnungen anlegen.
3. Ergebnis: Legs eintragen und `Status` auf `Bestätigt` setzen.
4. Nächste Runde: Sieger in die jeweiligen Folgebegegnungen eintragen.
5. Abschluss: Turnierstatus `Abgeschlossen` setzen. Die Website übernimmt alles nach dem erneuten Laden.

**Datenschutz:** Neue Teilnehmernamen werden öffentlich angezeigt; nur geeignete Daten veröffentlichen. **Nicht implementiert:** automatische Auslosung, Schreiben von der Website in die Tabelle, Spielerregistrierung oder eigenständige Ergebnisfreigabe durch Website-Admins.


## Aktualisierung: Zwei separat veröffentlichte Turnier-Tabellen

Die Turnierdaten kommen jetzt aus **zwei separaten, bereits im Web veröffentlichten Google Sheets** und nicht mehr aus zwei Tabs derselben Liga-Datei. Die Links sind am Anfang von `app.js` unter `TOURNAMENT_CSV_URLS` hinterlegt.

- `Turniere`: https://docs.google.com/spreadsheets/d/e/2PACX-1vTUR8lQ-aONlLrRKNH15Y4IybaskuOwgDRoCnfT_5DhmMKBXwD6ZlGQws3CqEGNlpnxPGtVOaCffb0P/pubhtml
- `Turnierspiele`: https://docs.google.com/spreadsheets/d/e/2PACX-1vQlZLxmxit_Y7lzArLmKSFUPpHbfuq9j9xx5YP8_2P0g105wRF5Vq_5yy32KdmzRIjeeAbkriWuNKzN/pubhtml

**Wichtig:** Die ältere Anleitung unter „Turniere verwalten“ ging noch von zwei Tabs der bestehenden Liga-Datei aus. Dies gilt für diese Version nicht mehr. Die Spaltenüberschriften aus den beigefügten CSV-Vorlagen werden weiterhin benötigt. In den Veröffentlichungseinstellungen von Google Sheets sicherstellen, dass die **Daten bei Änderungen automatisch erneut veröffentlicht** werden. Eine `pubhtml`-Adresse wird für den CSV-Abruf als `/pub?output=csv` verwendet. Prüfe die beiden URLs nach dem Upload direkt im Browser: Es müssen CSV-Zeilen und keine HTML-Fehlerseite kommen. Die Live-Erreichbarkeit und die tatsächlichen Spalten konnten in dieser Umgebung nicht verifiziert werden.

Die bisherige Liga-Sheet-ID und alle fünf Ligatabellen bleiben unverändert.
