# Download  der Distribution

Zunächst habe ich das x86_64 DVD Image von [https://software.opensuse.org/distributions/leap](https://software.opensuse.org/distributions/leap) heruntergeladen. Auf dieser Seite findet man auch nützliche Hinweise darauf, wie man daraus eine DVD brennt oder einen bootbaren USB-Stick erstellt.

Ich habe mich für die DVD entschieden. Das geht unter Windows 7 ganz leicht: Rechtsklicka auf das Image und "DVD brennen" auswählen. Ich habe dann noch den Haken bei der Option gesetzt, das Ergebnis zu verifizieren. Das war sehr nützlich, denn der erste Rohling machte gleich Probleme und war nichtz benutzbar. Beim zweiten Mal klappte alles reibungsfrei.

# Installation

DVD eingelegt, Boot Menu aufrufen und vond er DVD starten. Im wesentlichen habe ich mich dann an die Standardvorgaben gehalten. Nachdem ich eine zusätzliche SSD installiert hatte, habe ich dem Installer im entsprechenden Dialog diese angeboten. Die Standardvorgabe, von den 500GB nur 40GB für die Root Partition zu verwenden und den gesamten Rest der `/home` Partition zuzuschlagen wollte ich aber ändern. Denn ein Großteil meiner Daten liegt ja auf einer weiteren getrennten Festplatte. `/home` muss also nur die Linux-spezifischen Daten enthalten. Die Fotosammlung bleibt z.B. aber auf der Festplatte.

Um die Größe der Partitionen zu ändern muss man den Experten-Modus wählen. Davon bin ich zuerst auch zurückgeschreckt, aber auch hier wird man gut geführt. Ich habe im Assistenten lediglich die Größen verändert und die Auswahl von btrfs für das Root Dateisystem und xfs für die `/home` Partition beibehalten. Über Vor- und Nachteile von Dateisystemen lässt sich trefflich stretien - mein Argument war, dass ich mich möglichst weitgehend an die Standardeinstellungen von SUSE halten und nicht grundlos davon abweichen wollte.

Sonst gab es nichts besonderes bei der Installation - hat einfach funktioniert!

Nach der Installation wurden noch jede Menge Updates installiert. Und dann war das System fertig!

# Dual boot

Der Installer hat auzf der neuen SSD auch gleich den GRUB Bootloader installiert der nun anbietet Linux oder Windows zu booten. Im BIOS habe ich deshalb die neue SSD als Boot Device eingetragen. Dadurch wird GRUB gestartet, und dann kann ich wählen, welches Betriebssystem denn laufen soll. Die Standardvorgabe ist erst einmal Linux. Das kann man über YaST leicht ändern, und um die anderen Familienmitglieder nicht unnötig zu verwirren, habe ich erst einmal Windows als Standard eingestellt.

Jetzt, schon einen Monat später, ist Linux aber schon so weit, dass ich die Standardeinstellung wieder zurück auf Linux stellen konnte!

# NTFS Dateisystem einbinden

Startet man den Doplhin File Manager, dann erscheint die NTFS-formatierte Festplatte, auf der meine Windows Datedn liegen, dort mit einem roten Icon. Ein Klick darauf verlangt die eingabe des Passwortes, dann wird die Partition automatisch unter `/run/media` eingebunden. Diese Prozedur muss man aber nach jedem Neustart wiederholen.

Ich wollte aber, dass die Partition automatisch nach dem Booten zur Verfügung steht - ohne Passwortabfrage. Dazu bin ich wie folgt vorgegangen:

Zuerst habe ich ein Verzeichnis angelegt, das als dauerhafter Mount Point für die Partition dienen kann. `/run/media` eignet sich dazu nicht, da dieses Verzeichnis ja nicht persistent ist. Meine Wahl viel auf `/windows/d` und ich habe eine `Konsole` geöffnet und das Verzeichnis mit dem Befehl `sudo mkdir -p /windows/d` angelegt.

Dann habe ich dort nach der UUID des Laufwerks gesucht. Das Kommando `ls -l /dev/disk/by-uuid/` liefert etwa folgende Ausgabe:

```
lrwxrwxrwx 1 root root 10  4. Mai 15:07 4078961A78960EB2 -> ../../sda2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 666A8B5F6A8B2B3F -> ../../sda1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86840bcb-52b8-46c7-9e24-319322e71e6c -> ../../sde2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86941f9b-dd5d-47f8-8b25-346f91850258 -> ../../sde3
lrwxrwxrwx 1 root root 10  4. Mai 15:07 CA04184404183643 -> ../../sdb1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 e506251e-497e-4780-800b-7a1d0e4a2260 -> ../../sde1
```

`sda` ist höchst wahrscheinlich dasd Laufwerk mit der Windows Boot Partition. Hier sind zwei Partitionen auszumachen, wobei eine wohl eine System rettungspartition ist und die andere das Drive C:. 

`sdb` ist wohl meine Festplatte, also Drive D: unter Windows. Dieses Laufwerk möchte ich unter Linux ansprechen können. Ich habe die UUID markiert und in die Zwischenablage kopiert.

Die braucht man jetzt nämlich, um den richtigen Eintrag in der `/etc/fstab` hinzuzufügen. Dazu habe ich Kate als Superuser per `SUDO_EDITOR=kate sudoedit /etc/fstab` gestartet und die folgende Zeile hinzugefügt:

```
UUID=CA04184404183643   /windows/d    ntfs-3g user,users,uid=myuser,gid=users,umask=0002  0 0
```

Die UUID muss natürlich der oben ermittelten entsprechen, und der Username `myuser` sollte durch denjenigen User ersetzt werden, dem die Dateien auf der Partition gehören sollen. Das ist nämlich ein Punkt, den es zu beachten gilt: NTFS hat ein ganz anderes Rechtesystem als Linux. Beim Mounten wird deshalb ein Linux-User ausgewählt, der als Eigentümer der Dateien gilt. Schaut man sich neu angelegte Dateien dann unter Windows an, dann hat dort jeder Benutzer alle Zugriffsrechte auf solche Dateien. Die Rechte bestehender Dateien werden jedoch nicht verändert.

Nach dem nächsten Reboot ist das Laufwerk jedenfalls automatisch gemountet und Dolphin zeigt von Anfang an ein grünes Icon.
