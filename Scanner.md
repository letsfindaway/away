
# Drucker

Für meine beiden Laserdrucker (Canon LBP3360 und Brother DCP-9020CDW) habe ich zunächst mit Freude festgestellt, dass Treiber für diese beiden einfach mit an Bord sind! Das [gutenprint-Projekt](http://gimp-print.sourceforge.net/) und [foomatic](https://wiki.linuxfoundation.org/openprinting/database/foomatic) unterstützen eine breite Palette an Druckern und ich habe beide Drucker erst einmal mit diesen Treibern zum Laufen gebracht. Oder besser: zum Schleichen. Denn manche Ausdrucke gar nicht so komplizierte Dokumente haben mehrere Minuten gedauert (pro Seite!), und zwar auf beiden Druckern.

Ich bin dann auf die Support-Seiten der Hersteller gegangen. Dort werden Linux-Druckertreiber für diese Modelle angeboten. Diese habe ich dann nach Anweisung installiert. Die Druckgeschwindigkeit hat sich dadurch erheblich verbessert.

# Scanner

## Installation des Brother Scanner Treibers

Ich habe einen Brother DCP-9020CDW Laser-Multifunktionsgerät, das drucken und scannen kann. Die Einbindung als Drucker gelingt über die normalen Systemwerkzeuge. Für den Scanner sind aber Treiber von Brother erforderlich. Glücklicherweise haben die meisten großen Hersteller aber erkannt, dass Treiber auch für Linux gefragt sind. Über die Brother Webseite kommt man unter "Support" zum Download der entsprechenden Pakete. 

Für mein Gerät habe ich von http://support.brother.com/g/b/downloadlist.aspx?c=de&lang=de&prod=dcp9020cdw_eu&os=127&flang=English den 64bit-Scanner-Treiber heruntergeladen. Per Klick auf das rpm-File lässt sich dieser einfach installieren. Startet man den Download, so erhält man weitere Instruktionen zur Installation. Für einen über Netzwerk angeschlossenen Scanner ist danach noch folgendes Kommando notwendig:

```bash
brsaneconfig4 -a name=(name your device) model=(model name) ip=xx.xx.xx.xx
```

Danach ist der Scanner in allen sane-kompatiblem Scan-Programmen verfügbar!

## Installation von gscan2pdf

Für mich gibt es zwei Einsatzfälle für den Scanner:

* Scannen einzelner Fotos, Grafiken oder sonstiger Vorlagen in ein .jpeg-File oder ein anderes Grafikformat, meist in Farbe
* Scannen mehrseitiger Dokumente in ein pdf-File, meist in Graustufen

Für den ersten Fall leistet das im Standardrepository verfügbare `xsane` gute Dienste. Es erlaubt die wichtigsten EInstellungen der Scanqualität, macht eine Vorschau, die es erlaubt, den endgültigen Ausschnitt festzulegen und kann dann das Ergebnis in einer Reihe unterschiedlicher Grafikformate speichern.

`skanlite` wäre auch ein Kandidat gewesen. Allerdings gab es bei diesem Programm immer einen Versatz zwischen dem Ausschnitt in der Vorschau und dem Scanergebnis. Deshalb setze ich stattdessen das ältere und auch optisch weniger ansprechende `xsane` ein.

Für den zweiten Fall habe ich in den Standard-Repositories erst mal kein passenden Programm gefunden. Vom Funktionsumfang her hat mir `gscan2pdf` gut gefallen, aber das ist in den Standardrepositories nicht verfügbar. Im Rahmen meiner Recherchen habe ich dann einiges über openSUSE Repositories gelernt.

Neben den standardmäßig eingebundenen Repositories bietet nämlich bereits openSUSE eine große Zahl weiterer Quellen für Software, die über den Open Build Service für openSUSE gebaut worden ist. EIn Blick nach http://download.opensuse.org/repositories/ lohnt sich: die Liste dort ist lang. Unter "Publishing" finden sich da Pakete, die nicht offiziell freigegeben sind, aber sich auf dem Weg dahin befinden. Dort ist auch `gscan2pdf` mit dabei. 

`gscan2pdf` braucht aber noch eine Reihe von perl-Modulen, die ebenfalls nicht im Standardrepository liegen. Doch auch dafür gibt es eine Quelle. Unter `devel:/languages:/perl` findet sich alles, was `gscan2pdf`braucht. Also muss man zwei neue Reporitories einbinden.

Dazu ruft man YaST auf und von dort die Verwaltung der Software-Repositories. Hier auf "Hinzufügen" klicken und die richtige URL eingeben. Dann noch einen Namen vergeben und die Priorität anpassen. Ich habe folgende URLs konfiguriert:

* https://download.opensuse.org/repositories/Publishing/openSUSE_Leap_15.0/ , Prio 100
* https://download.opensuse.org/repositories/devel:/languages:/perl/openSUSE_Leap_15.0/ , Prio 150

Damit kommen beide Repositories in der Reihenfolge nach den Standard-Paketquellen.

Nach der Einrichtung dieser Quellen kann dann `gscan2pdf` wie jede andere Software über YaST installiert werden. Das Paket hat Abhängigkeiten zu `texlive`, deren Ursache ich nicht näher untersucht habe. Das führt jedenfalls dazu, dass knapp 2 GByte und über 2000 Pakete installiert werden. Aber vielleicht kann ich TeX ja mal brauchen - und Platz ist noch reichlich vorhanden auf meiner root Partition!

Zuletzt habe ich noch in den Einstellungen statt des bevorzugten `libimage-sane-perl` das `scanimage` Frontend ausgewählt. Mit diesem hat die Bedienung des Dokumenteneinzugs erheblich besser funktioniert als mit der ursprünglichen Auswahl.

## gscan2pdf Publishing Package

Wer noch weiter reinschauen möchte, woher das Paket stammt, der kann sich auch den Open Build Service anschauen:

https://build.opensuse.org/package/show/Publishing/gscan2pdf
