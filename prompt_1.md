# Automatische Zuordnung von Fahrzeugen, Fahrern und Guides zu Touristengruppen

## Ausgangssituation

Ich betreibe ein Touristikunternehmen mit einer eigenen Fahrzeugflotte. Die verfügbaren Fahrzeuge befinden sich im Dictionary `all_cars`.

Die Fahrzeuge haben unterschiedliche Größen und Kapazitäten. Die jeweilige Mindest- und Höchstkapazität wird über folgende Keys angegeben:

* `capacidade_min_de_pessoas`
* `capacidade_max_de_pessoas`

Außerdem arbeiten verschiedene Personen für das Unternehmen. Ihre Daten befinden sich im Dictionary `all_guides`.

Dabei gibt es drei Arten von Mitarbeitern:

1. **Nur Fahrer**

   * `is_driver=True`
   * `is_guide=False`

2. **Nur Guide**

   * `is_driver=False`
   * `is_guide=True`

3. **Fahrer und Guide**

   * `is_driver=True`
   * `is_guide=True`

Die Fahrzeuge, die eine Person fahren darf, sind unter dem Key `can_drive` aufgelistet.

Die Sprachen, die eine Person spricht, befinden sich unter dem Key `languages`.

Wenn eine Person ausschließlich als Guide tätig ist und nicht fahren darf, muss zusätzlich ein Fahrer eingeteilt werden. Dies bietet sich insbesondere bei größeren Gruppen an.

Die Gäste sind in verschiedenen Hotels untergebracht. Die Daten dieser Hotels befinden sich im Dictionary `hotels`.

---

## Aufgabe

Das Unternehmen betreut täglich eine Vielzahl von Touristengruppen.

Im Dictionary `tourist_groups` befindet sich ein Beispiel mit den Informationen zu den Gruppen, die am **05.08.2026** ankommen. Das relevante Datum befindet sich unter dem Key `voo_chegada_data`.

Jeder Gruppe müssen automatisch folgende Ressourcen zugeordnet werden:

* ein Fahrzeug mit geeigneter Kapazität,
* ein Fahrer,
* ein Guide, der die Sprache der Gruppe spricht.

Dabei soll nach Möglichkeit immer das **kleinste geeignete Fahrzeug** verwendet werden.

Diese Planung wird derzeit manuell durchgeführt und verursacht einen erheblichen Arbeitsaufwand.

Erstelle deshalb ein Python-Skript, das die Zuordnung von Fahrzeugen, Fahrern und Guides automatisiert.

---

# Beispiel für die gewünschte Ausgabe

Für `group2` könnte die Ausgabe beispielsweise folgendermaßen aussehen:

| O.S.  | File  | Pax | Pax/Grupo                 | Chegada         | Saída      | Vôo Out         | Hotel                                          | Idioma | Guia        | Veículo / Motorista              | Agência     |
| ----- | ----- | --: | ------------------------- | --------------- | ---------- | --------------- | ---------------------------------------------- | ------ | ----------- | -------------------------------- | ----------- |
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Paulo Baron | EXPERT 4 - UAY7D24 - Paulo Baron | Idéia Tours |

> **Anmerkung:** Dies ist nur eine mögliche korrekte Zuordnung. Da mehrere geeignete Fahrer, Guides und Fahrzeuge verfügbar sein können, sind auch andere Ergebnisse zulässig.

Beispielsweise wäre auch folgende Zuordnung korrekt:

| O.S.  | File  | Pax | Pax/Grupo                 | Chegada         | Saída      | Vôo Out         | Hotel                                          | Idioma | Guia    | Veículo / Motorista          | Agência     |
| ----- | ----- | --: | ------------------------- | --------------- | ---------- | --------------- | ---------------------------------------------- | ------ | ------- | ---------------------------- | ----------- |
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Romildo | EXPERT 4 - UAY7D24 - Romildo | Idéia Tours |

Ebenso wäre die Verwendung eines anderen geeigneten Fahrzeugs möglich:

| O.S.  | File  | Pax | Pax/Grupo                 | Chegada         | Saída      | Vôo Out         | Hotel                                          | Idioma | Guia        | Veículo / Motorista                      | Agência     |
| ----- | ----- | --: | ------------------------- | --------------- | ---------- | --------------- | ---------------------------------------------- | ------ | ----------- | ---------------------------------------- | ----------- |
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Paulo Baron | PEUGEOT/EXPERT 1 - SEN9F61 - Paulo Baron | Idéia Tours |

Auch diese Kombination wäre zulässig:

| O.S.  | File  | Pax | Pax/Grupo                 | Chegada         | Saída      | Vôo Out         | Hotel                                          | Idioma | Guia    | Veículo / Motorista                  | Agência     |
| ----- | ----- | --: | ------------------------- | --------------- | ---------- | --------------- | ---------------------------------------------- | ------ | ------- | ------------------------------------ | ----------- |
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Romildo | PEUGEOT/EXPERT 1 - SEN9F61 - Romildo | Idéia Tours |

Für dieses Beispiel existieren noch zahlreiche weitere korrekte Zuordnungsmöglichkeiten.

---

# Erklärung der Ausgabefelder

## `Pax`

Dieses Feld setzt sich aus folgenden Keys zusammen:

* `pax`
* `numero_de_guias_externos`

Beide Werte werden mit einem Pluszeichen verbunden.

### Beispiel

```text
3+1
```

Wenn `numero_de_guias_externos` den Wert `0` hat, wird ausschließlich der Wert von `pax` ausgegeben.

### Beispiel

```text
3
```

---

## `Pax/Grupo`

Hier werden die Werte aus `nomes_dos_passageiros` mit einem Pluszeichen verbunden.

### Beispiel

```text
Hans Müller + Ana Schmidt
```

Wichtig ist, dass hier nur die Hauptansprechpartner der Gruppe angegeben werden.

Die Anzahl der aufgeführten Namen muss daher nicht mit dem Wert von `pax` übereinstimmen.

---

## `Chegada`

Dieses Feld setzt sich aus folgenden Werten zusammen:

* `voo_chegada_numero`
* `voo_chegada_horario`

Die Werte werden mit einem Bindestrich verbunden.

### Beispiel

```text
KK 3290 - 11:30
```

Wenn die entsprechenden Flugdaten fehlen, bleibt das Feld leer.

---

## `Vôo Out`

Dieses Feld setzt sich aus folgenden Werten zusammen:

* `voo_partida_numero`
* `voo_partida_horario`

Die Werte werden mit einem Bindestrich verbunden.

### Beispiel

```text
JJ 1179 - 07:30
```

Wenn die entsprechenden Flugdaten fehlen, bleibt das Feld leer.

---

# Zentrale Zuordnungsfelder

Die Hauptaufgabe des Skripts besteht in der korrekten Ermittlung der folgenden drei Felder:

1. `Idioma`
2. `Guia`
3. `Veículo / Motorista`

---

## `Idioma`

Die eingeteilte Person muss die Sprache der jeweiligen Touristengruppe sprechen.

Wenn die Sprache der Gruppe beispielsweise Deutsch ist, muss der ausgewählte Guide Deutsch sprechen.

---

## `Guia`

Im oben dargestellten Beispiel wurde `Paulo Baron` ausgewählt, weil er Deutsch spricht und damit die sprachlichen Anforderungen der Gruppe erfüllt.

Ein anderer verfügbarer Guide, der ebenfalls Deutsch spricht, wäre jedoch genauso zulässig.

---

## `Veículo / Motorista`

Im ersten Beispiel wurde das Fahrzeug mit dem Kennzeichen `UAY7D24` ausgewählt.

Dieses Fahrzeug besitzt eine Mindestkapazität von vier Personen und ist deshalb für die Gruppe geeignet.

Die relevante Gruppengröße wird folgendermaßen berechnet:

```python
gruppengroesse = pax + numero_de_guias_externos
```

Der vom Unternehmen eingeteilte Guide und der Fahrer werden bei dieser Kapazitätsberechnung **nicht** berücksichtigt.

Zusätzlich muss geprüft werden, ob die ausgewählte Person das Fahrzeug fahren darf. Diese Information befindet sich im jeweiligen `can_drive`-Eintrag innerhalb von `all_guides`.

Der endgültige Wert des Feldes `Veículo / Motorista` setzt sich folgendermaßen zusammen:

```text
marca_modelo - numero_do_carro - Hauptkey des Fahrzeugs - Fahrer
```

Der Hauptkey des Fahrzeugs entspricht dem Autokennzeichen.

### Beispiel

```text
EXPERT 4 - UAY7D24 - Paulo Baron
```

---

# Trennung von Fahrer und Guide

Normalerweise kann eine Person gleichzeitig als Fahrer und Guide eingesetzt werden, sofern sie beide Voraussetzungen erfüllt.

Unter mindestens einer der folgenden Bedingungen sollen jedoch zwei unterschiedliche Personen eingeteilt werden:

1. Die Summe aus `pax` und `numero_de_guias_externos` übersteigt den Wert der Variable `maximum_group_size_with_only_one_person`.

2. Der Key `pagou_pelo_guia_extra` hat den Wert `True`.

In diesen Fällen soll eine Person als Guide und eine andere Person als Fahrer eingeteilt werden, da die gleichzeitige Tätigkeit als Fahrer und Guide bei größeren Gruppen sehr stressig sein kann.

---

# Wichtige Regeln und Sonderfälle

## 1. Verwendung größerer Fahrzeuge bei Engpässen

Angenommen, es gibt 19 Gruppen mit jeweils höchstens drei Personen.

Es stehen jedoch nur 17 Fahrzeuge zur Verfügung, deren maximale Kapazität drei Personen beträgt.

In diesem Fall sollen für die beiden verbleibenden Gruppen die nächstgrößeren verfügbaren Fahrzeuge verwendet werden.

Dieses Prinzip gilt nicht nur für kleine Gruppen, sondern für alle Gruppengrößen:

> Wenn kein Fahrzeug der bevorzugten Größenklasse mehr verfügbar ist, soll das nächstgrößere geeignete Fahrzeug verwendet werden.

Ein zu kleines Fahrzeug darf niemals zugeteilt werden.

---

## 2. Nicht ausreichende Anzahl an Fahrzeugen

Falls die vorhandenen Fahrzeuge nicht für alle Gruppen ausreichen, soll bei den nicht zugeordneten Gruppen ein deutlicher Hinweis erscheinen.

### Beispiel

```text
Für diese Gruppe muss ein zusätzliches Fahrzeug angemietet werden.
```

---

## 3. Keine mehrfachen Zuordnungen

Da es sich um den Fahrplan eines einzelnen Tages handelt, dürfen Ressourcen nicht mehrfach vergeben werden.

Jede der folgenden Ressourcen darf maximal einmal verwendet werden:

* jedes Fahrzeug,
* jeder Fahrer,
* jeder Guide.

Es dürfen keine Überschneidungen oder Doppelbelegungen entstehen.

Wenn eine Person gleichzeitig als Fahrer und Guide für eine Gruppe eingesetzt wird, gilt diese Person damit vollständig als belegt und darf keiner weiteren Gruppe zugeordnet werden.

---

# Gewünschtes Ausgabeformat

Die tatsächliche Ausgabe des Python-Skripts soll vorerst **kein Markdown** sein.

Eine **List of Lists** ist ausreichend.

Die Struktur könnte beispielsweise folgendermaßen aussehen:

```python
[
    [
        "51121",
        "51851",
        "3+1",
        "Hans Müller + Ana Schmidt",
        "KK 3290 - 11:30",
        "11.08.2026",
        "JJ 1179 - 07:30",
        "Bourbon Thermas Eco Resort Cataratas do Iguaçu",
        "alemão",
        "Paulo Baron",
        "EXPERT 4 - UAY7D24 - Paulo Baron",
        "Idéia Tours",
    ],
]
```

Erstelle ein vollständiges und ausführbares Python-Skript, das diese Anforderungen berücksichtigt und die Gruppen automatisch möglichst sinnvoll auf die verfügbaren Fahrzeuge, Fahrer und Guides verteilt.

## Hier findest du die benötigten Daten als Python-Datentypen

```py
all_cars = {
    "BDQ3B09": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN/ VERSA",
        "renavam": "1206595407",
        "ano_modelo": "2019/2020",
        "selo_foztrans": "46518",
        "numero_do_carro": 3,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE9300": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1160746858",
        "ano_modelo": "2018/2020",
        "selo_foztrans": "46514",
        "numero_do_carro": 9,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE7879": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "FIDEL",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46515",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE6088": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1160726814",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46511",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE5700": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1160726300",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46515",
        "numero_do_carro": 5,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE0G77": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1161575763",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46514",
        "numero_do_carro": 10,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BDQ3B05": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1208328554",
        "ano_modelo": "2019/2020",
        "selo_foztrans": "46514",
        "numero_do_carro": 11,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE8022": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1160728302",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46518",
        "numero_do_carro": 8,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BDQ3B06": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1206594915",
        "ano_modelo": "2019/2020",
        "selo_foztrans": "46511",
        "numero_do_carro": 12,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "BAE5088": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "MERCEDEZ/SPRINTER",
        "renavam": "1158860029",
        "ano_modelo": "2018/2019",
        "selo_foztrans": "46520",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 7,
        "capacidade_max_de_pessoas": 12,
    },
    "BAE8282": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "MERCEDEZ / C180",
        "renavam": "1164768759",
        "ano_modelo": "2018/2018",
        "selo_foztrans": "46522",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "UAY7D24": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "EXPERT",
        "renavam": "1465010154",
        "ano_modelo": "2025/2025",
        "selo_foztrans": "46366",
        "numero_do_carro": 4,
        "capacidade_min_de_pessoas": 4,
        "capacidade_max_de_pessoas": 6,
    },
    "UBV6G82": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1489705772",
        "ano_modelo": "2026/2026",
        "selo_foztrans": "46519",
        "numero_do_carro": 6,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "UBV7A12": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "1489704644",
        "ano_modelo": "2026/2026",
        "selo_foztrans": "46519",
        "numero_do_carro": 14,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "UBH8I23": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "01481816338",
        "ano_modelo": "2025/2026",
        "selo_foztrans": None,
        "numero_do_carro": 7,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "UBH9J12": {
        "frota": "ARVOREVIDA",
        "marca_modelo": "NISSAN / VERSA",
        "renavam": "01482124260",
        "ano_modelo": "2025/2026",
        "selo_foztrans": None,
        "numero_do_carro": 4,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "SEN9F61": {
        "frota": "EIDT",
        "marca_modelo": "PEUGEOT/EXPERT",
        "renavam": "01351561143",
        "ano_modelo": "2023/2024",
        "selo_foztrans": "46200",
        "numero_do_carro": 1,
        "capacidade_min_de_pessoas": 4,
        "capacidade_max_de_pessoas": 6,
    },
    "TAJ3G67": {
        "frota": "EIDT",
        "marca_modelo": "PEUGEOT/EXPERT",
        "renavam": "01398871866",
        "ano_modelo": "2024/2024",
        "selo_foztrans": "46211",
        "numero_do_carro": 2,
        "capacidade_min_de_pessoas": 4,
        "capacidade_max_de_pessoas": 6,
    },
    "TAO0J52": {
        "frota": "EIDT",
        "marca_modelo": "PEUGEOT/EXPERT",
        "renavam": "01412141823",
        "ano_modelo": "2024/2024",
        "selo_foztrans": "46249",
        "numero_do_carro": 3,
        "capacidade_min_de_pessoas": 4,
        "capacidade_max_de_pessoas": 6,
    },
    "TAI2I59": {
        "frota": "EIDT",
        "marca_modelo": "VERSA / NISSAN",
        "renavam": "01397590006",
        "ano_modelo": "2024/2024",
        "selo_foztrans": "46225",
        "numero_do_carro": 1,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "SEM9G22": {
        "frota": "EIDT",
        "marca_modelo": "VERSA / NISSAN",
        "renavam": "01349525437",
        "ano_modelo": "2023/2023",
        "selo_foztrans": "46326",
        "numero_do_carro": 2,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "TBS5B25": {
        "frota": "EIDT",
        "marca_modelo": "VERSA / NISSAN",
        "renavam": "01449619158",
        "ano_modelo": "2025/2026",
        "selo_foztrans": "ENIO PARTICULAR",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 1,
        "capacidade_max_de_pessoas": 3,
    },
    "EWU2C33": {
        "frota": "EIDT",
        "marca_modelo": "VW/ GRANMICRO",
        "renavam": None,
        "ano_modelo": "2012/2012",
        "selo_foztrans": "NICO",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 13,
        "capacidade_max_de_pessoas": 17,
    },
    "BAE4008": {
        "frota": "RIGOR",
        "marca_modelo": "MORCOPOLO / ONIBUS",
        "renavam": "528714945",
        "ano_modelo": "2012/2013",
        "selo_foztrans": "46515",
        "numero_do_carro": None,
        "capacidade_min_de_pessoas": 18,
        "capacidade_max_de_pessoas": 50,
    },
}
all_guides = {
    "Maiko": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Veronique": {
        "languages": ["francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Loni": {
        "languages": ["alemão", "espanhol"],
        "is_driver": False,
        "is_guide": True,
        "can_drive": [],
    },
    "Elcio": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Julierton": {
        "languages": ["inglês", "italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Wagner": {
        "languages": ["francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Ivone": {
        "languages": ["alemão"],
        "is_driver": False,
        "is_guide": True,
        "can_drive": [],
    },
    "Willian": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Giovani": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Hakin": {
        "languages": ["francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Romildo": {
        "languages": ["alemão", "espanhol"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Bernardo": {
        "languages": ["inglês", "francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Fidel": {
        "languages": ["inglês", "italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Ana Selle": {
        "languages": ["francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Jandir": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Debora": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Flavio": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Paulo Baron": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Carini": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Nereu": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Wilson": {
        "languages": ["inglês", "francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Paulinho": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Lino": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Reginaldo": {
        "languages": ["inglês", "francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Enio Baron": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Junior": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Jair Triaca": {
        "languages": ["inglês", "italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BAE4008",
        ],
    },
    "Denis": {
        "languages": ["francês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Darci": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Nicolas": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Sartor": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Jair Afonso": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Netto": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Miguel": {
        "languages": ["inglês", "italiano"],
        "is_driver": False,
        "is_guide": True,
        "can_drive": [],
    },
    "Edio": {
        "languages": ["alemão"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Oliveira": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Fabiano": {
        "languages": ["italiano"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Ilton": {
        "languages": ["alemão", "espanhol"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BAE5088",
        ],
    },
    "Tiago": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Geovani": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Rodrigo": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Marcolino": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Chader": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Jeferson": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Leonardo": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Celso Aguayo": {
        "languages": ["inglês"],
        "is_driver": True,
        "is_guide": True,
        "can_drive": [
            "BDQ3B09",
            "BAE9300",
            "BAE7879",
            "BAE6088",
            "BAE5700",
            "BAE0G77",
            "BDQ3B05",
            "BAE8022",
            "BDQ3B06",
            "BAE8282",
            "UAY7D24",
            "UBV6G82",
            "UBV7A12",
            "UBH8I23",
            "UBH9J12",
            "SEN9F61",
            "TAJ3G67",
            "TAO0J52",
            "TAI2I59",
            "SEM9G22",
            "TBS5B25",
        ],
    },
    "Jair Polaco": {
        "languages": [],
        "is_driver": True,
        "is_guide": False,
        "can_drive": ["BAE4008"],
    },
    "Nico": {
        "languages": [],
        "is_driver": True,
        "is_guide": False,
        "can_drive": ["EWU2C33"],
    },
}

hotels = {
    "Hotel das Cataratas, A Belmond Hotel, Iguassu Falls": {
        "adresse": "Rodovia BR-469, Km 32, Parque Nacional do Iguaçu, Foz do Iguaçu - PR, 85855-750",
        "land": "Brasilien",
    },
    "Sanma Hotel": {
        "adresse": "Av. das Cataratas, 12280 - Km 21, Foz do Iguaçu - PR, 85859-899",
        "land": "Brasilien",
    },
    "Vivaz Cataratas Resort": {
        "adresse": "Av. das Cataratas, 6798 - Carimã, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "Grand Carimã Resort & Convention Center": {
        "adresse": "Av. das Cataratas, 4790, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "Mabu Thermas Grand Resort": {
        "adresse": "Av. das Cataratas, 3175 - Vila Yolanda, Foz do Iguaçu - PR, 85853-000",
        "land": "Brasilien",
    },
    "DoubleTree by Hilton Foz do Iguaçu Brazil": {
        "adresse": "Av. das Cataratas, 2930 - Vila Yolanda, Foz do Iguaçu - PR, 85853-000",
        "land": "Brasilien",
    },
    "Bourbon Thermas Eco Resort Cataratas do Iguaçu": {
        "adresse": "Av. das Cataratas, 2345 - Vila Yolanda, Foz do Iguaçu - PR, 85853-000",
        "land": "Brasilien",
    },
    "Viale Cataratas Hotel & Eventos": {
        "adresse": "Av. das Cataratas, 2420 - Vila Yolanda, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "LAS Hotel Boutique": {
        "adresse": "Rua Oscar Genehr, 425 - Cataratas, Foz do Iguaçu - PR, 85853-860",
        "land": "Brasilien",
    },
    "Viale Tower Hotel": {
        "adresse": "Av. Jorge Schimmelpfeng, 232 - Centro, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "Hotel Rafain Centro": {
        "adresse": "Rua Marechal Deodoro, 984 - Centro, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "Nadai Confort Hotel & SPA": {
        "adresse": "Av. República Argentina, 1332 - Centro, Foz do Iguaçu - PR, 85851-200",
        "land": "Brasilien",
    },
    "Tarobá Hotel": {
        "adresse": "Rua Tarobá, 1048 - Centro, Foz do Iguaçu - PR, 85851-220",
        "land": "Brasilien",
    },
    "Recanto Cataratas Thermas Resort & Convention": {
        "adresse": "Av. Costa e Silva, 3500, Foz do Iguaçu - PR",
        "land": "Brasilien",
    },
    "Falls Galli Hotel": {
        "adresse": "Av. Costa e Silva, 1602, Foz do Iguaçu - PR, 85852-282",
        "land": "Brasilien",
    },
    "Wish Foz do Iguaçu Resort": {
        "adresse": "Av. das Cataratas, 6845 - Tamanduá, Foz do Iguaçu - PR, 85853-000",
        "land": "Brasilien",
    },
    "Gran Meliá Iguazú": {
        "adresse": "Parque Nacional Iguazú S/N, Puerto Iguazú, Misiones 3370",
        "land": "Argentinien",
    },
    "La Reserva Virgin Lodge": {
        "adresse": "Calles Ñamandú Rú Eté y Batalla Tekoá, Selva Iryapú, Puerto Iguazú, Misiones 3370",
        "land": "Argentinien",
    },
    "Loi Suites Iguazú Hotel": {
        "adresse": "Selva Iryapú s/n, Puerto Iguazú, Misiones 3370",
        "land": "Argentinien",
    },
    "Mercure Iguazu Hotel Iru": {
        "adresse": "Selva Iryapú S/N, Predio 600 Has, Puerto Iguazú, Misiones 3370",
        "land": "Argentinien",
    },
}

tourist_groups = {
    "group1": {
        "pax": 2,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 51421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Fuchs Anajali", "Mario Sperry"],
        "nacionalidade": "Inglaterra",
        "hotel": "DoubleTree by Hilton Foz do Iguaçu Brazil",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "19:00",
        "voo_chegada_numero": "JJ 3290",
        "voo_partida_existe": True,
        "voo_partida_data": "11.08.2026",
        "voo_partida_horario": "06:00",
        "voo_partida_numero": "JJ 3879",
        "idioma": "inglês",
        "file": "51852",
        "pedagios": "br+arg",
    },
    "group2": {
        "pax": 3,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 51121,
        "numero_de_guias_externos": 1,
        "nomes_dos_passageiros": ["Hans Müller", "Ana Schmidt"],
        "nacionalidade": "Alemanha",
        "hotel": "Bourbon Thermas Eco Resort Cataratas do Iguaçu",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "11:30",
        "voo_chegada_numero": "KK 3290",
        "voo_partida_existe": True,
        "voo_partida_data": "11.08.2026",
        "voo_partida_horario": "07:30",
        "voo_partida_numero": "JJ 1179",
        "idioma": "alemão",
        "file": "51851",
        "pedagios": "br+arg",
    },
    "group3": {
        "pax": 4,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 11421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Luca Bianchi", "Elena Ferrara"],
        "nacionalidade": "Itália",
        "hotel": "LAS Hotel Boutique",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": True,
        "voo_partida_data": "12.08.2026",
        "voo_partida_horario": "08:45",
        "voo_partida_numero": "LA 4721",
        "idioma": "italiano",
        "file": "58294",
        "pedagios": "br",
    },
    "group4": {
        "pax": 6,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 21421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["John Carter", "Emily Carter"],
        "nacionalidade": "Estados Unidos",
        "hotel": "Hotel das Cataratas, A Belmond Hotel, Iguassu Falls",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "15:20",
        "voo_chegada_numero": "AA 7814",
        "voo_partida_existe": True,
        "voo_partida_data": "13.08.2026",
        "voo_partida_horario": "10:10",
        "voo_partida_numero": "AA 7822",
        "idioma": "inglês",
        "file": "73916",
        "pedagios": "br+arg",
    },
    "group5": {
        "pax": 2,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 31421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Claire Dubois", "Antoine Moreau"],
        "nacionalidade": "França",
        "hotel": "Sanma Hotel",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "18:35",
        "voo_chegada_numero": "AF 4562",
        "voo_partida_existe": False,
        "voo_partida_data": "",
        "voo_partida_horario": "",
        "voo_partida_numero": "",
        "idioma": "francês",
        "file": "61483",
        "pedagios": "br",
    },
    "group6": {
        "pax": 11,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 41421,
        "numero_de_guias_externos": 1,
        "nomes_dos_passageiros": ["Carlos García", "Lucía Torres"],
        "nacionalidade": "Espanha",
        "hotel": "Vivaz Cataratas Resort",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": True,
        "voo_partida_data": "14.08.2026",
        "voo_partida_horario": "09:00",
        "voo_partida_numero": "IB 3907",
        "idioma": "espanhol",
        "file": "84520",
        "pedagios": "br+arg",
    },
    "group7": {
        "pax": 5,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 61421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Thomas Weber", "Laura Klein"],
        "nacionalidade": "Alemanha",
        "hotel": "Grand Carimã Resort & Convention Center",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "21:15",
        "voo_chegada_numero": "LH 5088",
        "voo_partida_existe": True,
        "voo_partida_data": "15.08.2026",
        "voo_partida_horario": "06:40",
        "voo_partida_numero": "LH 5091",
        "idioma": "alemão",
        "file": "39271",
        "pedagios": "br",
    },
    "group8": {
        "pax": 3,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 71421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Michael Evans", "Daniel Green"],
        "nacionalidade": "Inglaterra",
        "hotel": "Mabu Thermas Grand Resort",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": False,
        "voo_partida_data": "",
        "voo_partida_horario": "",
        "voo_partida_numero": "",
        "idioma": "inglês",
        "file": "10486",
        "pedagios": "br+arg",
    },
    "group9": {
        "pax": 7,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 81421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Isabella Rossi", "Matteo Russo"],
        "nacionalidade": "Itália",
        "hotel": "DoubleTree by Hilton Foz do Iguaçu Brazil",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "14:50",
        "voo_chegada_numero": "AZ 7428",
        "voo_partida_existe": True,
        "voo_partida_data": "16.08.2026",
        "voo_partida_horario": "11:25",
        "voo_partida_numero": "AZ 7431",
        "idioma": "italiano",
        "file": "68735",
        "pedagios": "br",
    },
    "group10": {
        "pax": 2,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 91421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Marie Laurent", "Julien Bernard"],
        "nacionalidade": "França",
        "hotel": "Bourbon Thermas Eco Resort Cataratas do Iguaçu",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "13:10",
        "voo_chegada_numero": "AF 2219",
        "voo_partida_existe": False,
        "voo_partida_data": "",
        "voo_partida_horario": "",
        "voo_partida_numero": "",
        "idioma": "francês",
        "file": "52840",
        "pedagios": "br+arg",
    },
    "group11": {
        "pax": 8,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 52421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Pablo Navarro", "Elena Morales"],
        "nacionalidade": "Espanha",
        "hotel": "Viale Cataratas Hotel & Eventos",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": True,
        "voo_partida_data": "17.08.2026",
        "voo_partida_horario": "07:55",
        "voo_partida_numero": "UX 3045",
        "idioma": "espanhol",
        "file": "91627",
        "pedagios": "br",
    },
    "group12": {
        "pax": 12,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 53421,
        "numero_de_guias_externos": 1,
        "nomes_dos_passageiros": ["Max Schneider", "Anna Wagner"],
        "nacionalidade": "Alemanha",
        "hotel": "Viale Tower Hotel",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "16:05",
        "voo_chegada_numero": "LH 4172",
        "voo_partida_existe": True,
        "voo_partida_data": "18.08.2026",
        "voo_partida_horario": "12:30",
        "voo_partida_numero": "LH 4175",
        "idioma": "alemão",
        "file": "75038",
        "pedagios": "br+arg",
    },
    "group13": {
        "pax": 4,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 51421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Anna Taylor", "George White"],
        "nacionalidade": "Inglaterra",
        "hotel": "Hotel Rafain Centro",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": True,
        "voo_partida_data": "19.08.2026",
        "voo_partida_horario": "15:15",
        "voo_partida_numero": "BA 6620",
        "idioma": "inglês",
        "file": "48395",
        "pedagios": "br",
    },
    "group14": {
        "pax": 9,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 54421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Federico Costa", "Martina Rinaldi"],
        "nacionalidade": "Itália",
        "hotel": "Nadai Confort Hotel & SPA",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "20:25",
        "voo_chegada_numero": "AZ 3348",
        "voo_partida_existe": False,
        "voo_partida_data": "",
        "voo_partida_horario": "",
        "voo_partida_numero": "",
        "idioma": "italiano",
        "file": "26174",
        "pedagios": "br+arg",
    },
    "group15": {
        "pax": 3,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 55421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Camille Petit", "Élodie Garnier"],
        "nacionalidade": "França",
        "hotel": "Tarobá Hotel",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "17:40",
        "voo_chegada_numero": "AF 9021",
        "voo_partida_existe": True,
        "voo_partida_data": "20.08.2026",
        "voo_partida_horario": "09:35",
        "voo_partida_numero": "AF 9026",
        "idioma": "francês",
        "file": "60719",
        "pedagios": "br",
    },
    "group16": {
        "pax": 10,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 51421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Alejandro Santos", "María Peña"],
        "nacionalidade": "Argentina",
        "hotel": "Recanto Cataratas Thermas Resort & Convention",
        "voo_chegada_existe": False,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "",
        "voo_chegada_numero": "",
        "voo_partida_existe": True,
        "voo_partida_data": "21.08.2026",
        "voo_partida_horario": "13:50",
        "voo_partida_numero": "AR 1783",
        "idioma": "espanhol",
        "file": "39582",
        "pedagios": "br+arg",
    },
    "group17": {
        "pax": 5,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 56421,
        "numero_de_guias_externos": 0,
        "nomes_dos_passageiros": ["Oliver Smith", "Charlotte Smith"],
        "nacionalidade": "Inglaterra",
        "hotel": "Wish Foz do Iguaçu Resort",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "12:05",
        "voo_chegada_numero": "BA 5107",
        "voo_partida_existe": True,
        "voo_partida_data": "22.08.2026",
        "voo_partida_horario": "18:20",
        "voo_partida_numero": "BA 5110",
        "idioma": "inglês",
        "file": "87406",
        "pedagios": "br",
    },
    "group18": {
        "pax": 13,
        "pagou_pelo_guia_extra": False,
        "agencia": "Idéia Tours",
        "O.S.": 51431,
        "numero_de_guias_externos": 1,
        "nomes_dos_passageiros": ["Klaus Berger", "Tobias Graf"],
        "nacionalidade": "Alemanha",
        "hotel": "Loi Suites Iguazú Hotel",
        "voo_chegada_existe": True,
        "voo_chegada_data": "05.08.2026",
        "voo_chegada_horario": "19:30",
        "voo_chegada_numero": "LH 8894",
        "voo_partida_existe": True,
        "voo_partida_data": "23.08.2026",
        "voo_partida_horario": "08:15",
        "voo_partida_numero": "LH 8899",
        "idioma": "alemão",
        "file": "14263",
        "pedagios": "br+arg",
    },
}
maximum_group_size_with_only_one_person = 7
```
    


      

