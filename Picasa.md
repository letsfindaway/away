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

# Importieren von Bildern

Auch das Importieren von Bildern ist mühsamer als unter Windows. Wenn ich die Kamera per USB anschließe, dann habe ich sie bisher nicht in Picasa finden können. Ich muss also die SD Karte in den Kartenleser stecken. Und da organisiert meine Kamera die Bilder in mehrere Ordner. Ich muss jeden Ordner einzeln importieren. Picasa unter Wine kann die Kamera nicht direkt als "Kamera" erkennen, und auch die SD Karte nicht direkt als eine Karte, die aus einer Kamera stammt, so wie das unter Windows war.

Das sind ein paar Klicks mehr als unter Windows, aber damit kann ich leben.

# Bilder als E-Mail senden

Diese Funktion tut erst mal nicht so wie gewünscht. zwar wird eine neue E-Mail in Thunderbird geöffnet, aber die Anlagen fehlen. Und gerade darum geht es ja. Tiefere Untersuchungen haben ergeben, dass dies generell ein Problem der MAPI Implementierung in wine ist: Das Senden von E-Mail erfolgt über einen ` mailto:`-Link. Über diesen Weg wird zwar immer der Standard-Mailer angesprochen. Attachments gehen damit aber nicht.

Ich habe im Forum dann noch jemand gefunden, der dieses Problem hatte: https://askubuntu.com/questions/989830/how-to-mailing-photos-from-picasa-3-9-in-thunderbird. Dort habe ich auch genau beschrieben, wie ich es gelöst habe! Das MAPI baut nun einen compose-String zusammen und übergibt diesen direkt an Thunderbird, ohne Umweg über `mailto:`. Das Repository mit meinem Patch ist hier zu finden: https://build.opensuse.org/package/show/home:letsfindaway:branches:openSUSE:Leap:15.0/wine. Die neue Methode zum Aufruf von Thunderbird hat darüber hinaus den Vorteil, dass die Umlaute richtig im Betreff ankommen!

Ohne den openSUSE Build Service hätte ich das nicht so schnell geschafft. Vielen Dank!

# EXIF Daten bearbeiten

Immer wieder passiert es, dass die Uhrzeit der Kamera nicht richtig gestellt ist. Besonders beim Mischen von Bildern von Kamera, Smartphone und anderen Quellen kommt dann die zeitliche Ordnung durcheinander.

Unter Windows hatte ich dann den EXIF Date Changer verwendet, der genau das kann. Nicht viel mehr, aber dafür reicht es. Unter Linux ist das `exiftool` fester Bestandteil der Distribution. Es kann noch viel mehr, ist aner ein typisches Linux Command Line Tool ohne grafische Oberfläche.

Unter openSUSE ist aber `Photini` in der Distribution enthalten, das eine grafische Oberfläche für die wichtigsten Funktionen von `exiftool` bietet. Damit das Programm läuft, muss aber noch das Paket `python3-requests` installiert werden, das leider nicht in der Liste der Abhängigkeiten von `Photini` steht. Dann bietet dieses Tool aber eine brauchbare, englischsprachige Oberfläche für viele Aufgaben rund um EXIF.
