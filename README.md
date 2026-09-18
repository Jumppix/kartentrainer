# Kartenpalast

Gedächtnistraining für Skat: ein Adressen-Palast mit 32 festen Plätzen — vier
Räume à acht Punkte, jeder Ort dauerhaft einer Karte zugeordnet (Regal =
Kreuz-9, für immer). Kernübung ist die Negativabfrage: „Ist Karo-10 schon
gespielt?“

**Live:** <https://jumppix.github.io/kartentrainer/>

Eine einzige Datei, `index.html`. Kein Build, keine Abhängigkeiten, läuft
offline. Über „Zum Home-Bildschirm“ verhält sie sich wie eine App.

## Aufbau

| Raum | Farbe | Index |
|------|-------|-------|
| 1 | ♣ Kreuz | 0–7 |
| 2 | ♠ Pik | 8–15 |
| 3 | ♥ Herz | 16–23 |
| 4 | ♦ Karo | 24–31 |

Wertreihenfolge je Raum: 7, 8, 9, 10, J, D, K, A.

Die sechs Stufen (Rohbau, Route, Zuordnung, Markieren, Tempo, Rotation) lassen
sich jederzeit in beliebiger Reihenfolge öffnen. Ist der Palast noch nicht
vollständig, heißen die leeren Plätze in den Übungen „Punkt 1“ bis „Punkt 32“.

## Daten über GitHub synchronisieren

Palast, Fortschritt und Farbfilter liegen als JSON-Datei im Repo
(Standard: `kartenpalast.json`). Auf einem neuen Gerät genügt es, die Seite zu
öffnen — die Daten werden von dort geladen. Ohne Einrichtung bleibt alles wie
bisher nur im Browser.

**Laden** braucht bei einem öffentlichen Repo nichts weiter. **Speichern**
braucht auf jedem Gerät einmalig einen Token:

1. [Fine-grained Token anlegen](https://github.com/settings/personal-access-tokens/new)
2. *Repository access* → **Only select repositories** → dieses Repo
3. *Permissions* → *Repository permissions* → **Contents: Read and write**
4. In der App: **GitHub-Sync** → Token einfügen

Danach speichert die App fünf Sekunden nach der letzten Änderung von selbst,
außerdem beim Verlassen der Seite. Owner und Repository werden aus der
Pages-Adresse vorausgefüllt.

Der Token liegt ausschließlich im `localStorage` des jeweiligen Geräts. Er wird
nie in die JSON-Datei geschrieben und nie irgendwohin außer an `api.github.com`
geschickt. „Token auf diesem Gerät löschen“ entfernt ihn wieder; Laden
funktioniert danach weiter, Speichern nicht mehr.

### Wenn zwei Geräte auseinanderlaufen

Liegt im Repo eine neuere Version, fragt die Übersicht nach — **Laden** oder
**Diese behalten** — und speichert bis zur Entscheidung nichts automatisch
hoch. Kommt eine Änderung erst während der Sitzung dazu, fragt die App vor dem
Überschreiben nach.

### Privatsphäre

In einem öffentlichen Repo kann jeder die Datei lesen, also auch die eigenen
Orte. Wer das nicht möchte, legt ein privates Repo an und trägt es unter
GitHub-Sync ein; mit Token liest die App auch daraus.

## Speicher

| Schlüssel | Inhalt |
|-----------|--------|
| `kp.palace` | Räume, 32 Punkte, „laut vorgelesen“-Flag |
| `kp.prog` | Ergebnis je Stufe |
| `kp.s3suits` | Farbfilter Stufe 3 |
| `kp.meta` | Zeitstempel für den Abgleich |
| `kp.gh` | Repo, Branch, Dateiname, Token |

`kp.gh` wird nie hochgeladen.
