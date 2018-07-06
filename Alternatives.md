# Alternativen

Einige Programme werden nicht unter Wine laufen und haben auch keine direkte Entsprechung unter Linux. Macht nichts! Die Linux Softwarewelt ist riesig und da werde ich doch schon etwas passendes für mich finden!

## Moneyplex: Alternative für VR NetWorld (Banking Programm der VR Banken)

Auch an das Homebanking habe ich einige Ansprüche. So möchte ich kein browserbasiertes Banking nutzen und habe für meine Hausbank HBCI mit Chipkarte. Auch die freiberufliche Tätigkeit meiner Frau führt zu weiteren Anforderungen. Drei Punkte stehen deshalb als Muss auf der Liste:

* Unterstützung von HBCI (FinTS) mit Chipkarte
* Unterstützung von Lastschriften
* Unterstützung des Abrufs von Kontoauszügen
* Gute Importunterstützung für Aufträge

Beim Kontoauszug meine ich nicht nur die Umsatzanzeige, sondern den Abruf eines PDF Dokumentes, das als Ersatz für den schriftlichen Kontoauszug der Bank dient. Das können nicht alle Programme, insbesondere auch nicht das unten erwähnte Hibiscus.

Das einzige Programm, das ich gefunden habe und das alle diese Anforderungenw erfüllt, ist [Moneyplex](http://www.matrica.de/produkte/produktmpx.html) von Matrica Software. Ich benötige außerdem die Business-Variante für 139,- €.

Vielleicht sollte ich das hier noch einmal betonen: es geht mir beim Linux-Umstieg nicht darum, alles kostenlos zu bekommen. Es geht mir darum, meine Daten bei mir zu behalten und nicht dem Softwaregiganten Microsoft ausgeliefert zu sein. Gute Software darf gutes Geld kosten, das ich gerne bezahle.

Ein erster Versuch mit der Trial Variante verlief allerdings zunächst erfolglos. Der Grund war aber wohl ein unglückliches Zusammentreffen mit einem Versionswechsel. Ein Anruf beim Support endete nicht in einer Warteschleife, sondern sofort bei einem kompetenten Mitarbeiter, der mir alle notwendigen Informationen gab. Auch zur Installation und Konfiguration des Smart Card Readers hatte er einige Hinweise parat. Daneben gibt es bei Matrica auch ein Wiki mit wertvollen Informationen zum Banking unter Linux. Hat man einen Chipkartenleser, so ist z.B. [das Abschalten der Stromsparfunktion](http://wiki.matrica.com/index.php/Cyberjack#Stromsparfunktion_bei_pcsc-Dienst_deaktivieren) wichtig! Update: mit der aktuellsten Version von Suse Leap 15.0 scheint diese Änderung schon eingeflossen zu sein!

Minuten später hatte ich den Link zur brandneuen 2018er-Version. Die Installation verlief problemlos und kurze Zeit später hatte ich vier verschiedene Banken online, eine mit Chipkarte, eine mit TAN Generator, die dritte mit TAN Liste und die vierte mit einem stark eingeschränkten Banking. Alle Varianten werden problemlos unterstützt.

ich denke als deutscher Anwender mit Anforderungen, die über [Hibiscus](https://www.willuhn.de/products/hibiscus/) hinausgehen, ist Moneyplex die Alternative der Wahl!

## BackupServiceHome

Beim Backup habe ich lange rumgesucht. Schließlich habe ich zwei Favoriten gefunden:

* backintime
* borg

Backintime kommt mit einer netten grafischen Oberfläche. Wie der Name schon sagt, kann man den Zustand der gesicherten Verzeichnisse zu jedem Backup grafisch anschauen und leicht Dateien zurückkopieren. Im Hintergrund arbeitet rsync, das für inkrementelle Backups zuständig ist. Auch ohne das Tool kann man alle Dateien auf der Sicherungsplatte als normale Dateien ansprechen. Für nicht geänderte Dateien wir dein Hardlink auf die letzte Version angelegt.

borg besticht dagegen durch viele Features: Backups werden dedupliziert, komprimiert und verschlüsselt. Die Dateien auf der Platte sind dann aber nur Chunks von 500MByte Größe. Zugreifen kann man auf die Sicherungen, indem man sie wie ein Filesystem mountet. Dann hat man ebenfalls Zugriff auf alle Dateien zu allen Sicherungszeitpunkten -- allerdings braucht man dazu eben borg. Ohne das Tool ist kein Zugriff möglich. Eine schöne grafische Oberfläche gibt es aber nicht.

Schließlich habe ich mich für borg entschieden. Die Deduplizierung verringert die Größe des Backups paralleler wine Prefixe. Sichert man sehr viele Dateien (ich habe alleine 40.000 Fotos!), dann sind die Hardlinks auch keine schöne Sache und das Erzeugen dieser Links dauert länger als der ganze restliche Backup-Vorgang.

Will man es einfach haben und hat keine so riesige Anzahl an Dateien, dann würde ich backintime empfehlen. Wer mehr Features haben will, der könnte mit borg sehr gut bedient sein. Beide Tools sind im Standard Repository von openSUSE zu haben.

Damit aber das Mounten von Backups als virtuelles FUSE Dateisystem funktioniert, brauch man noch das Paket `python3-llfuse`, das mal wieder nicht in den Standard-Repositories verfügbar ist. Fündig geworden bin ich dann unter `http://download.opensuse.org/repositories/filesystems/openSUSE_Leap_15.0`. Ich habe dieses Repository mit Prio 100 hinzugefügt und dann das Paket von dort installiert. Dann funktioniert auch `borg mount` ohne Probleme!

## Kate: alternative for Notepad++

Der KDE Standard Text Editor Kate hat alles was ich erst mal brauche.

## Putty

Der Konsolen - `ssh` Client ist eigentlich ausreichend für die wenigen Male wo ich eine ssh-Verbindung brauche. Also auch hier kein Ersatzbedarf.

## WinSCP

`Dolphin`, der Standard File Manager von KDE unterstützt bereits von Hause aus `SFTP`. In der Ansicht mit zwei nebeneinanderliegenden Verzeichnissen ist das Kopieren einfach und bequem möglich. 

## Ulead PhotoImpact

I liked this graphics program a lot on Windows, because it offers a rich feature set without the steep learning curve other programs require. It also allows to use a scanner from within the program.

Working through the huge list of possible alternatives is still a 

TODO
