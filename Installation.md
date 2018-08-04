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

# Removable Devices

Die Partitionen meiner neuen SSD wurden von Dolphin und vom Gerätemanager als "Wechseldatenträger" erkannt, mit der Option, diese doch vom System zu trennen! Das ist bestimmt keine gute Idee. Woher das kommt und wie man das behebt ist eine etwas längere Story, die man unter https://www.opensuse-forum.de/thread/40568 nachlesen kann. Beim siebten Beitrag (https://www.opensuse-forum.de/thread/40568#post121460) steht die Lösung!

# Einige Wochen später ...

... war ich dann doch wieder etwas frustriert. Der Boot-Vorgang dauerte länger als bei Windows - fast doppelt so lang, und das trotz SSD an einem 6GB/s SATA Anschluss. Und manchmal blieb die Spash-Animation auch einfach hängen. Erst heftiges Drücken einiger Tasten, insbesondere die Umschaltung zwischen verschiedenen virtiuellen Bildschirmen mit Alt-F1 und Alt-F7 brachte dann wieder Leben in die Bude. Diesen Zustand konnte ich niemandem zumuten.

Habe ich nicht oben den guten Community Support gelobt? Den habe ich jetzt gleich ausprobiert, habe mich bei http://www.opensuse-forum.de angemeldet und einen [Thread](https://www.opensuse-forum.de/thread/40558) gestartet. Minuten später erhielt ich die ersten Hinweise. Parallel dazu habe ich natürlich auch selbst weiter nachgeforscht.

OpenSUSE ist mein erstes System, das mit `systemd` arbeitet und da muss ich mich erst noch einarbeiten. Aber was mir definitiv weitergeholfen hat ist das Kommando

```
sudo systemd-analyze plot > startup.svg
```

Die Ausgabedatei dann z.B. von Dolphin auf den geöffneten Firefox schieben. Die angezeigte Grafik zeigt ganz genau, wie der Boot-Vorgang abläuft und wer wofür wie viel Zeit braucht. Da waren dann insbesondere plymouth und wicked.service zu finden.

Plymouth ist der Splash Screen, der beim Booten diese nette Animation anzeigt. Er hat wohl den Hänger verursacht. Ich habe ihn nach Rückfrage im Forum einfach deinstalliert. 

Eine weitere Verzögerung entstand durch den IPv6 Stack in Verbindung mit meiner FritzBox. Auch das wohl ein bekanntes [Problem des wicked Netzwerkmanagers](https://github.com/openSUSE/wicked/issues/681). Ich habe deshalb wie geraten IPv6 deaktiviert. In meinem Heimnetz brauche ich es zumindest momentan auch definitiv nicht.

Und das Ergebnis: Ein sicher und schnell startendes System!

# Da capo

Und wieder einige Zeit später: nach dem Starten ist das System für ca 20 Minuten praktisch unbenutzbar. Ich habe es noch geschafft eine Konsole zu öffnen und `top` aufzurufen. Dort standen `btrfs-balance` und `btrfs-transaction` abwechselnd ganz oben und verbrauchten jeweils 100% CPU.

Die Meinungen und Diskussionen zu `btrfs` sind ja recht unterschiedlich. Ich habe daraufhin [diesen Thread](https://www.opensuse-forum.de/thread/40607) im openSUSE Forum gestartet. Die Antworten haben mich nicht von `btrfs` überzeugt. Wenn ich mal wieder ein paar Stunden Zeit habe, dann heißt das "da capo". Neuinstallieren mit `ext4` als root Filesystem.

Ein Filesystem muss für mich vor allem schnell, ruhig und zuverlässig und völlig unauffällig sein. Ein Filesystem, das regelmäßige Wartung braucht (und das nicht mal unauffällig im Hintergrund erledigen kann) und das mich von der Benutzung meines Rechners abhält, ist für meine Zwecke nicht brauchbar. 

Ich möchte ja immer möglichst nahe an der Distribution bleiben, möglichst wenig umkonfigurieren, und wenn dass System mal läuft, dann will ich auch nicht mehr viel verändern. Snapshots sind entbehrlich, wenn ich den Arbeitszustand von einer frischen Neuinstallation weg mit vertretbarem Aufwand herstellen kann. Genau das kann ich jetzt ja mal ausprobiereen, und genau deshalb schreibe ich mir hier auch meine Schritte auf! Hier der Plan:

* Neuinstallation Leap 15.0 von DVD mit folgenden Änderungen an der Partitionierung:
  * Entfernen der 300GB `btrfs` root Partition
  * Anlegen von zwei 150GB Partitionen. Eine wird dann die neue root Partition mit `ext4`, die andere bleibt in Reserve für den nächsten Versionssprung.
* Konfigurieren folgender Geräte
  * Drucker Canon LBJ3360 (mit dem Treiber von Canon)
  * Drucker Brother DCP-9020 (mit dem Treiber von Brother)
  * Scannereinheit des Brother DCP-9020 (mit dem Treiber von Brother)
  * Chipkartenleser ReinerSCT
* Editieren folgender Dateien
  * `/etc/fstab`, siehe oben
  * `/lib/systemd/system/pcscd.service` gemäß [dieser Anleitung von Matrica](http://wiki.matrica.com/index.php/Cyberjack) (PS: das scheint mit der aktuellen Leap 15.0 nicht mehr notwendig zu sein!)
* Installieren zusätzlicher Pakete
  * `wine`
  * `playonlinux`
  * `thunderbird`
  * `keepass`
  * `perl-Image-Sane`
  * `gscan2pdf-lang`
  * `xsane`
  * `owncloud`
  * `borg`
  * `borgmatic`
  * `photini`
  * `python3-requests`
  * `libopenssl1_0_0`
  
Das sollte es fast schon sein. Viele Pakete liegen auf meinem `/home`, so z.B. Moneyplex, die ganzen Dinge, die unter `wine` laufen, die Arduino IDE. Bin gespannt, wie reibungslos das läuft!

Das war dann mein kurzer Ausflug zu `btrfs`. Ich hab's probiert, aber in Zukunft gehöre ich zu denjenigen, die davon abraten.

## Problemlose Neuinstallation

Schon nach eine Stunde war der Rechner wieder einsatzbereit. Die Neuinstallation verlief deutlich besser, als ich mir das vorgestellt hatte. In der Tat war alles, was auf meiner `/home` Partiton stand, sofort wieder einsatzbereit. Drucker- und Scannertreiber musste ich neu installieren.
