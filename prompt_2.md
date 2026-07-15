# Entwicklung einer grafischen Benutzeroberfläche

## Ausgangssituation

Die bisherige Lösung funktioniert bereits sehr gut. Allerdings wird das Programm von Mitarbeitern verwendet, die keine oder nur geringe Python-Kenntnisse besitzen.

Deshalb soll das bestehende Python-Skript um eine **grafische Benutzeroberfläche** erweitert werden.

Für die Benutzeroberfläche soll **Tkinter** verwendet werden, da es plattformübergreifend verfügbar ist und das Programm dadurch auf verschiedenen Betriebssystemen eingesetzt werden kann.

---

# Aufgabe

Erweitere das bestehende Python-Skript um eine vollständige Tkinter-Benutzeroberfläche.

Über die Benutzeroberfläche sollen folgende Daten verwaltet werden können:

1. Fahrzeuge
2. Guides und Fahrer
3. Hotels
4. Touristengruppen
5. Planungsergebnisse

---

# 1. Verwaltung der Fahrzeuge

Die bereits im Dictionary `all_cars` vorhandenen Fahrzeuge sollen in der Benutzeroberfläche angezeigt werden.

Folgende Funktionen müssen zur Verfügung stehen:

* bestehende Fahrzeuge anzeigen,
* Fahrzeugdaten bearbeiten,
* neue Fahrzeuge hinzufügen,
* vorhandene Fahrzeuge löschen.

Alle Eigenschaften eines Fahrzeugs, die bisher im Dictionary `all_cars` gespeichert werden, müssen über die Benutzeroberfläche verwaltet werden können.

---

# 2. Verwaltung der Guides und Fahrer

Die bereits im Dictionary `all_guides` vorhandenen Personen sollen ebenfalls in der Benutzeroberfläche angezeigt werden.

Folgende Funktionen müssen zur Verfügung stehen:

* bestehende Personen anzeigen,
* Personendaten bearbeiten,
* neue Personen hinzufügen,
* vorhandene Personen löschen.

Dabei müssen sämtliche Informationen berücksichtigt werden, die bisher in `all_guides` gespeichert werden, beispielsweise:

* ob eine Person als Fahrer eingesetzt werden darf,
* ob eine Person als Guide eingesetzt werden darf,
* welche Sprachen die Person spricht,
* welche Fahrzeuge die Person fahren darf.

---

# 3. Verwaltung der Hotels

Die bereits im Dictionary `hotels` vorhandenen Hotels sollen über die Benutzeroberfläche verwaltet werden können.

Folgende Funktionen müssen zur Verfügung stehen:

* bestehende Hotels anzeigen,
* Hoteldaten bearbeiten,
* neue Hotels hinzufügen,
* vorhandene Hotels löschen.

Alle bisher im Dictionary `hotels` gespeicherten Informationen müssen editierbar sein.

---

# 4. Verwaltung der Touristengruppen

Die Daten im Dictionary `tourist_groups` stellen lediglich ein Beispiel für die Gruppen eines einzelnen Tages dar.

In der Praxis müssen jeden Tag neue Touristengruppen erfasst und geplant werden. Deshalb soll es über die Benutzeroberfläche möglich sein, Gruppen vollständig neu anzulegen.

Für jede Touristengruppe müssen alle Felder eingegeben und bearbeitet werden können, die bisher im Dictionary `tourist_groups` enthalten sind.

Zusätzlich müssen zwei neue Felder ergänzt werden.

## Feld `Escala`

Dieses Feld enthält das Datum des jeweiligen Einsatz- oder Planungstages.

Das Datum soll im folgenden Format eingegeben werden:

```text
DD-MM-YYYY
```

### Beispiel

```text
05-08-2026
```

---

## Feld `In/Out`

Dieses Feld gibt an, ob es sich um eine ankommende oder abreisende Gruppe handelt.

Der Wert soll als Boolean gespeichert werden.

```python
True
```

oder:

```python
False
```

In der Benutzeroberfläche sollte dieses Feld benutzerfreundlich dargestellt werden, beispielsweise durch:

* eine Checkbox,
* zwei Radiobuttons,
* oder ein Auswahlfeld mit den Optionen `In` und `Out`.

Intern kann der ausgewählte Wert weiterhin als Boolean gespeichert werden.

---

# 5. Erstellung der Tagesplanung

Die Benutzeroberfläche soll eine Funktion enthalten, mit der die automatische Zuordnung gestartet werden kann.

Dabei soll die bereits entwickelte Logik verwendet werden, um jeder Touristengruppe möglichst sinnvoll folgende Ressourcen zuzuordnen:

* ein geeignetes Fahrzeug,
* einen Fahrer,
* einen Guide mit den erforderlichen Sprachkenntnissen.

Die Zuordnung soll für den ausgewählten Planungstag beziehungsweise für den Wert aus `Escala` erfolgen.

Die berechneten Ergebnisse sollen anschließend übersichtlich in der Benutzeroberfläche angezeigt werden.

---

# 6. Export der Ergebnisse

Die erzeugte Tagesplanung soll exportiert werden können.

Mindestens folgende Exportformate müssen unterstützt werden:

* Excel (`.xlsx`)
* CSV (`.csv`)
* JSON (`.json`)

Beim Export soll der Benutzer über einen Dateidialog auswählen können:

* in welchem Ordner die Datei gespeichert wird,
* welchen Dateinamen die Datei erhält,
* in welchem unterstützten Format sie gespeichert wird.

Die exportierten Daten sollen alle relevanten Gruppeninformationen sowie die automatisch zugeordneten Fahrzeuge, Fahrer und Guides enthalten.

---

# Anforderungen an die Benutzeroberfläche

Die Benutzeroberfläche soll übersichtlich und auch für Personen ohne Programmierkenntnisse leicht verständlich sein.

Die verschiedenen Datenbereiche sollten klar voneinander getrennt werden, beispielsweise durch Tabs:

```text
Fahrzeuge | Guides und Fahrer | Hotels | Gruppen | Tagesplanung
```

Für die Verwaltung der Datensätze sollten verständliche Schaltflächen verwendet werden, beispielsweise:

```text
Neu | Bearbeiten | Speichern | Löschen | Abbrechen
```

Für die Planung und den Export könnten unter anderem folgende Schaltflächen vorgesehen werden:

```text
Planung erstellen | Ergebnisse anzeigen | Exportieren
```

Vor dem Löschen eines Datensatzes soll eine Sicherheitsabfrage erscheinen, damit Einträge nicht versehentlich entfernt werden.

Fehlende oder ungültige Eingaben sollen durch verständliche Fehlermeldungen angezeigt werden.

---

# Technische Anforderungen

* Verwende Python und Tkinter.
* Verwende nach Möglichkeit ausschließlich plattformübergreifende Bibliotheken.
* Die bisherige Zuordnungslogik soll erhalten bleiben und in die Benutzeroberfläche integriert werden.
* Trenne die Benutzeroberfläche möglichst klar von der eigentlichen Planungslogik.
* Das Programm soll direkt ausführbar sein.
* Der vollständige Quellcode soll ausgegeben werden.
* Alle benötigten Imports müssen enthalten sein.
* Es dürfen keine wichtigen Programmteile durch Platzhalter wie `...` ausgelassen werden.
* Der Code soll verständlich strukturiert und sinnvoll kommentiert sein.

Erstelle auf dieser Grundlage eine vollständige, funktionsfähige Tkinter-Anwendung.
