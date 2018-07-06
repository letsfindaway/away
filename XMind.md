# XMind

XMind ist eine Eclipse-basierte Mind Mapping Software, die es auch für Linux gibt. Aber Linux ist nicht gleich Linux und was man da bekommt ist so definitiv nur auf Debian-basierten Systeme lauffähig, die nicht mehr als Java 8 installiert haben. openSUSE bringt schon mal Java 10 mit, und auch das ist ein kleines Problem.

Meine Anleitung zum Installieren von XMind sieht nun nach einigen Experimenten und Recherchen wie folgt aus:

* XMind für Linux von https://www.xmind.net/download/linux/ herunterladen
* Das ZIP-Archiv in einen Order der Wahl auspacken, z.B. nach `~/XMind`
* Die Datei `~/XMind/XMind_amd64/XMind.ini mit `kate` öffnen und wie folgt ändern:

```
-configuration
./configuration
-data
../workspace
-startup
../plugins/org.eclipse.equinox.launcher_1.3.200.v20160318-1642.jar
--launcher.library
../plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.400.v20160518-1444
--launcher.defaultAction
openFile
--launcher.GTK_version
3                                <-- da stand eine 2
-vmargs
-Dfile.encoding=UTF-8
--add-modules=java.se.ee         <-- diese Zeile ist neu, siehe https://aur.archlinux.org/packages/xmind/
```
* z.B. mit der YaST Softwareverwaltung prüfen, dass folgende Pakete installiert sind
  * java-10-openjdk
  * libgtk-3-0
  * libwebkit2gtk-4_0-37
  * lame 
  * glibc
  * libglib-2_0-0
* den Inhalt des Ordners `~/XMind/fonts` in einen neu zu erstellenden Ordner `/usr/share/fonts/truetype/xmind/` kopieren
* den Befehl `sudo fc-cache -f` ausführen, um den Font Cache neu aufzubauen
* von https://software.opensuse.org//download.html?project=home%3Asdrahn%3Aktrepte&package=xmind das experimentelle xmind Paket herunterladen, mit `ark` öffnen und die Dateien von `share` nach `.local/share` kopieren.
* `xmind.desktop` an die neue Versionsnummer 8 anpassen
* Dort außerdem die Exec-Zeile anpassen: `Exec=cd /home/family/XMind/XMind_amd64 && ./XMind %U` oder ein Starterskript nach `~/bin` legen.

