# BB-Trainer – Hinweise für Claude

Persönliche Trainings-App (PWA) für den Präsenztest im Auswahlverfahren der Deutschen Bundesbank
(duales Studium Zentralbankwesen, **Test am 23.11.2026 in Berlin**). Vanilla-JS-ES-Module **ohne Build**,
Deploy über GitHub Pages (`.github/workflows/pages.yml`). Antworten an den Nutzer auf Deutsch.

## Regeln
- **Keine Originalaufgaben** aus dem Online-Test (PERLS/eligo) übernehmen – nur eigene Aufgaben im gleichen Format. Die App darf nicht behaupten, Originalaufgaben zu enthalten.
- **Mathe ist Schwerpunkt** (das Online-Ergebnis in Zahlen ist nicht aussagekräftig). Lösungen immer Schritt für Schritt an den konkreten Zahlen erklären, ohne Taschenrechner lösbar.
- Inhalte der Fragenbanken müssen eindeutig genau eine richtige Antwort haben – im Zweifel weglassen.
- Code und Kommentare Englisch, Oberfläche und Lösungswege Deutsch.

## Arbeitsablauf
- Bei jeder Änderung: `VERSION` in `sw.js` erhöhen (`bbt-vN`), neue Dateien in `DATEIEN` aufnehmen.
- Vor dem Push: `node --test tests/*.test.mjs`. Screenshots hell und dunkel (430 px) prüfen: keine JS-Fehler, kein horizontaler Überlauf.

## Aufbau
- Module wie im Ergebnisbericht: **Verarbeitungsgeschwindigkeit** (`js/vg.js`: Formen-Gleichungen, Legende 1–9 unten links, wechselt je Aufgabe), **Angewandtes Schlussfolgern** (`js/logik.js`: Szenarien listen alle möglichen Fälle, richtig/unbestimmt/falsch wird **berechnet**), **Umgang mit Zahlen** (`js/zahlen.js`: seed-basierte Generatoren, Stufen 1–3, inkl. Ableitungen und Ableitungsgraphen als SVG), **Englisch** (`js/englisch.js`: Sätze ergänzen, Satzbau und Verstehen, Lückentext, Texte zuordnen).
- `js/typen.js` – Registry (`erzeuge(typ, seed, stufe, idx)` reproduzierbar, Zielzeiten), Einstiegstest (8 feste Aufgaben).
- `js/speicher.js` – localStorage `tt.stat.v1`: Statistik je Typ und Tag, Fehlerprotokoll (Seeds), Lernkartei je Typ (falsch oder zu langsam → Fach 1), Export/Import JSON.
- `js/plan.js` – Phasen (Verstehen bis 9.11., Tempo bis 16.11., Simulation bis 21.11.), Tagesplan: Einstiegstest zuerst, täglich Mathe (`MATHE_ZYKLUS`, ab 17.11. schwächster Mathetyp) + Formen-Sprint, Wechsel Schlussfolgern/Englisch, sonntags Simulation.
- `js/app.js` – gesamte UI (`render()`, Aktionen über `data-a`/`data-v`, Map `AKTIONEN`), Sitzungen aus Blöcken (Zeitmodus keine/aufgabe/block/sprint).
- Design: `css/style.css` stammt aus dem Finanzwirt-Trainer (Glas, Leuchten, 3D-Knöpfe; Farbe `--m` je Modul, per JS gesetzt), eigene Komponenten in `css/tt.css`. Farben nur über Variablen, hell **und** dunkel prüfen.
