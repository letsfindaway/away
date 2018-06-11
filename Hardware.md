# Hardware

## Momentane Ausstattung

Mein Rechner ist zur Zeit mit zwei Laufwerken ausgerüstet:

* eine 250 GB SSD für Betriebssystem und Software (Drive C:)
* eine 2 TB Festplatte für alle meine Daten, Fotos usw. (Drive D:)

Auch Linux möchte ich unbedingt von SSD booten, denn den Geschwindigkeitsvorteil eines nicht-rotierenden Massenspeichers möchte ich nicht mehr missen! Die bestehende SSD will ich aber auch nicht repartitionieren. Der Aufwand wäre groß, die Gefahr, dass was schiefgeht, hoch, und 250GB sind auch nicht die Welt.

## Upgrade

Deshalb habe ich mich entschlossen für Linux eine weitere SSD einzubauen - eine 500 GB Samsung Evo 860. Da soll die Linux Installation drauf und auch das Linux `/home` Verzeichnis. Außerdem soll da der GRUB Bootloader installiert werden und dafür sorgen, dass Linux und Windows alternativ gestartet werden können.

Platz war noch reichlich vorhanden, ein freier 6GB/s SATA Port ebenfalls. Damit war dieser Teil nicht sehr kompliziert. Neben dem Laufwerk und einem SATA Kabel habe ich noch einen Einbauadapter benötigt, um das Laufwerk befestigen zu können und ein Adapterkabel für die Stromversorgung, weil das Netzteil keinen geeigneten Anschluss mehr frei hatte.

Die 2 TB Festplatte soll sowohl von Windows als auch von Linux benutzt werden können. So sind alle meine Daten vom ersten Tag an unter beiden Betriebssystem verfügbar, egal ob ich Windows oder Linux boote. Das macht dem Umstieg erheblich einfacher, insbesondere einen weichen Umstieg, so wie ich ihn vorhabe. Die Unterstützung für NTFS in Linux ist inzwischen so ausgereift, dass es problemlos möglich ist, dieses Filesystem auch unter Linux einzusetzen - zumindest für die nächsten Monate. Ist dann Windows irgendwann komplett von meinem Rechner verschwunden, dann werde ich auch dieses Laufwerk auf ein Linux-Dateisystem migrieren.
