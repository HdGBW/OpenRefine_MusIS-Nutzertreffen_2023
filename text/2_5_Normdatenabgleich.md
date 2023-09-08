## Normdatenabgleich

In diesem Abschnitt gehen wir nun daran, Spalte `Nachname` mit den Datensätzen der [Gemeinsamen Normdatei](https://www.dnb.de/DE/Professionell/Standardisierung/GND/gnd_node) abzugleichen, um die GND-ID der Körperschaften zu erhalten. 
Ein solcher Abgleich mit einem externe Webservice wird als "reconciling" bezeichnet.

Für die GND stellt das [Hochschulbibliothekszentrum des Landes NRW](https://www.hbz-nrw.de/produkte/linked-open-data) unter https://lobid.org/gnd/reconcile/ einen entsprechenden Dienst zur Verfügung.[^2]

Um diese URL in OpenRefine zu hinterlegen, muss im Menü der Spalte `Nachname` -> `Reconcile` -> `Start reconcoling...` angewählt werden, und im sich öffnenden Dialogfenster mit `Add standard sercice...` die lobid-URL eingegeben werden.

Nun steht der Service als "GND reconciliation for OpenRefine" zur Verfügung.

Wird dieser ausgewählt, öffnet sich ein Fenster, in dem der abzugleichende Entitätstyp ausgewählt werden kann. 
In unserem Fall wäre das die "Körperschaft".

> [!IMPORTANT] 
> Den Haken bei `Auto-match candidates with high confidence` abwählen.
> Ansonsten erstellt OpenRefine automatisch matches zu GND-Einträgen mit hoher Übereinstimmung - was allerdings nicht immer die tatsächlich gemeinte Entität sein muss.

![Reconciliation Detailfenster](../images/Reconciliation_window.png)
*Die Voreinstellungen zur reconciliation.*

Nach erfolgten Datenabgleich werden in den Zellen alle Datensätze angezeigt, die OpenRefine als ähnlich zum Zelleneintrag betrachtet.

![Anzeige des Reconciliation-Ergebnis](../images/Reconciliation.png)
*Das Ergebnis einer reconciliation mit Links zu GND-Datensätzen unter jedem Begriff.*

Unter jedem Begriff wird nun ein Link zum vorgeschlagenen Datensatz angezeigt.
Per Mouseover über den Link werden auch einige weiteren Informationen geladen - eine hilfreiche Funktion, um schnell zu sichten, ob es sich auch tatsächlich um die gesuchte Entität handelt.
Mit den Buttons `Match this cell` wird diese Zelle und mit `Match all identical cells` weden allen Zellen in der Spalte mit gleichen Wert diesem GND-Datensatz zugewiesen.
Sollten alle Vorschläge nicht stimmen, kann über `Search for match` nach weiteren möglichen Matches in der GND gesucht werden, oder mit `Create new item` festgelegt werden, dass es keinen Match gibt.

Nachdem wir allen Werte so einen GND-Eintrag zugewiesen haben, können wir nun Daten aus der GND ergänzen - wie z. B. die GND-ID.
Dafür gibt es bei OpenRefine eine eigene Funktion, die über das Spaltenmenü -> `Reconcile` -> `Add entity identifiers column...` aufgerufen werden kann. 

Für den Import nach Imdas muss diese Spalte zum einem als `Normdaten` betitelt werden, und zum anderen dem Schema `O-GND~{GND-ID}~https://d-nb.info/gnd/{GND-ID}` folgen (s. Abschnitt [2.1](2_1_IMDAS-Import.md)).
Für diese Transformation müssen wir über Spaltenmenü -> `Edit cells` -> `Transform...` das Fenster für die GREL-Expressions öffnen. 
Hier können nun diverse Transformationen mittels GREL durchgeführt werden.
Der Reiter "Help" listet eine kurze Dokumentation aller Funktionen auf.
`value` ist dabei der Stellvertreterterm für den tatsächlichen Zellenwert.
Da wir allerdings nur feste Textteile ergänzen wollen, kommen wir noch ohne Spezialfunktionen aus, und geben einfach nur folgendermaßen den gewünschten Textaufbau ein:

`"O-GND~" + value + "~https://d-nb.info/gnd/" + value`

Das Ergebnis der Transformation sehen wir im Preview. 

![Custom text transform](../images/Transforming.png)
*Transformations-Fenster mit Vorschau auf das Resultat.*

[^2]: Siehe für eine Zusammenstellung von Diensten für OpenRefines reconciliation-api https://reconciliation-api.github.io/testbench/#/.

[Vorige Seite](./2_4_Informationen_aufteilen.md) | [Inhaltsverzeichnis](../README.md) | [Nächste Seite](./2_6_Thesauruspfade_ergänzen.md)