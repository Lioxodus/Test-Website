# Future Oche League – MVP

Lauffähige mehrseitige Community-Website mit eigener lokaler SQLite-Datenbank, ohne externe npm-Abhängigkeiten.

## Start

Benötigt **Node.js 22.13+**.

```bash
cd future-oche-league
npm start
```

Browser: http://localhost:3000

## Administrator einrichten

Es gibt bewusst **keinen bekannten Standard-Admin und kein Admin-Passwort im Quellcode**.
1. Regulär ein Konto über `/registrieren` erstellen.
2. Server beenden.
3. Im Projektordner folgenden Befehl ausführen, wobei die registrierte E-Mail-Adresse angepasst wird:

```bash
node -e "const {DatabaseSync}=require('node:sqlite');const d=new DatabaseSync('league.sqlite');console.log(d.prepare('UPDATE users SET role=? WHERE email=?').run('admin','DEINE-EMAIL@BEISPIEL.DE'))"
```

4. Server starten, anmelden und `/admin` öffnen.

## Seiten

`/` Startseite, `/rangliste`, `/spieler`, `/spieler/:slug`, `/liga`, `/turniere`, `/ergebnisse`, `/ergebnis-melden`, `/community`, `/informationen`, `/registrieren`, `/anmelden`, `/mein-profil`, `/admin`.

## Resultat-Workflow

Registrierter Spieler meldet ein eigenes Match gegen einen anderen registrierten Spieler. Es wird mit `pending` gespeichert und erscheint nur unter seinen eigenen Meldungen und im Admin-Panel. Admin kann bestätigen oder ablehnen. Nur `approved`-Resultate erscheinen öffentlich und beeinflussen Sieg/Niederlage/Punkte. Die vorläufige Punkteberechnung lautet 3 Punkte je Sieg und muss mit dem Liga-Regelwerk abgestimmt werden.

## Einschränkungen vor öffentlichem Produktivbetrieb

- Derzeit keine Autodarts-API-Verknüpfung oder automatische Verifikation. Das Autodarts-Feld ist eine frei angebbare Profilinformation.
- Kein E-Mail-Verifikations-/Passwort-Reset-System, keine Ratenbegrenzung und keine Audit-Historie für Admin-Aktionen; diese müssen vor öffentlichem Einsatz ergänzt werden.
- Keine fertige Rechts-/Datenschutz-/Impressum-Seite: Pflichtinformationen und Verantwortlichkeiten ergänzen.
- Moderation kann eine Einreichung bestätigen oder ablehnen, aber keine eigenen Matches korrigieren. Wettbewerbsstruktur, Spielplan, genaue Wertung und Zulassung müssen konfiguriert werden.
- Ergebnis-Einreichungen mit Links sind keine fälschungssicheren Beweise. Regelwerk und Verifikationsstandard ausarbeiten.
- Für öffentliche Bereitstellung HTTPS, `COOKIE_SECURE=1`, sicheren Reverse Proxy, Backups und Datenbank-Zugriffsschutz konfigurieren.
- Google-Font-Import durch selbst gehostete System-/Lizenzschriften ersetzen, falls Datenschutzanforderungen dies erfordern.

## Datenbank

`league.sqlite` wird beim ersten Start lokal automatisch angelegt. Keine Spieler oder Ergebnisse werden erfunden.
