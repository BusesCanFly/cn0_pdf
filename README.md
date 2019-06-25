I got an email that google marked as obvious scam, and the PDF was flagged as having malware.
![alt text](https://github.com/BusesCanFly/cn0_pdf/blob/master/files/malwarepdf.png "Screenshot of the original email")
By downloading the email as an .eml file, and opening that in a different mail client, the malicious PDF can be dowloaded.

Running it through VirusTotal shows a low detection rate:
![alt text](https://github.com/BusesCanFly/cn0_pdf/blob/master/files/pdf_VT.png "Virustotal")
VT also shows that there is an embedded file, but more later.

`file ./cn0.pdf` shows `Creator: wkhtmltopdf 0.12.5` meaning the pdf was made with ![wkhtmltopdf](https://wkhtmltopdf.org/)

`strings ./cn0.pdf` shows `/URI (https://5evro161.blogspot.com)` but I was apparently too late, as that blogspot page is down. This was linked in the PDF, so maybe it was a phishing page. Would be cool if it was a blogspot c2 though.

```bash
ExifTool Version Number         : 11.38
File Name                       : cnO.pdf
Directory                       : .
File Size                       : 40 kB
File Modification Date/Time     : 2019:06:25 14:58:59-04:00
File Access Date/Time           : 2019:06:25 15:49:53-04:00
File Inode Change Date/Time     : 2019:06:25 15:47:59-04:00
File Permissions                : rw-r--r--
File Type                       : PDF
File Type Extension             : pdf
MIME Type                       : application/pdf
PDF Version                     : 1.4
Linearized                      : No
Title                           : 
Creator                         : wkhtmltopdf 0.12.5
Producer                        : Qt 4.8.7
Create Date                     : 2019:06:06 01:52:18+03:00
Page Count                      : 1
```

```bash
[buses@xps PDF]$ pdfdetach -list ./cnO.pdf 
0 embedded files
```
`pdftohtml` extracts three HTML files, cnO.html, cnO_ind.html, cnOs.html. These contain an image, ![cnO-1_1.png](https://github.com/BusesCanFly/cn0_pdf/blob/master/files/cnO-1_1.png "The embedded image")

Emails:
```
from:	ГосУслуги <dimi1986@t-online.de>
reply-to:	"fosl2adeha3252@sureul.dev" <dimi1986@t-online.de>
to:	"derpefera@dafaub.doc" <semashkate@gmail.com>
date:	Jun 5, 2019, 6:52 PM
```
![haveibeenpwned](https://haveibeenpwned.com/) shows "Dimi1986[@]t-online[.]de" as being in the "2,844 Separate Data Breaches," "Anti Public Combo List," "Collection #1," "Kayo.moe Credential Stuffing List," "MyFitnessPal," and " "Trillian" breaches.
    * `./query.sh Dimi1986@t-online.de` gives `Dimi1986@t-online.de:diima1986`

