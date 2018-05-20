# Microsoft Access 2010 and TZ-EasyBuch

Microsoft Access 2010 does not run under wine. Fullstop.

Most article I found had no success, and if somebody got it working, then only small parts of it.

I have a Microsoft Access database as part of a bookkeeping solution together with TZ-EasyBuch, and in some way I have to transfer this solution to Linux. I keep customers and invoices in the database and generate bookings using the COM interface of TZ-EasyBuch. This way will no longer be possible. So what to do?

Currently I run an investigation of the following way:

* Transfer the database to LibreOffice Base
* Install TZ-EasyBuch inside wine
* Install a Java JRE in the same wine prefix
* Write a Java Application running inside wine which interacts with the database on one side and Tz-EasyBuch on the other side using com4j.

## Transfer the database to LibreOffice Base

TODO

## Install TZ-EasyBuch inside wine

TODO

## Install a Java JRE in the same wine prefix

TODO

## Write a Java Application for interaction of the database and TZ-EasyBuch

TODO
