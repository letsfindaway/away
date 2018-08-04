# Microsoft Access 2010 and TZ-EasyBuch

Microsoft Access 2010 does läuft nicht unter wine. Punkt.

Die Autoren der meisten Beiträge, die ich gefunden habe, hatten keinen Erfolg. Wenn jemand doch Access zum Laufen gebracht hat, dann nur zu kleinen Teilen.

Ich habe eine Microsoft Access Datenbank als Teil einer Buchhaltungslösung zusammen mit [TZ-EasyBuch](https://www.tz-easybuch.de/), und irgendwie muss ich diese Lösung auf Linux übertragen. Kunden und Rechnungen werden in der Datenbank abgelegt und bisher über das COM-Interface nach TZ-EasyBuch übergeben. Das Wird in Zukunft so nicht mehr gehen. Was tun?

Ich habe verschiedene Lösungsansätze untersucht und bin jetzt beim folgenden Ansatz gelandet:

* Übertragen der Access Datenbank nach LibreOffice Base
* Installation von TZ-EasyBuch unter wine
* Exportieren von Buchhaltungsdaten aus LibreOffice Base in CSV-Dateien und Importieren dieser Daten in TZ-EasyBuch

## Übertragen der Access Datenbank nach LibreOffice Base

Im Wesentlichen heißt das, die Datenbank neu aufzubauen. Die Skripte muss ich ebenfalls neu schreiben. Das Übertragen der Daten ist dann das kleinste Problem. Ich mache das unter Windows wie folgt:

* Unter Windows LibreOffice Base installieren (ich habe die Portable Version gewählt, aber das ist egal)
* Die notwendigen Tabellen in LibreOffice Base anlegen
* Access und Base parallel öffnen
* Daten aus den Tabellen per Copy/Paste kopieren. Wenn die Spalten passen, geht das ganz problemlos

## Installation von TZ-EasyBuch unter wine

TZ-EasyBuch läuft ohne irgendwelche besonderen Klimmzüge unter wine. Die Elster-Funktionen habe ich nicht getestet, da ich sie nicht benötige. Aber sonst scheint das ohne größere Probleme zu gehen.
