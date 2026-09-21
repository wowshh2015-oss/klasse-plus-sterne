# Klasse: Plus und Sterne

Einfacher Belohnungs-Tracker für die Grundschule. Eine Datei `index.html` — ohne Installation und ohne Server.

**Ein-Bildschirm-Raster:** Alle **19 Schüler** ohne Scrollen im Grid — ideal im **Querformat** (ca. 5×4) auf Tablet/Beamer. Plus-/Minus-Slots skalieren mit der Kartenhöhe. Button **Vollbild** füllt den Bildschirm (Chrome/Edge/Safari).

Live (GitHub Pages): https://wowshh2015-oss.github.io/klasse-plus-sterne/

## Öffnen (Tablet / Beamer)

1. Öffne die Pages-URL oder lokal **`index.html`** in **Chrome**, **Edge** oder **Safari**.
2. **Querformat** bevorzugen (10″-Tablet oder 1280×800). Hochformat: App versucht 4/3 Spalten; bei sehr schmalen Displays ggf. nicht alles ohne Zoom — dann Querformat + **Vollbild**.
3. Einmal **«Mikrofon erlauben»** tippen — danach merkt sich der Browser die Erlaubnis möglichst dauerhaft.
4. Optional **«Vollbild»** tippen (Label wechselt zu «Vollbild beenden»).

> **Hinweis zu `file://`:** Unter `file://` bleibt die Mikrofon-Erlaubnis oft **nicht** gespeichert. Empfohlen: lokalen Server (`python3 -m http.server 8080`) oder die Pages-URL.

### Spracherkennung — Browser-Hinweis

- **Am besten:** Chrome oder Edge auf **Android-Tablets**, bzw. Chrome auf **iPadOS** (falls verfügbar).
- **Safari auf dem iPad:** Web Speech oft eingeschränkt; Karten-Bedienung funktioniert trotzdem.
- **Einmal erlauben:** Button «Mikrofon erlauben» fragt `getUserMedia` einmal an.

## Layout & Vollbild

- Seite nutzt `100dvh`, Flex-Spalte; `#students` füllt den Rest (`flex: 1; min-height: 0; overflow: hidden`) — **kein Scrollen** im Schüler-Raster.
- Raster: typisch **5 Spalten × 4 Zeilen** (Querformat); Karten und Slots schrumpfen mit `minmax(0, 1fr)` / `aspect-ratio`.
- Kopfzeile kompakt: Datum, CSV, Klasse, Zurücksetzen, **Vollbild**; in Vollbild wird «＋ Schüler» ausgeblendet und Abstände weiter reduziert.
- Mikrofon-Leiste schwebt unten (leicht transparent), deckt keine Namen ab.

## Regeln (Plus, Minus & Sterne)

### Plus (3 × 5)

- Gute Arbeit → **+1 Plus** (nächster leerer Slot).
- Maximal **15 Plus** (3 Reihen à 5).

### Minus (unabhängig von Plus)

- **Minus** +1 — auch bei 0 Plus.
- Maximal **5 Minus** (1 Reihe à 5 unter Plus).
- Gedimmte Plus für `min(Plus, Minus)`; Extra-Minus bleiben in der Minus-Zeile sichtbar.

### Karten-Bedienung (Slots)

| Geste | Aktion |
|--------|--------|
| **Einfachklick** auf leeren Plus-Slot | +1 Plus |
| **Doppelklick** auf gefüllten Plus-Slot | −1 Plus |
| **Einfachklick** auf leeren Minus-Slot | +1 Minus |
| **Doppelklick** auf gefüllten Minus-Slot | −1 Minus |

Buttons **＋ / −** bleiben Shortcuts.

### Effektive Plus & Sterne

- **Effektive Plus** = `max(0, Plus − Minus)`.
- ≥ **5** → 1 Stern, ≥ **10** → 2 Sterne, ≥ **15** → 3 Sterne (können bei Minus wieder erlöschen).

### Zurücksetzen

- **Zurücksetzen:** Plus und Minus auf 0 (Namen bleiben).

## Datum & Klasse

- Kopf: aktuelles Datum (kurz, deutsch).
- Voreingestellt (19, A–Z): Aian, Amara, Amer, Andre, Bella, Ceren, Clara, Emmi, Khalil, Leo, Mina, Mostafa, Mussa, Noura, Patricia, Rose, Sanna, Shantal, Valeriia.
- **Klasse** lädt die Liste neu (Zähler null).

## Sprachbefehle (Deutsch, `de-DE`)

1. **«Mikrofon erlauben»**, dann 🎤 halten oder tippen.
2. z. B. «Amer plus», «Bella plus», «Khalil Minus» — mehrere Befehle in einem Halten möglich.

Daten: `localStorage` Schlüssel `classroom-plus-v8` (ältere v7/v6/v5 werden migriert; Plus auf max. 15, Minus auf max. 5 geklemmt).

## Bedienung

| Taste | Aktion |
|--------|--------|
| Vollbild | An/Aus (`requestFullscreen` auf `<html>`) |
| ＋ Schüler | Hinzufügen (in Vollbild ausgeblendet) |
| CSV | Export `Name;Plus;Minus;EffektivePlus;Sterne` |
| Klasse | Die 19 Namen (Zähler null) |
| Zurücksetzen | Plus/Minus null |

## Dateien

- `index.html` — gesamte App (CSS + JS)
- `README.md` — diese Anleitung
