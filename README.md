# rmnschwrz2.github.io
[app.md](https://github.com/user-attachments/files/33049445/app.md)
# Lokale App

Eine Datei: `dist/tablettenerinnerung.html`. Kein Server, kein Konto, keine Netzwerkaufrufe. Im Browser öffnen (Smartphone: Datei aufs Gerät laden und öffnen oder auf eigenem Webspace ablegen).

## Ablauf für Patienten

1. **Einrichten:** Medikamente eintragen (Name, Einnahme morgens/mittags/abends/nachts oder "nur bei Bedarf"), Bestand und Stückzahl pro Packung eintragen (beides Pflicht). Alternativ Medikationsplan (BMP-XML) einfügen.
2. **Heute:** Die App sagt, ab wann Tabletten fehlen, zeigt einen Zeitstreifen (grün: noch Zeit, gelb: Praxis melden, rot: knapp) und markiert Schätzungen.
3. **Packung abgeholt:** Pro Medikament einzeln "Wieder N Stück?" mit Ja oder Anders. Nie eine Sammelbestätigung.
4. **Tabletten gezählt:** Gesamtbestand pro Medikament. Korrigiert Abweichungen.
5. **In Kalender speichern:** `.ics`-Datei mit bis zu vier Terminen: „Praxis kontaktieren“ am Erinnerungstag und zwei Tage später, „Dringend: Praxis kontaktieren“ am spätesten Anfragetag und zwei Tage später. Folgetermine entfallen, wenn sie nicht vor der nächsten Stufe liegen. Ohne Medikamentennamen. Ändert sich der Rechenstand (Bestand, Abholung, Einnahme), zeigt „Heute“: „Ihr Kalendereintrag ist nicht mehr aktuell.“
6. **Versichertenkarte:** Der Kartenkasten auf „Heute“ fragt per Button („Karte ist eingelesen“ / „Noch nicht eingelesen“). Die Angabe gilt für das laufende Quartal. Liegt der Kontakt erst im nächsten Quartal, erscheint nur ein Hinweis. Korrigieren geht auch unter Einstellungen. Die App hält nur fest, was der Patient angibt.
7. **E-Mail vorbereiten:** Entwurf, `mailto:`-Link oder Text kopieren. Gesendet wird erst im E-Mail-Programm durch den Patienten.

## Technik

- `core.js` ist unverändert dieselbe Logik wie in n8n.
- `applib.js` enthält alle Funktionen ohne Oberfläche (in Node getestet).
- `app/app.html` ist die Oberfläche. Alle Texte aus Eingaben werden maskiert (`esc`).
- Speicher: localStorage, Schlüssel `tablettenerinnerung.v1`. Format wie die Sicherung (`app`, `version`, `patient`).
- Schrift: Atkinson Hyperlegible (SIL Open Font License, Datei `app/fonts/OFL-LICENSE.txt`), als Base64 eingebettet. Rückfall: Verdana.
- Bedienung: Schrift ca. 20 px, Schaltflächen mindestens 56 px, Status immer auch als Text, Dunkelmodus, Tastaturfokus sichtbar.

## Neu bauen und testen

```
npm run build
npm test
```

## Nächste Schritte

- Auf echten Geräten mit 3 bis 5 Personen testen (Lesbarkeit, Kalenderimport, Eingabe der Stückzahl).
- Als App verpacken (Capacitor) für lokale Mitteilungen.
- Offene Punkte: `docs/risiken_offene_punkte.md`.
