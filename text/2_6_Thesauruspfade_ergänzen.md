## Thesauruspfade via GeoNamesID ergänzen

Für den Import nach Imdas müssen wir als Letztes die Ortsbezeichnungen mit den in IMDAS verwendeten Ortsthesauri abgleichen und den Thesauruspfad des entsprechenden Ortes eintragen (s. Abschnitt [2.1](2_1_IMDAS-Import.md)).

Im folgenden werden wir folgende Schritte durchführen:
- Zunächst müssen wir in unsere Körperschafts-Tabelle wieder mittels reconciliation eine ID ergänzen: und zwar die GeoNames-ID der Orte.
- Dann müssen wir die Exporttabelle des IMDAS-Ortsthesaurus in OpenRefine laden. Wichtig sind in dieser Tabelle die Spalten `GeoNamesID` und `PFAD`.[^3]
- Schließlich nutzen wir in OpenRefine die GREL-Funktion [`cross()`](https://openrefine.org/docs/manual/grelfunctions#crosscell-s-projectname-optional-s-columnname-optional), die es uns erlaubt, Daten zwischen verschiedenen OpenRefine-Projekten auszustauschen.
So können wir über den Abgleich der GeoNamesID in beiden Tabellen den passenden Thesauruspfad in das Körperschafts-Datenset laden.

[^3]: Der Export des Ortsthesaurus kann durch das BSZ vorgenommen werden.

### Reconciliation mit GeoNames

Der Abgleich mit GeoNames läuft ähnlich wie [im Abschnitt vorher](2_5_Normdatenabgleich.md) beschrieben.
Als webservice für GeoNames geben wir unter `Add standard service...` die URL `https://fornpunkt.se/apis/reconciliation/geonames` ein.[^4]
Die reconciliation führen wir in der Spalte `Ort` durch.

Nach dem matchen der Ortsbegriffe mit GeoNames, können wir wieder über das Spaltenmenü -> `Reconcile` -> `Add entity identifiers column...` die GeoNames-IDs in einer eigenen Spalte namens `GeoNamesID` ergänzen.

[^4]: Der von der schwedischen Citicen Science-Plattform fornpunkt.se angebotene reconciliation-service für GeoNames bietet weniger Funktion an als z. B. die GND-Schnittstelle von lobid. Ein alternativer Weg wäre, zunächst die Orte mit wikidata zu matchen, um aus wikidata die GeoNames-ID zu ergänzen. 

### Abgleich mit dem Thesaurusexport

Für die Pfade müssen wir als nächstes die Excel-Tabelle mit den Thesaurusexport in OpenRefine laden.
Laden Sie für dieses Beispiel die Tabelle ["Export_Ortsthesaurus.xlsx"](../data/Export_Ortsthesaurus.xlsx) aus diesem Repository herunter.
Über den `Open...`-Button im oberen rechten Eck öffnet sich ein neuer Tab im Browser, und wir laden die Export_Ortsthesaurus.xlsx wie [zu Beginn beschrieben](2_2_Installation.md).
In der Vorschau geben wir dem neuen Projekt unter "Project name" den Namen "Ortsthesaurus".

Nun wechseln wir wieder in den Tab mit unseren Körperschafts-Daten.
Dort lassen wir aus der GeoNames-ID-Spalte eine neue Spalte erstellen (Spaltenmenü -> `Edit column` -> `Add column based on this column...`) mit dem Titel `Thesauruspfad`.
In das Expression-Fenster geben wir nun die cross-Funktion ein:

`cell.cross("Ortsthesaurus", "GeoNamesID")[0].cells["PFAD"].value`

Im Grunde bedeutet dieser Ausdruck:
1. `cell.cross("Ortsthesaurus", "GeoNamesID")`: Gehe in das Projekt "Ortsthesaurus" und Vergleiche die Werte in dieser Spalte mit der dortigen Spalte "GeoNamesID" ab.
2. `cells["PFADE"].value`: Stimmen diese Werte und die GeoNames-ID des "Ortsthesaurus"-Projektes überein, ergänze hier den entsprechenden Wert aus der Spalte "PFAD" des Projektes "Ortsthesaurus".

![Spalte ergänzen durch corss-Funktion](../images/cross.png)
*Ergänzen der Thesauruspfade aus der Export_Ortsthesaurus.xlsx in die Körperschaften-Tabelle mittels `cross()`-Funktion.*

Nachdem wir uns über die Vorschau versichert haben, dass die Thesauruspfade korrekt übernommen werden, und wir die Transformation bestätigen, bleibt uns nur noch, die Spalten `Ort` und `GeoNamesID` zu löschen, und die Spalte `Thesauruspfad` in `Ort` umzubenennen.

Und wenn die Reihenfolge der Spalten [wie am Anfang genannt](2_1_IMDAS-Import.md) stimmt, haben wir nun eine für den Import nach Imdas fertig aufbereitete Tabelle mit Körperschaften.

[Vorige Seite](./2_5_Normdatenabgleich.md) | [Inhaltsverzeichnis](../README.md) | [Nächste Seite](./3_Fazit.md)
