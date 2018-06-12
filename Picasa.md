# Picasa

Den Bildermanager Picasa würde ich wirklich vermissen, wenn er unter Linux nicht verfügbar wäre. Picasa ist einfach zu benutzen und gestattet doch auf simple Weise die wichtigsten Bildbearbeitungen. Und jeder Bearbeitungsschritt kann auch später wieder rückgängig gemacht werden, weil das Originalfoto nicht verändert wird.

Eine echte Linux-Version von Picasa gibt es nicht. Aber PlayOnLinux - eine grafische Oberfläche für die Installation und Verwaltung von Programmen unter Wine, unterstützt Picasa anscheinend.

PlayOnLinux selbst ist einfach installiert, die openSUSE Repositories bieten es an. Bei der Installation von Picasa jedoch wollte PlayOnLinux eine 300MByte Datei für den Internet Explorer herunterladen. Nach 192MByte brach dieser Download reproduzierbar ab. Aber wozu brauche ich den Internet Explorer? Ich wollte doich nur Picasa installieren!

Eine Suche im Internet ergab, dass Picasa Teile des Internet Explorers benutzt, um sich bei Google anzumelden. Aber erstens gibt es die Google Webalben nicht mehr und zweitens würde ich ja genau das gerne vermeiden. Also zweiter Versuch: Picasa ohne Google.

Diesmal bin ich im Installationsdialog von PlayOnLinux auf den Button "Installiere ein Programm, das nicht aufgeführt ist" gegangen, habe einen neuen Prefix für eine 32-bit Version eingericht mit der Systemversion von Wine initialisiert und dann das Setup-Programm von Picasa 3.9 ausgeführt. Das ging völlig problemlos.

Als nächsten Schritt habe ich in PlayOnLinux Picasa ausgewählt, bin auf "Konfigurieren" gegangen und von dort zu "Wine konfigurieren". Im "Laufwerke" Tab habe ich das Laufwerk D: ausgewähl und ihm den Pfad `/windows/d` zugewiesen, wo ja meine NTFS Festplatte mit den Daten gemountet ist. Es ist wichtig, genau den gleichen Laufwerksbezeichner zu nehmen wie unter Windows, weil die Picasa Datenbank alle Albuminformationen mit absoluten Pfaden speichert. Diese Albuminformationen wollte ich ebenfalls migrieren.

Dazu habe ich erst mal Picasa unter Wine gestartet, ohne die Laufwerke nach Fotos durchsuchen zu lassen. Dann habe ich gesucht, wo Picasa die Albuminformationen ablegt. Das war:

* unter Linux: `~/.PlayOnLinux/wineprefix/Picasa/drive_c/users/<username>/Local\ Settings/Application\ Data/Google/`
* unter Windows: `c:\Users\<username>\AppData\Local\Google`

Dort gibt es jeweils die beiden Ordner `Picasa2` and `Picasa2Albums`. Den gesamten Inhalt der beiden Ordner habe ich dann einfach von Windows nach Linux kopiert, und dabei den alten Inhalt unter Linux überschrieben.

Beim nächsten Start von Picasa unter Linux waren alle meine Alben, Einstellungen und Fotos da, genau wie unter Windows!

Ein kleiner Nachteil: weil ich den Internet Explorer nicht installiert habe, gibt es bei jedem Start eine Message Box mit dem Hinweis, dass die Anmeldung bei Google fehlgeschlagen ist. Den muss man wegklicken. Aber das mache ich gerne und erinnert mich jedesmal daran, dass ich damit nicht nur Microsoft, sondern auch Google ein bisschen weniger meiner Daten überlasse.
