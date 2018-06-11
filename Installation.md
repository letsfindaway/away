# Download  der Distribution

Zunächst habe ich das x86_64 DVD Image von [https://software.opensuse.org/distributions/leap](https://software.opensuse.org/distributions/leap) heruntergeladen. Auf dieser Seite findet man auch nützliche Hinweise darauf, wie man daraus eine DVD brennt oder einen bootbaren USB-Stick erstellt.

Ich habe mich für die DVD entschieden. Das geht unter Windows 7 ganz leicht: Rechtsklicka auf das Image und "DVD brennen" auswählen. Ich habe dann noch den Haken bei der Option gesetzt, das Ergebnis zu verifizieren. Das war sehr nützlich, denn der erste Rohling machte gleich Probleme und war nichtz benutzbar. Beim zweiten Mal klappte alles reibungsfrei.

# Installation

DVD eingelegt, Boot Menu aufrufen und vond er DVD starten. Im wesentlichen habe ich mich dann an die Standardvorgaben gehalten. Nachdem ich eine zusätzliche SSD installiert hatte, habe ich dem Installer im entsprechenden Dialog diese angeboten. Die Standardvorgabe, von den 500GB nur 40GB für die Root Partition zu verwenden und den gesamten Rest der `/home` Partition zuzuschlagen wollte ich aber ändern. Denn ein Großteil meiner Daten liegt ja auf einer weiteren getrennten Festplatte. `/home` muss also nur die Linux-spezifischen Daten enthalten. Die Fotosammlung bleibt z.B. aber auf der Festplatte.

Um die Größe der Partitionen zu ändern muss man den Experten-Modus wählen. Davon bin ich zuerst auch zurückgeschreckt, aber auch hier wird man gut geführt. Ich habe im Assistenten lediglich die Größen verändert und die Auswahl von btrfs für das Root Dateisystem und xfs für die `/home` Partition beibehalten. Über Vor- und Nachteile von Dateisystemen lässt sich trefflich stretien - mein Argument war, dass ich mich möglichst weitgehend an die Standardeinstellungen von SUSE halten und nicht grundlos davon abweichen wollte.

Sonst gab es nichts besonderes bei der Installation - hat einfach funktioniert!

Nach der Installation wurden noch jede Menge Updates installiert. Und dann war das System fertig!

# Dual boot

The installer finally installed a grub bootloader on the new SSD which offers to select from either Linux or Windows. I therefore activated the new hard disk as first boot device in the BIOS setup and selected to have Windows as default for the time being. This adjustment can easily be done from the Yast bootloader configuration.

# Mounting the NTFS file system

When startibng the Dolphin file manager the Windows partitions are indicated under "Devices" with a red icon. When you klick on this icon you have to enter your password. The partition is then automatically mounted under some subdirectory of `/run/media`. However this procedure has to be followed after each reboot.

I wanted to have the partition mounted immediately after booting Linux. Do achieve this I followed the following steps:

First create a directory which can act as mount point for the partition. I chose `/windows/d` and created the directory with the command `sudo mkdir -p /windows/d`

Then open a Konsole and enter the command `ls -l /dev/disk/by-uuid/`. This gives you some output like

```
lrwxrwxrwx 1 root root 10  4. Mai 15:07 4078961A78960EB2 -> ../../sda2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 666A8B5F6A8B2B3F -> ../../sda1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86840bcb-52b8-46c7-9e24-319322e71e6c -> ../../sde2
lrwxrwxrwx 1 root root 10  4. Mai 15:07 86941f9b-dd5d-47f8-8b25-346f91850258 -> ../../sde3
lrwxrwxrwx 1 root root 10  4. Mai 15:07 CA04184404183643 -> ../../sdb1
lrwxrwxrwx 1 root root 10  4. Mai 15:07 e506251e-497e-4780-800b-7a1d0e4a2260 -> ../../sde1
```
`sda` is most probably the drive where your Windows boot partition is located, which corresponds to C:. I can see two partitions here, where one of them is a system rescue partition, the other is C:.

`sdb` is probably the second hard drive, mapped to D: under windows. This is the drive I want to access under Linux. Copy the UUID to the clipboard.

Then edit the `/etc/fstab` file using the command `SUDO_EDITOR=kate sudoedit /etc/fstab`. Add the following line:

```
UUID=CA04184404183643   /windows/d    ntfs-3g user,users,uid=myuser,gid=users,umask=0002  0 0
```

Replace the UUID with the value you got in the previous step and the uid `myuser` with the name of the user who should own the files on this drive. 

After the next reboot the drive will be automatically mounted and Dolphin shows a green icon from the beginning.
