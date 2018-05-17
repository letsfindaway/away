# Picasa

The photo manager Picasa is one of the programs I would really miss. It is simple and easy to use, but still allows the most important image manipulations. All effects can be undone and the original photo is never modified.

Fortunately, PlayOnLinux seems to support Picasa out of the box. However when I tried to install it this way, I always failed at a point where PoL wanted to download a 300MByte file needed for Internet Explorer. After 192MBytes of download it stopped reproducably. But why is Internet Explorer installed when I wanted to install Picasa?

Searching on the Internet reveals that Picasa uses parts of IE to manage the sign in at Google. However do I really want this? Google Web Album is no longer available and I see absolutely no advantage for signing in. So my second try was to install Picasa without Internet Explorer.

I first started PlayOnLinux and went to Tools -> Manage wine versions. Here I installed the newest available version of wine, which was 3.8. I then clicked on Install and selected the link at the bottom: Install a program that is not listed. In the following dialog I selected to use a new virtual drive and called it "Picasa". I selected the x86 version for a 32-bit wine and finally the Picasa setup program. Installation runs easily and without problem.

I then selected Picasa and clicked on "Configure", went to the tab "wine" and clicked "Configure wine". There I went to the "Drives" tab and added a drive D pointing to `/windows/d` where I have mounted my NTFS formatted hard disk with all the photos. It is important to use the same drive letters as on Windows, because the Picasa database storing all the album information contains absolute paths including drive letters.

After starting Picasa a very first time without scanning my drives I found out that the Picasa database is located under `~/.PlayOnLinux/wineprefix/Picasa/drive_c/users/<username>/Local\ Settings/Application\ Data/Google/` in the two folders `Picasa2` and `Picasa2Albums`. I located these folders also on my Windows installation. Here I could find it at `c:\Users\<username>\AppData\Local\Google`. I then just copied these two folders, ovewriting what was already there at the destination.

When I started Picasa the next time, all my settings, albums, photos, etc have been available exactly as under Windows!

One mior drawback: because I did not install Internet Explorer, a message box is popping up each time I start Picasa telling me that it is unable to sign in at Google. It needs that extra click to get rid of this box, but all the rest works for me.
