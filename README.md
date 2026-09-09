# Klasse: Plus und Sterne

Einfacher Belohnungs-Tracker für die Grundschule. Eine Datei `index.html` — ohne Installation und ohne Server.

**Kompaktes Klassenraster:** Alle 19 Schüler auf **einem Bildschirm** (Tablet Querformat ideal: 5 Spalten; Hochformat ca. 3–4 Spalten). Kleine Karten, enger Abstand, schwebende Mikrofon-Leiste unten.

## Öffnen (Tablet)

1. Öffne **`index.html`** in **Google Chrome**, **Microsoft Edge** oder **Safari** auf dem Tablet.
2. Einmal **«Mikrofon erlauben»** tippen (Warm-up) — danach merkt sich der Browser die Erlaubnis möglichst dauerhaft.
3. Funktioniert **offline** nach dem Öffnen; Daten liegen im Browser (`localStorage`, Schlüssel `classroom-plus-v7`; ältere v6/v5-Daten werden migriert).

> **Hinweis zu `file://`:** Unter `file://` bleibt die Mikrofon-Erlaubnis oft **nicht** gespeichert (erneute Abfrage möglich). Empfohlen: lokalen Server starten, z. B.  
> `python3 -m http.server 8080`  
> und `http://localhost:8080/` öffnen. Der Mikrofon-Button bleibt trotzdem nutzbar.

### Spracherkennung — Browser-Hinweis

- **Am besten:** Chrome oder Edge auf **Android-Tablets**, bzw. Chrome auf **iPadOS** (falls verfügbar).
- **Safari auf dem iPad:** Die Web Speech API ist oft nur eingeschränkt oder gar nicht nutzbar. Die Plus-/Minus-Tasten auf den Karten funktionieren trotzdem immer.
- **Einmal erlauben:** Button «Mikrofon erlauben» fragt `getUserMedia` einmal an; erst danach startet die Spracherkennung (kein Dialog mitten im Halten).

## Regeln (Plus, Minus & Sterne)

### Plus (2 × 5, größere Slots)

- Gute Arbeit → **+1 Plus** (füllt den nächsten leeren Slot).
- Maximal **10 Plus** pro Schüler, dargestellt als **2 Reihen à 5 Felder** (deutlicher Abstand zwischen den Reihen, große Tippfeldern).

### Minus (unabhängig von Plus)

- **Minus** erhöht den Minus-Zähler um 1 — **auch bei 0 Plus** (keine Obergrenze an Plus gekoppelt).
- Maximal **10 Minus**, ebenfalls **2 Reihen à 5** unter dem Plus-Raster.
- Visuell: Plus-Slots, die durch Minus storniert sind, bleiben **gedimmt** für `min(Plus, Minus)`. Wenn Minus > Plus, sind **alle** Plus gedimmt; die **zusätzlichen Minus** bleiben in der Minus-Zeile sichtbar.
- Beispiel: **2 Minus zuerst**, danach Plus → Minus zählen schon; später gefüllte Plus starten ggf. storniert, bis Minus ausgeglichen wird.

### Karten-Bedienung (Slots)

| Geste | Aktion |
|--------|--------|
| **Einfachklick** auf leeren Plus-Slot | +1 Plus |
| **Doppelklick** auf gefüllten Plus-Slot (aktiv oder storniert) | −1 Plus (`max(0, pluses−1)`) |
| **Einfachklick** auf leeren Minus-Slot | +1 Minus |
| **Doppelklick** auf gefüllten Minus-Slot | −1 Minus (`max(0, minuses−1)`) |

Die Karten-Buttons **＋ / −** bleiben Shortcuts zum Hinzufügen. Einfach- und Doppelklick greifen auf unterschiedliche Slot-Zustände (leer vs. gefüllt), damit sie sich nicht beißen.

### Effektive Plus & Sterne (können erlöschen)

- **Effektive Plus** = `max(0, Plus − Minus)`.
- Sterne werden aus den effektiven Plus **abgeleitet**:
  - effektiv ≥ **5** → 1 Stern
  - effektiv ≥ **10** → 2 Sterne
- Sinken die effektiven Plus durch Minus unter 5 / 10, **erlischt** der entsprechende Stern wieder. Steigen sie erneut, kommen die Sterne zurück.

### Zurücksetzen

- **Zurücksetzen** setzt bei allen Schülern **Plus und Minus auf 0** (Sterne erlöschen). **Namen bleiben.**

## Datum & Stunden

- Im Kopf steht das **aktuelle Datum** (kurz, deutsch) in einer Zeile mit den Steuerelementen.
- Zwischen Stunden: manuell **Zurücksetzen**.

## Klasse (Namen)

Voreingestellt (19 Kinder, A–Z): Aian, Amara, Amer, Andre, Bella, Ceren, Clara, Emmi, Khalil, Leo, Mina, Mostafa, Mussa, Noura, Patricia, Rose, Sanna, Shantal, Valeriia.

Button **Klasse** lädt diese Liste neu (Zähler auf null).

## Sprachbefehle (Deutsch, `de-DE`)

1. Einmal **«Mikrofon erlauben»** (in der Mikrofon-Leiste).
2. 🎤 **gedrückt halten** und nacheinander z. B. «Amer plus», «Bella plus», «Khalil Minus» sagen — mehrere Befehle in **einem** Halten (continuous).
3. Alternativ **kurz tippen** = Sitzung an/aus (praktisch auf Tablets).

Beispiele: «Bella plus», «Amer Plus», «Khalil Minus» / «Kalil minus».  
Aktionswörter: **plus**, **Minus** (sowie **Stern**/**Sternchen** → Plus). Der Name wird unscharf mit der Schülerliste verglichen.

**Namensabgleich:** Die App nutzt Aliase (z. B. Haiyan→Aian, Kalil→Khalil), phonetische Normalisierung und Levenshtein über bis zu 5 ASR-Alternativen; bei Korrektur erscheint kurz ein Toast «Haiyan» → Aian + Plus. Optional JSGF-Grammatik mit Klassennamen (Chrome oft ohne Wirkung).

## Bedienung

| Taste | Aktion |
|--------|--------|
| ＋ Schüler | Hinzufügen |
| CSV | Export `Name;Plus;Minus;EffektivePlus;Sterne` für Excel |
| Klasse | Die 19 Namen oben (Zähler null) |
| Zurücksetzen | Plus und Minus auf null (Namen bleiben) |

Auf der Karte: Tippen auf leere Plus-/Minus-Slots, Doppelklick auf gefüllte Slots zum Entfernen; Buttons ＋ / − als Shortcuts; Umbenennen ✏️, Entfernen 🗑️ (mit Bestätigung).

## Dateien

- `index.html` — gesamte App (CSS + JS darin)
- `README.md` — diese Anleitung
