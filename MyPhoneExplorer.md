# MyPhoneExplorer

Dieses Windows-Tool habe ich schätzen gelernt. Es kann Kontaktdaten, Kalender, Nachrichten und Dateien zwischen Android Phones und Computer synchronisieren und vieles mehr. Unter Linux habe ich bisher nichts vergleichbares gefunden.

Die Berichte darüber, ob es unter wine läuft, sind zwiespältig. Die einen meine ja, die anderen nein, und eine richtige Analyse habe ich nirgends gefunden. Die will ich nun hier - soweit meine Erkenntnisse reichen - nachreichen. Zunächst: ja, es funktioniert. Allerdings muss man ein paar Dinge beachten und verstehen.

Bei der Installation unter wine verwendet man am besten einen neuen Präfix - PlayOnLinux macht das einfach - und eine aktuelle wine-Version. Dann kann man den Installer starten. Und nun kommt der erste wichtige Punkt:

__Unbedingt die "Portable" Installation wählen!__ Die "normale" Installation führt nicht zum Erfolg. Dann aber kann man MyPhomeExplorer erst mal starten.

Doch nun der zweite Punkt: MyPhoneExplorer findet das Telefon nicht :( Da ist zu beachten:

* Die Verbindung geht nur mit WLAN, nicht per USB!
* Und man muss die IP-Adresse von Hand vorgeben, die automatische Erkennung geht nicht.

Der erste Punkt hat damit zu tun, das wine generell für UBS keine Unterstützung bietet - jenseits vom Einbinden von Massenspeicher. Damit kann die Anbindung per USB mit wine nicht klappen.

Der zweite Punkt könnte an der Firewall liegen. Ich habe aber noch nicht mit den Einstellungen experimentiert. Stattdessen in MyPhoneExplorer die IP Adresse des Telefons einstellen. Diese bleibt typischerweise immer gleich, weil WLAN Router meist einem Gerät immer die gleiche Adresse zuweisen. Dann kann man in MyPhoneExplorer mit F2 die Einstellungen aufrufen, Verbindung wählen und dort "Fixe IP-Adresse" auswählen und die Adresse eingeben. Damit klappt die Verbindung!
