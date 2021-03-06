# Microsoft Office 2010

Die schon in die Tage gekommene Microsoft Office Suite hat mich unter Windows nun schon länger begleitet. Hauptsächlich sind es Word Dokumente und einige Powerpoint Präsentationen. Daneben noch ein paar Excel Tabellen. Viele Freunde und Bekannte nutzen diese Tools auch, und so sind `.docx`, `.pptx` und `.xlsx` eben auch Formate für den Dokumentenaustausch. Natürlich kann auch LibreOffice alle diese Formate lesen und schreiben, aber nicht immer mit dem gewünschten Ergebnis. Deshalb wollte ich die Microsoft Office Suite wenn möglich auch unter Linux weiter verwenden.

Wie bei Picasa war auch hier PlayOnLinux das Hilfsmittel meiner Wahl. Hier gibt es fertige Skripte zum Setup der passenden Umgebung, auch für Office 2010.

Ich habe also PlayOnLinux gestartet, im Install-Menu 

To run Windows applications under Linux you need wine - but you're even better off with installing PlayOnLinux, which is an application which can manage multiple parallel versions of wine and comes with a set of scripts to install commonly used software. Many games, but also Microsoft Office 2010.

So I first installed PlayOnLinux using YaST from the official OpenSUSE repositories. I then opened PlayOnLinux, slected install, chose the Microsoft Office 2010 package and went further on. I inserted my DVD into the drive. When asked by PlayOnLinux do not try to tell the path to your DVD drive - this did not work. Instead chose to give the path to the setup.exe located in the root folder of the DVD. Then the typicall Office installer starts up and installs the suite flawless.

The harder part was to get the office suite activated. There are a lot of posts and questions about that on the Internet, but the following was the only thing which worked for me - and it is a very official way. Activation over Internet does not work, so I selected actvation by telephone. However the next dialog says that this is no longer supported for that product. However I found a [post](https://www.codeweavers.com/compatibility/crossover/forum/microsoft-office-2010?msg=204082) pointing to [this official Microsoft page](https://support.office.com/en-us/article/-telephone-activation-is-no-longer-supported-for-your-product-error-when-activating-office-9b016cd2-0811-4cb3-b896-5a6a13177713). Here you can select your country and you will get a phone number allowing for activation of your product! Dane, thanks for this tip!

With the default options there is still a problem with Word: The window can be maximized or minimized, but not resized. The solution is in the wine configuration:

* Start PlayOnLinux
* Select Microsoft Word
* Select `Configure` in the list on the left
* Click on `Configure Wine`
* Select the tab `Graphic`
* Deselect the option `Allow the window manager to control the windows`

and viola! the windows can be resized!
