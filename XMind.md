# XMind

XMind ist eine Eclipse-basierte Mind Mapping Software, die es auch für Linux gibt. Aber Linux ist nicht gleich Linux und was man da bekommt ist so definitiv nur auf Debian-basierten Systeme lauffähig, die nicht mehr als Java 8 installiert haben. openSUSE bringt schon mal Java 10 mit, und auch das ist ein kleines Problem.

Zunächst stand an dieser Stelle eine ziemlich lange Anleitung, wie man das Ding zum Laufen kriegt. Doch dann habe ich auf dem openSUSE Build Service mein eigenes Paket für XMind gebaut. Jetzt kann ich (und jeder andere auch) es einfach aus meinem eigenen Repository installieren!

Den Build selber kann man hier einsehen: https://build.opensuse.org/package/show/home:letsfindaway/XMind

Das Repository liegt unter https://download.opensuse.org/repositories/home:/letsfindaway/openSUSE_Leap_15.0/ und kann wie jedes andere Repository in die Softwareverwaltung eingebunden werden. Danach steht XMind zur Installation zur Verfügung.

Meine Änderungen am Original betreffen insbesondere:

* Verwendung von gtk3 statt gtk2
* Hinzufügen der Option `--add-modules=java.se.ee` in die XMind.ini, die für Java > 8 erforderlich ist

Der Build steht momentan ausschließlich als 64-Bit-Build für openSUSE Leap 15.0 zur Verfügung. Die im Originalpaket enthaltenen Fonts werden momentan nicht installiert, ich plane aber ein XMind-fonts Paket.
