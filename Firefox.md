# Firefox

Firefox kommt vorinstalliert mit openSUSE, da ist also nicht viel zu tun. Die nette openSUSE Startseite mit dem farben-wechselnden Chamäleon kam jedenfalls auch bei den anderen Familienmitgliedern gut an und hat die Akzeptanz für meine Linux-Ambitionen gleich merklich gesteigert! Ja, manchmal sind es auch die kleinen Spielereien...

Die Lesezeichen habe ich mit dem Firefox Lesezeichen-Manager in ein JSON File exportiert und auf Linux wieder importiert. Ich habe mir keine Mühe gemacht, sie auf Dauer zu synchronisieren, nachdem Windows ja sowieso in Rente geschickt werden soll. Und eine Online-Synchronisation mit irgendeinem Dienst würde ich wirklich gerne vermeiden. Ich steige ja gerade auf Linux um, weil ich Kontrolle über meine Daten behalten möchte. Da gehören definitiv auch Lesezeichen dazu.

# KeePass

Unter Windows habe ich alle meine Passwörter mit KeePass verwaltet. Das Kee Plugin macht sie dann in Firefox verfügbar.

KeePass läuft auch unter Linux, wobei es ein Windows .NET Programm bleibt, das unter `mono` ausgeführt wird. Auf [https://keepass.info/help/v2/setup.html#mono](https://keepass.info/help/v2/setup.html#mono) kann man einige Informationen dazu finden, wie das zu installieren ist. Aber diese werden nicht einmal benötigt. denn SUSE hat bereits ein fertiges Paket für KeePass im Repository liegen, das alles Notwendige mitbringt und die nötigen Abhängigkeiten mitinstalliert! Ich musste also nur die Softwareverwaltung von YaST starten, nach keepass suchen und das angebotene Paket installieren.

Nach dem ersten Start musste ich nun die Datei mit meinen Schlüsseln finden, die auf dem Windows NTFS Laufwerk liegt. Wenn ich im Datei-öffnen Dialog von KeePass auf "My Computer" klicke, erhalte ich aber eine lange Liste von Einträgen der Art `HDD (none, sdb1)`. Über den Gerätenamen und die Infos, die ich beim Mounten des Laufwerkes gesammelt habe, konnte ich aber den richtigen Eintrag identifizieren und meine Schlüsseldatei auswählen. Zum Glück merkt sich KeePass diese für weitere Aufrufe.

Standardmäßig kommt KeePass mit einer englischen Bedienoberfläche. Hier hat sich SUSE nicht die Mühe gemacht, die ganzen Sprachpakete ebenfalls über das Repository mit auszuliefern.

Um die Sprache zu ändern habe ich zuerst im Menu Tools -> Change language ausgewählt. Da wird erst einmal nur Englisch angeboten. Unten gibt es aber einen Button "Download more languages...", der auf eine Webseite führt, von der weitere Sprachpakete heruntergeladen werden können. Ich habe die passende deutsche Sprachdatei ausgewählt, heruntergeladen und as zip-Archiv ausgepackt. Darin befindet sich lediglich eine einzige Datei `German.lngx`. Die muss nun an die passende Stelle! Dazu muss man Dolphin im Administrator-Modus starten, was sich leicht aus dem Startmenu und dem System Untermenu heraus bewerkstelligen lässt. Jetzt dort zum Ordner `/usr/lib/keepass` navigieren und dort einen Unterordner `Languages` anlegen. Dahinein muss nun das Sprachpaket kopiert werden. Jetzt kann man auch Deutsch als Sprache auswählen.

# Kee

Kee ist das Firefox Plugin, das Zugriff auf die in KeePass gespeicherten Daten erlaubt. Man kann es einfach über den Firefox Plugin Manager installieren und erhält dann weitere Informationen zum Vorgehen. Wie unter Windows, so muss man auch unter Linux die Datei `KeePassRPC.plgx` in ein Verzeichnis `plugins` unterhalb von `/usr/lib/keepass` kopieren. Der Administrator-Dolphin aus dem vorigen Abschnitt leistet ahci hier gute Hilfe!

Nach dem nächsten Neustart von Firefox muss man noch - wie von Windows gewohnt - einen Key von Kee in ein Popup-Fenster von KeePass kopieren, um den Zugriff auf die Daten zu erlauben. Dann funktioniert alles so wie von Windows gewohnt.
