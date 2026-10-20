# Gruppenrotation

Browser-Werkzeug für Kleingruppeneinteilungen in Seminaren und Ausbildungsmodulen. Es teilt Teilnehmende so in Gruppen ein, dass möglichst viele neue Paarungen entstehen und niemand zu oft mit denselben Personen zusammensitzt – über einzelne Tage und über mehrere Module hinweg.

Die gesamte Anwendung ist eine einzige Datei (`gruppenrotation.html`). Sie braucht keinen Server, keine Datenbank und keine Installation.

## Funktionen

- Teilnehmerliste einlesen: Anwesenheitsliste aus dem Portal als PDF, als CSV-Datei oder per Kopieren und Einfügen
- Anwesenheit pro Tag aus der Liste übernehmen und vor Ort per Antippen korrigieren
- Gruppen nach Gruppenzahl oder Gruppengröße einteilen, mit möglichst wenigen Wiederbegegnungen
- Vorschau mit Handumstellung (tauschen und verschieben), andere Varianten auswürfeln
- Sperrpaare: zwei Personen werden nie in dieselbe Gruppe gesetzt
- Runden mit Datum und Uhrzeit speichern, nachträglich bearbeiten oder löschen
- Begegnungsmatrix mit Farbstufen relativ zum üblichen Wert
- Mehrere Module: neue Liste einlesen, Namen werden abgeglichen, Historie bleibt erhalten
- Spitznamen und wählbares Namensformat (wie in der Liste, Vorname Nachname, nur Vorname)
- Druckansicht im INeKO-Stil mit Logo und Fußzeile
- Sicherung als JSON-Datei speichern und wieder laden
- Neue Gruppe beginnen: alle Daten löschen, auf Wunsch mit Sicherung vorab

## Betrieb

**Auf einem Webspace:** `gruppenrotation.html` hochladen und im Browser aufrufen. Wer die Seite direkt unter der Domain erreichen will, benennt sie in `index.html` um. Jeder normale Webspace reicht, PHP oder Python werden nicht benötigt.

**Lokal:** Die Datei per Doppelklick im Browser öffnen. Alles funktioniert gleich, die Daten liegen dann im lokalen Browserprofil.

**Externe Quellen:** Die Seite lädt die Schrift Roboto von Google Fonts und beim ersten PDF-Import die Bibliothek pdf.js von cdnjs. Ohne Internetverbindung fällt die Schrift auf Arial zurück, und statt des PDF-Imports funktioniert nur Kopieren und Einfügen.

Getestet mit aktuellen Versionen von Chrome, Edge, Firefox und Safari, auf Desktop und Smartphone.

## Bedienung

### Erster Einsatz

1. Im Reiter **Teilnehmende** die Anwesenheitsliste einlesen. Die Nummern werden in der Reihenfolge der Liste vergeben.
2. Optional unter **Erscheinungsbild** Titel, Fußzeile und Namensformat einstellen.
3. Auf **Neue Runde einteilen** klicken.

### Eine Runde einteilen

Im Einteilen-Fenster Tag, Gruppenzahl oder Gruppengröße und Bezeichnung festlegen. Die Anwesenheit kommt aus der Liste: eine leere Tageszelle heißt anwesend, „Entschuldigt“ oder ein anderer Eintrag heißt abwesend. Wer vor Ort fehlt oder früher geht, wird per Antippen ab- oder angemeldet.

**Gruppen berechnen** zeigt eine Vorschau mit allen Wiederbegegnungen. **Andere Variante** liefert eine andere, ebenso gute Lösung. Dieselben Eingaben ergeben immer dieselben Gruppen, Vorschau und gespeicherte Runde stimmen also überein.

Zum Umstellen eine Person antippen und dann eine Person in einer anderen Gruppe (tauschen) oder einen Gruppennamen (verschieben). **Runde speichern** legt die Runde mit Uhrzeit ab.

Schließen per Esc, Kreuz oder Zurück-Taste fragt nach, wenn eine ungespeicherte Vorschau offen ist.

### Runden

Der Reiter **Runden** zeigt alle Runden nach Modul und Tag, zeitlich sortiert. Standardmäßig ist nur die jüngste Runde aufgeklappt. **Bearbeiten** öffnet eine Runde zum Umstellen und zum Ändern von Bezeichnung und Uhrzeit. **Letzte Runde löschen** entfernt die zuletzt gespeicherte Runde.

### Matrix

Die Matrix zeigt, wie oft zwei Personen bisher in derselben Gruppe saßen. Die Farben beziehen sich auf den üblichen Wert (Median aller Paare der aktuellen Teilnehmenden):

| Farbe | Bedeutung |
|---|---|
| keine | üblicher Wert oder weniger |
| gelb | 1× über dem üblichen Wert |
| orange | 2× darüber |
| dunkelorange | 3× darüber |
| rot | 4× oder mehr darüber |

Neu hinzugekommene oder lange abwesende Personen liegen unter dem üblichen Wert und bleiben farblos. Mit dem Einteil-Algorithmus allein bleibt der Abstand erfahrungsgemäß bei 2 bis 3; Rot entsteht praktisch nur durch Handumstellungen.

### Neues Modul

1. Seite öffnen (auf einem neuen Gerät vorher **Sicherung laden**).
2. Bei den Teilnehmenden **Neues Modul einlesen** und die neue Liste wählen.
3. Im Abgleich-Fenster prüfen und **Übernehmen**.

Das Abgleich-Fenster zeigt, wer wiedererkannt wurde, wer neu ist und wer nicht mehr dabei ist. Namen, die sich nur leicht unterscheiden (Doppelname nach Heirat, Tippfehler, Kurzform), werden der bisherigen Person vorgeschlagen und lassen sich per Auswahl zuordnen. Unterschiede nur bei Umlauten (ü/ue) werden ohne Nachfrage erkannt.

Wiedererkannte behalten Nummer, Spitzname, Sperrpaare und alle Begegnungen. Neue bekommen die nächste freie Nummer. Wer nicht mehr dabei ist, wird ausgeblendet, behält aber seine Historie und wird bei einer Rückkehr wiedererkannt. Frühere Module zählen beim Einteilen voll mit.

### Neue Gruppe beginnen

Für eine ganz neue Gruppe (keine Fortsetzung mit neuem Modul) im Reiter **Teilnehmende** auf **Neue Gruppe beginnen** klicken. Das Fenster zeigt, was gelöscht wird: Teilnehmende (auch aus früheren Modulen), Runden mit allen Begegnungen, Sperrpaare und vor Ort geänderte Anwesenheit. Standardmäßig wird vorher eine Sicherung heruntergeladen, mit der sich die alte Gruppe über **Sicherung laden** wiederherstellen lässt. Titel, Fußzeile und Namensformat bleiben erhalten. Danach die neue Teilnehmerliste einlesen.

### Teilnehmende bearbeiten

Über **Bearbeiten** in der Teilnehmerliste lassen sich ein Spitzname vergeben und Sperrpaare festlegen („Nie in eine Gruppe mit“). Der Name selbst ist nicht bearbeitbar, weil er beim nächsten Einlesen zur Wiedererkennung dient.

Lassen sich Sperrpaare bei der gewählten Gruppenzahl nicht trennen, erscheint in der Vorschau eine rote Warnung.

## Eingabeformate

**PDF:** Druckansicht der Anwesenheitsliste aus dem Portal. Erkannt werden die Spalten Teilnehmer_in, Gruppe, eine Spalte pro Tag (Datum im Kopf) und Bemerkung sowie der Kursname über der Tabelle. Gedrehte Seiten und in Einzelbuchstaben zerlegte Wörter werden korrigiert. Eingescannte oder geschwärzte Listen enthalten keinen Text und lassen sich nicht auslesen; dann zeigt die Seite eine Diagnose.

**Kopieren und Einfügen:** Tabelle im Portal, in Excel oder Word markieren und einfügen. Text vor der Kopfzeile wird als Kursname übernommen.

**CSV/Text:** Getrennt durch Tabulator, Semikolon oder Komma. Beispiel:

```
Teilnehmer_in;Gruppe;28.09.2026;29.09.2026;Bemerkung
"Mustermann, Max";;;Entschuldigt;
"Beispiel, Anna";A;;;geht um 14 Uhr
```

Namen werden im Format „Nachname, Vorname“ erwartet. Die Anzahl der Tagesspalten ist beliebig.

## Datenschutz und Speicherung

Alle Daten bleiben im Browser (`localStorage`, Schlüssel `gruppenrotation.v1`). Nichts wird an einen Server übertragen, auch nicht beim PDF-Import. Die HTML-Datei selbst enthält keine personenbezogenen Daten und kann bedenkenlos veröffentlicht werden.

Die Daten gelten nur für diesen Browser auf diesem Gerät. Wer den Browserverlauf löscht, verliert sie. Deshalb regelmäßig **Sicherung speichern**.

**Sicherungsdateien und Anwesenheitslisten enthalten Namen von Teilnehmenden** und gehören nicht in ein öffentliches Repository. Die mitgelieferte `.gitignore` schließt sie aus.

In abgeschotteten Vorschauen (zum Beispiel in eingebetteten Frames) kann der Browser das Speichern verbieten. Die Seite weist dann einmalig darauf hin.

## Wie die Einteilung rechnet

Jedes Paar in einer Gruppe kostet so viele Strafpunkte wie das Quadrat seiner bisherigen Treffen: ein zweites Treffen 1, ein drittes 4, ein viertes 9. Ein drittes Treffen ist damit viel teurer als ein zweites, die Einteilung verteilt Wiederbegegnungen also möglichst breit. Sperrpaare kosten 100.000 Punkte und kommen nur zusammen, wenn es rechnerisch nicht anders geht.

Gesucht wird mit 400 zufälligen Startverteilungen, die jeweils so lange durch Tauschen verbessert werden, bis kein Tausch mehr hilft. Der Zufall wird aus den Eingaben abgeleitet (Anwesende, Gruppengrößen, Historie, Sperrpaare, Variante), daher sind die Ergebnisse reproduzierbar.

Ein Vergleich mit dem früheren Python-Skript über 20 Szenarien zu je 5 Runden ergab gleich gute Einteilungen: Bei identischem Ausgangsstand fanden beide Verfahren in allen Fällen eine gleich gute Runde. Die Seite rechnet dabei etwa hundertmal schneller (im Schnitt 0,03 s statt 3,7 s pro Runde).

## Technisches

- Eine Datei: HTML, CSS und JavaScript ohne Build-Schritt und ohne Framework
- Barrierefreiheit: Skip-Link, Reiter per Pfeiltasten, beschriftete Formularfelder, sichtbarer Tastaturfokus, `prefers-reduced-motion` wird beachtet
- Der aktive Reiter steht in der Adresse (`#teilnehmer`, `#runden`, `#matrix`, `#einstellungen`)
- Die Zurück-Taste schließt offene Fenster, statt die Seite zu verlassen
- Druck: `@media print` mit Logo und Fußzeile, alle Runden werden zum Drucken aufgeklappt

### Datenformat der Sicherung

```json
{
  "version": 1,
  "kurs": "CA2609-3 M1 – PZG & Erstgespräch",
  "tage": ["28.09.2026", "29.09.2026"],
  "teilnehmer": [
    {
      "nr": 1,
      "name": "Mustermann, Max",
      "spitzname": "Maxi",
      "alteNamen": ["Musterman, Max"],
      "gruppe": "",
      "bemerkung": "",
      "werte": { "28.09.2026": "", "29.09.2026": "Entschuldigt" },
      "inListe": true
    }
  ],
  "korrektur": { "28.09.2026": { "4": false } },
  "runden": [
    {
      "id": 1,
      "datum": "28.09.2026",
      "zeit": "10:15",
      "kurs": "CA2609-3 M1 – PZG & Erstgespräch",
      "label": "28.09.2026, Runde 1",
      "gruppen": [[1, 5, 12, 15], [2, 7, 14, 21]],
      "fehlend": [4]
    }
  ],
  "sperrpaare": [[1, 3]],
  "ci": {
    "titel": "Gruppenrotation",
    "fussLinks": "© INeKO – Institut an der Universität zu Köln",
    "fussRechts": "Kopie/Vervielfältigung nur nach schriftlicher Erlaubnis",
    "namensformat": "liste",
    "doppelteMitNachname": true
  }
}
```

`spitzname` und `alteNamen` sind optional. `inListe: false` kennzeichnet Personen, die nicht mehr dabei sind. `korrektur` enthält die vor Ort geänderte Anwesenheit pro Tag. Eine `historie.json` aus dem früheren Python-Skript lässt sich über **Sicherung laden** übernehmen; es werden dann nur die Runden importiert.

## Grenzen

- Daten sind an Browser und Gerät gebunden; zwischen Geräten über die Sicherungsdatei übertragen
- Keine gleichzeitige Bearbeitung durch mehrere Personen
- Der PDF-Import braucht eine Textebene im PDF und beim ersten Mal eine Internetverbindung
