# Firefox

Firefox comes pre-installed with OpenSUSE, so this works out of the box. To transfer my collection of boomarks, I used the bookmark manager to export them to a json file and imported them again on Linux.

# KeePass

On Windows I kept all my passwords in KeePass. KeePass also runs with Linux using mono. On [https://keepass.info/help/v2/setup.html#mono](https://keepass.info/help/v2/setup.html#mono) you can find instructions how to install it. Luckily Suse has already created a package for that! So I started the software installer from YaST. Searching for keepass you can easily find the package. The necessary dependencies including mono are automatically installed, too.

After starting KeePass I had to find my key file, which resides on the Windows NTFS drive. Klicking "My Computer" takes you to a huge list of entries like `HDD (none, sdb1)`. I could only guess which drive it is, but then I have the full directory tree available, found my key file and could open it using the normal credentials.

# Kee

But now I want to use these user names and passwords in Firefox using the Kee plugin. The plugin could easily be found and installed using the plugins page. Further instructions are then given. As on Windows, you have to copy the `KeePassRPC.plgx` file to the `plugins` directory of KeePass.

KeePass has a small program to start it under `/usr/bin`. The executable itself and other supporting files are however under `/usr/lib/keepass`. I created a subdirectory `plugins` there and copied the `KeePassRPC.plgx` file to this directory. You have to do that using `sudo`, as the target directory needs superuser rights. After restart of KeePass I had to copy-paste a key to allow Kee access to the KeePass database and then, voila!, it just worked as it was on Windows.
