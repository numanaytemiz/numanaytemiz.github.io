## Three Types Of XSS

- **Reflected XSS**
- **Stored (Persistent) XSS**
- **DOM XSS**

## Reflected XSS

**Reflected XSS ocuurs when untrusted user data is sent to web application and web application is immediately back as the untrusted content. Then the browser receives the code from web server response and renders it.**\
**reflected XSS deals wit the server-side code**
**Simple vulnerable reflected xss code**

```
<?php $name = @$_GET['name']; ?>
Welcome <?=$name?>
```

## Persistent XSS

**Persistent XSS flwas are similar to Reflected XSS; however , rather tahn the malicious input being directly reflected into the response, it stored within the web application.**\
**Once this occurs, it is then echoed somewhere else withih the web application and might be available to all visitors**
**This is a server side vulnerabilty and more dangerous then reflected xss, because attacker doesnt need to interact with user, any visitor of the web site affects immediatetly.**
**Simple Stored XSS Vulnerable Code**

```
<?php
$file = 'newcomers.log';
if(@$_GET['name']){
    $current = file_get_contents($file);
    $current .= $_GET['name']."\n";
    //store the new comer
    file_put_contents($file, $current);
}
// if admin show newcomers
if(@$_GET['admin']==1)
    echo file_get_contents($file);
?>
```

#### **Test Vulnerable Code**

**Reguest ---> http://site2.com/storedxss.php?name=Bob**

![Image](/img/stored1.png)

**Reguest ---> http://site2.com/storedxss.php?admin=1**

![Image](/img/stored2.png)

**Send Malicious javscript Payload : \<script>alert("xss")</script> ---> http://site2.com/storedxss.php?Name=%3Cscript%3Ealert(%22xss%22)%3C/script%3E**

![Image](/img/stored3.png)

![Image](/img/stored4.png)

## DOM Based XSS

**DOM based xss exists only within client-side. This vulnerability lives within DOM environments, thus within a page's client-side script itself and does not reach server-side code.**
**Simple Stored XSS Vulnerable Code**

```
<h1 id="welcome">Welcome to our website</h1>
<script>
     var w = "Welcome";
     var name = document.location.hash.substr(document.location.hash.search(/#w!/i) + 3);
     document.getElementById('welcome').innerHTML = w + name;
</script>

```
