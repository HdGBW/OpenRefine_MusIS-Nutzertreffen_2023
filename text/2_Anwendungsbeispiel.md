# Anwendungsbeispiel

Folgendes Beispiel stammte aus der geraden laufenden Datenbankumstellung am Haus der Geschichte Baden-Württemberg (HdGBW). Der Wechsel erfolgt von einer Eigenentwicklung aus dem Jahre 2001 nach ImdasPro, mit Unterstützung vom [BSZ](https://www.bsz-bw.de/MusIS.html).

Konkret sollen Adressangaben zu Körperschaften aus dem Feld "Herkunft/Leihgeber" bei Objektdatensätzen als Körperschafts-Datensätze in ImdasPro überspielt werden. 
Die alte Datenbank enthält keinen Adress- oder sonstige Stammdatenverwaltung, was zum einem bedeutet, dass dieses Feld ein Freitextfeld ist, und zum anderen, dass die selben Informationen (Name, Straße und Hausnummer, PLZ und Ort) bei jedem Objektdatensatz erneut eingegeben werden müssen. 
Entsprechend variantenreich können die Einträge ausfallen.

Die Schreibanweisung für das Feld lautet: 
> Name; Straße Hausnummer, PLZ Ort. 
Tatsächlich finden sich in den Feldinhalten Schreibvarianten, Typos und auch ausgelassene Informationen wie z. B. fehlende Straßennamen.

Als Grundlage für diese kleine Einführung in OpenRefine wurde von 25 exemplarischen Datensätzen die Inhalte des Feldes ausgelesen und hier im Repositorium unter der [Herkunft.xlsx](../data/Herkunft.xlsx) abgelegt.

[Vorige Seite](./1_Was_ist_OpenRefine.md) | [Inhaltsverzeichnis](../README.md) | [Nächste Seite](./2_1_IMDAS-Import.md)
