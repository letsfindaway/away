# Cewe Fotobuch

Löblicherweise stellt Cewe seine Fotobuchsoftware auch für Linux zur Verfügung. Das fällt nicht schwer, ist sie doch mit dem Qt-Framework programmiert, das viele verschiedene Plattformen unterstützt.

Der Download erfolgt von https://www.cewe.de/bestellsoftware.html. Als Linux-Anwender kriegt man von dort gleich ein tgz-Archiv, das aber eigentlich nur ein Installationsskript enthält. Damit kann nun die Software in ein beliebiges Verzeichnis installiert werden. Typischerweise sollte man dafür ein Verzeichnis unterhalb des home-Verzeichnises verwenden, da dies eine benutzerspezifische Software ist, die nicht mit den Paketen des Systems vermengt werden sollte.

Beim Erstellen meines ersten Fotobuchs lief alles glatt - bis ich das fertige Buch zum Server übertragen wollte. Dort gab es lediglich einen `Fehler 10000`, und dann war Schluss. 

Ein Anruf bei der Hotline ergab, das dies auf ein Verbindungsproblem hindeutet. Eine Analyse per Wireshark zeigte, dass die Verbindung zwar aufgebaut, aber ohne TLS Handshake sofort wieder abgebaut wurde. Das gleiche Problem hatte ich auch bei meiner Banking Software Moneyplex! Und schließlich war auch die Lösung die gleiche: Beide Programme erwarten `openssl` in einer Version 1.0.x. openSUSE Leap 15.0 installiert aber zunächst nur `libopenssl1_1`. Nachinstallieren von `libopenssl1_0_0` löst das Problem für beide Programme! Die beiden `openssl`-Versionen können übrigens problemlos friedlich nebeneinander existieren. Sie werden auch beide gewartet, so dass Sicherheitspatche bei Bedarf für beide Versionen ausgerollt werden.
