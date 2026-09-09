# Klasse: Plus und Sterne

Einfacher Belohnungs-Tracker für die Grundschule. Eine Datei `index.html` — ohne Installation und ohne Server.

**Kompaktes Klassenraster:** Alle 19 Schüler auf **einem Bildschirm** (Tablet Querformat ideal: 5 Spalten; Hochformat ca. 3–4 Spalten). Kleine Karten, enger Abstand, schwebende Mikrofon-Leiste unten.

## Öffnen (Tablet)

1. Öffne **`index.html`** in **Google Chrome**, **Microsoft Edge** oder **Safari** auf dem Tablet.
2. Einmal **«Mikrofon erlauben»** tippen (Warm-up) — danach merkt sich der Browser die Erlaubnis möglichst dauerhaft.
3. Funktioniert **offline** nach dem Öffnen; Daten liegen im Browser (`localStorage`, Schlüssel `classroom-plus-v6`).

> **Hinweis zu `file://`:** Unter `file://` bleibt die Mikrofon-Erlaubnis oft **nicht** gespeichert (erneute Abfrage möglich). Empfohlen: lokalen Server starten, z. B.  
> `python3 -m http.server 8080`  
> und `http://localhost:8080/` öffnen. Der Mikrofon-Button bleibt trotzdem nutzbar.

### Spracherkennung — Browser-Hinweis

- **Am besten:** Chrome oder Edge auf **Android-Tablets**, bzw. Chrome auf **iPadOS** (falls verfügbar).
- **Safari auf dem iPad:** Die Web Speech API ist oft nur eingeschränkt oder gar nicht nutzbar. Die Plus-/Minus-Tasten auf den Karten funktionieren trotzdem immer.
- **Einmal erlauben:** Button «Mikrofon erlauben» fragt `getUserMedia` einmal an; erst danach startet die Spracherkennung (kein Dialog mitten im Halten).

## Regeln (Plus, Minus & Sterne)

### Plus (3 × 5)

- Gute Arbeit → **+1 Plus** (füllt den nächsten leeren Slot).
- Maximal **15 Plus** pro Schüler, dargestellt als **3 Reihen à 5 Felder**.

### Minus (eigene Zeile)

- **Minus** erhöht den Minus-Zähler um 1.
- Minus darf **nicht über Plus hinausgehen**: bei 0 Plus wirkt Minus nicht (Toast). Bei z. B. 7 Plus sind höchstens 7 Minus möglich.
- Visuell: eine **Minus-Zeile** mit −-Symbolen unter dem Plus-Raster.
- Die ersten *n* gefüllten Plus-Slots werden bei *n* Minus **storniert** (gedimmt / durchgestrichen). Die übrigen gefüllten Plus bleiben **aktiv** (hell).
- Beispiel: **7 Plus + 3 Minus** → 3 Plus storniert, **4 Plus aktiv**.

### Effektive Plus & Sterne (können erlöschen)

- **Effektive Plus** = Plus − Minus (mindestens 0).
- Sterne werden aus den effektiven Plus **abgeleitet** (nicht dauerhaft „gesammelt“):
  - effektiv ≥ **5** → 1 Stern
  - effektiv ≥ **10** → 2 Sterne
  - effektiv ≥ **15** → 3 Sterne
- Sinken die effektiven Plus durch Minus unter 5 / 10 / 15, **erlischt** der entsprechende Stern wieder (сгорает). Steigen sie erneut, kommen die Sterne zurück.

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

Auf der Karte: ＋ / −, Umbenennen ✏️, Entfernen 🗑️ (mit Bestätigung).

## Dateien

- `index.html` — gesamte App (CSS + JS darin)
- `README.md` — diese Anleitung
