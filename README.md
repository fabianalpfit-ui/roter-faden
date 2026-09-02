# Roter Faden

Ein Fortschritts-Tracker für den Aufbau eines YouTube-Kanals. Eine Seite, kein Build, keine Abhängigkeiten, keine Konten.

Der Faden läuft senkrecht durch alle Aufgaben. Hinter dir ist er dunkelrot, vor dir grau. Antippen hakt ab.

## Was drin ist

- Fortschritt bleibt auf dem Gerät gespeichert
- Notiz zu jedem Punkt
- Termine als `.ics` — öffnet in Apple Kalender, Google Kalender und Outlook, ohne Anbieter
- Sicherung als JSON exportierbar
- Läuft offline, auch beim Kaltstart

## Aufs Handy

1. Über GitHub Pages veröffentlichen: **Settings → Pages → Source: main / root**
2. Die Adresse auf dem Handy öffnen
3. **Teilen → Zum Home-Bildschirm**

Danach startet sie ohne Browserleiste, mit eigenem Icon.

## Lokal ansehen

Direkt per Doppelklick geht, aber der Service Worker braucht einen Server:

```bash
python3 -m http.server 8080
# http://localhost:8080
```

## Aufbau

| Datei | Zweck |
|---|---|
| `index.html` | Die gesamte App — Struktur, Gestaltung, Logik |
| `sw.js` | Service Worker für den Offline-Betrieb |
| `manifest.webmanifest` | Name, Farben, Icon für den Homescreen |
| `icon.svg` | Das Icon |

## Aufgaben ändern

Die Liste steht in `index.html` in der Konstante `PLAN`. Aufbau:

```js
{ id: "1.2.3",                      // eindeutig, nie nachträglich ändern
  t:  "Aufgabe im Klartext",
  cal: "Titel für den Kalender",    // optional, blendet "Termin setzen" ein
  who: "Jarvis",                    // optional, kleines Etikett
  flag: true }                      // optional, roter Hinweis
```

**Die `id` ist der Schlüssel zum gespeicherten Fortschritt.** Wer sie nachträglich ändert, setzt den Haken dieses Punkts auf allen Geräten zurück. Text ändern ist unbedenklich, `id` ändern nicht.

## Nach jeder Änderung

Die Versionsnummer in `sw.js` erhöhen:

```js
const CACHE = "roter-faden-v2";
```

Sonst zeigen bereits installierte Geräte weiter die alte Fassung. Das ist der häufigste Fehler bei dieser Bauform.
