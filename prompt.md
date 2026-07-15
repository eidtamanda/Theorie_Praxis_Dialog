Ich habe ein Touristenunternehmen mit einer Fahrzeugflotte, die im dict "all_cars" gelisted sind.
Wie man anhand der Daten erkennen kann, sind die Fahrzeuge unterschiedlich groß (keys: capacidade_min_de_pessoas, capacidade_max_de_pessoas)
 

Dann habe ich Leute, die für mich arbeiten und die im dict "all_guides" gelisted sind. 
Es gibt dort Leute, die entweder 
1) nur Fahrer sind (is_driver=True, is_guide=False)
2) nur Guides sind (is_driver=False, is_guide=True) 
3) beides sind (is_driver=True, is_guide=True)
Die Fahrzeuge, die die Personen fahren dürfen, sind in "can_drive" gelistet. 
Die Sprachen, die eine Person spricht, sind in "languages" gelistet. 
Wenn eine Person nur Guide ist und nicht fahren darf, braucht sie natürlich noch einen zusätzlichen Fahrer. Dies bietet sich vor allem bei großen Gruppen an.

Die Gäste sind in verschiedenen Hotels untergebracht, deren Daten sich im dict "hotels" befinden.

Die Firma bekommt jeden Tag eine Vielzahl von Gruppen. In dem dict "tourist_groups" findest du ein Beispiel der Informationen der Gruppen, die wir am 05.08.2026 (key: voo_chegada_data) bekommen und denen wir ein Fahrzeug mit geeigneter Kapazität (Minimum bevorzugt), Fahrer, Guide (mit gleicher Sprache) zuordnen müssen. Diese Arbeit wird zurzeit manuell erledigt und erfordert großen Aufwand. Deine Aufgabe ist es, ein Python-Script zu erstellen, das diese Aufgabe automatisiert.  

Ich gebe dir hier ein Beispiel als Markdown, wie diese Ausgabe von "group2" sein könnte:

| O.S. | File | Pax | Pax/Groupo | Chegada | Saída | Vôo Out | Hotel | Idioma | Guia | Veículo / Motorista | Agência |
|------|------|-----|------------|---------|-------|---------|-------|--------|------|---------------------|---------|
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Paulo Baron | EXPERT 4 - UAY7D24 - Paulo Baron | Idéia Tours |

Amerkung: Das ist nur ein Beispiel, es wäre auch vollkommen okay, wenn die Ausgabe zum Beispiel so wäre:

| O.S. | File | Pax | Pax/Groupo | Chegada | Saída | Vôo Out | Hotel | Idioma | Guia | Veículo / Motorista | Agência |
|------|------|-----|------------|---------|-------|---------|-------|--------|------|---------------------|---------|
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Romildo | EXPERT 4 - UAY7D24 - Romildo | Idéia Tours |

oder so: 

| O.S. | File | Pax | Pax/Groupo | Chegada | Saída | Vôo Out | Hotel | Idioma | Guia | Veículo / Motorista | Agência |
|------|------|-----|------------|---------|-------|---------|-------|--------|------|---------------------|---------|
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Paulo Baron | PEUGEOT/EXPERT 1 - SEN9F61 - Paulo Baron | Idéia Tours |

oder so: 

| O.S. | File | Pax | Pax/Groupo | Chegada | Saída | Vôo Out | Hotel | Idioma | Guia | Veículo / Motorista | Agência |
|------|------|-----|------------|---------|-------|---------|-------|--------|------|---------------------|---------|
| 51121 | 51851 | 3+1 | Hans Müller + Ana Schmidt | KK 3290 - 11:30 | 11.08.2026 | JJ 1179 - 07:30 | Bourbon Thermas Eco Resort Cataratas do Iguaçu | alemão | Romildo | PEUGEOT/EXPERT 1 - SEN9F61 - Romildo | Idéia Tours |

Es gibt noch zig andere korrekte Optionen für dieses Beispiel.


Die Felder, die eine Erklärung benötigen:

Pax: hier werden die Keys "pax" und "numero_de_guias_externos" genommen und mit einem Pluszeichen verbunden. Wenn der Key "numero_de_guias_externos" die Value 0 hat, wird nur die Value von "pax" angegeben 
Pax/Groupo: Hier werden die Values von dem Key "nomes_dos_passageiros" mit einem Pluszeichen verbunden. Wichtig ist: Hier werden nur die Hauptansprechpartner angegeben. Die Anzahl der Personen hier muss nicht mit der Anzahl von "pax" übereinstimmen 

Chegada: Hier werden die Values von "voo_chegada_numero" und "voo_chegada_horario" mit einem Bindestrich verbunden. Wenn diese Daten fehlen, wird das Feld leergelassen.

Vôo Out: Hier werden die Values von "voo_partida_numero" und "voo_partida_horario" mit einem Bindestrich verbunden. Wenn diese Daten fehlen, wird das Feld leergelassen.

Jetzt du den wichtigsten Feldern, die deine Hauptaufgabe darstellen: 
Idioma, Guia, Veículo / Motorista

zu "Idioma": natürlich muss die Person Deutsch sprechen, denn die Sprache der Gruppe ist Deutsch 

zu "Guia": Hier wurde "Paulo Baron" ausgewählt, weil er Deutsch spricht.

zu "Veículo / Motorista": Hier wurde das Auto mit dem Kennzeichen UAY7D24 ausgewählt, da es eine minimale Kapazität von 4 Personen hat (Die Anzahl der Personen ergibt sich aus den Keys "pax" und "numero_de_guias_externos". Der Guia und der Fahrer werden nicht mit einberechnet. Außerdem darf Paulo Baron das Auto fahren, wie man anhand der Daten in "all_guides" sehen kann. Der entgültige Wert im Feld setzt sich aus dem  "marca_modelo" - "numero_do_carro" - Hauptkey (Autokennzeichen) - Fahrer zusammen. Wenn es eine Gruppe gibt, deren Summe von "pax" und "numero_de_guias_externos" die Variable maximum_group_size_with_only_one_person übertrifft oder der Key "pagou_pelo_guia_extra" die Value True, sollten 2 verschiedene Personen als Guia und Fahrer eingeteilt werden, da die Arbeit für eine Person sehr stressig wird.

Wichtig zu wissen:
1) Gehen wir von der folgenden Situation aus: Es gibt 19 Gruppen mit 3 oder weniger Personen. Wir haben aber nur 17 Autos verfügbar, die eine maximale Kapazität von 3 Personen haben. In diesem Fall sollen die nächstgrößeren Autos für die 2 übrigen Gruppen genommen werden. Diese Anforderung zählt natürlich nicht nur für die kleinsten Gruppen, sondern für alle Gruppen.

2) Sollten die Autos nicht für alle Gruppen reichen, soll ein Vermerk auftauchen, dass weitere Autos für die übriggebliebenen Gruppen angemietet werden muss. 

3) Da es sich um den Fahrplan eines Tages handelt, darf jeder Fahrer, Guide und jedes maximal nur einmal benutzt werden. Es darf keine Überschneidungen geben! 

Deine Ausgabe soll kein Markdown sein. Mir reicht eine List of Lists vorerst. 

