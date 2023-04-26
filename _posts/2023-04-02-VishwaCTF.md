---
layout: post
title:  "VishwaCTF"
---


Hi, Hello!

I played <a>VishwaCTF 2023</a> which was organised by <a href="https://ctftime.org/team/144677" style="color:cyan;">CyberCellVIIT</a> along with team <a>Invaders0x1</a>.

Here is one of the challenge I have solved from `#WEB` category

### Payload

Here is the challenge deployment : 

![Payload](/assets/img/post_img/payload.png)

We were given a button on the webserver which when pressed gave me the info about the system details.

So again dirsearch found robots.txt on the website which when accessed gave me the source code having if else condition mentioning cmd and btn.

So as we press the system details button we see that in the url /?btn= appears so simply i changed btn to cmd and to check for if the commands work i tried `?cmd=ls`

![Payload](/assets/img/post_img/payload1.png)


It gave me the files inside the directory index.html, index.php and one more file forgot the name. So i simply used command `?cmd=cat+index.php`

To notice I wasnt getting the flag anywhere instead the site was getting rendered so I decided to use an alt for cat command and I did the changes `?cmd=tac index.php`

and there we go, I found the whole source code with the flag.

![Payload](/assets/img/post_img/payload2.png)



Here is the hidden deatails of the deploymemnt which includes `flag` !

```
?> } } system("uname -a"); echo "System Details: "; if(isset($_GET['btn'])){ else { } system($_GET['cmd']); if(isset($_GET['cmd'])){ putenv("FLAG=VishwaCTF{y0u_f-o-u-n-d_M3}");
```
<br>

> `FLAG : VishwaCTF{y0u_f-o-u-n-d_M3}`