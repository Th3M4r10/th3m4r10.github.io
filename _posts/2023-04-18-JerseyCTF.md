---
layout: post
title:  "JerseyCTF III"
---

Hello mates!

I played <a href="https://ctf.jerseyctf.com/" target="_blank">JerseyCTF III</a> which was hosted by the <a style="color:cyan;">NJIT ACM</a> along with my team <a>Invaders0x1</a>.Our team achieved a commendable 125th place in the CTF competition, and we are determined to strive for even better results in future competitions.


Here are some of the challenges I have solved :


### back-to-the-office

Challenge details :

	There's a flag somewhere in this Microsoft Word document.

Hint :

	Newer Microsoft Office files are in OOXML format. Learn more about this file format to find the flag.

<p>Here is the attached file <a href="/assets/files/jerseyCTF/back-to-the-office.docx" download="">back-to-the-office.docx</a>.</p>

Download the given file and extract with the command `unzip back-to-the-office.docx`

And to check directories use `tree *`

```
m4r10@ARLinux:~/Desktop/CyberSec/CTF/jerseyCTF/misc$ tree *
back-to-the-office.docx  [error opening dir]
[Content_Types].xml  [error opening dir]
docProps
├── app.xml
└── core.xml
_rels
word
├── document.xml
├── fontTable.xml
├── _rels
│   └── document.xml.rels
├── settings.xml
├── styles.xml
├── theme
│   └── theme1.xml
└── webSettings.xml
```

After that run the command `cat word/settings.xml`

Yayy, you got the flag at the end of the xml code.

> _`Flag : jctf{601n6_1n70_7h3_0ff1c3}`_

### put-the-cookie-down

Challenge details :

```
The Terminator has sent you a frantic message from 1996, maybe it's something important! Wait... do I smell cookies?
Flag format: jctf{string}
```
Here are the steps I followed:

-Open your browser DevTools<br>
-As the hint suggests, we will be exploring DevTools a bit deeper<br>
-Navigate to the Application tab<br>
-On the left side of the Application tab, go to `Storage > Cookies`<br>
-Click on the website's URL to see the cookie data.

Or otherwise you can simply open cookies to check the flag,

![Payload](/assets/img/post_img/put-the-cookie-down.png)

> `Flag: jctf{I_WILL_BE_BACK_FOR_MORE_C00KI3S!}`


### back-to-socials

Challenge details :

	The NICC club that co-hosts this event jumped into the NCAE Cyber Games this past February and placed well for the first time competing as a club! The club wanted to let everyone at the school know of their successes and were very social! Can you dig deep and find out where this flag could be planted?

Hint :

	There is usually some sort of website that people can share their achievements to a professional crowd...

From this hint,

I have decided to search for the *`NICC Competes in their first NCAE Cyber Games`* post on LinkedIn.<br>
And here is the result with post link,

	https://www.linkedin.com/pulse/nicc-competes-first-ncae-cyber-games-njiticc/

![Payload](/assets/img/post_img/back-to-socials.png)

> _`Flag : jctf{c0mp3titi0n_spark5_excellency}`_






