## Web Security Academy Labs : Reflected XSS into HTML context with nothing encoded

- This lab contains a simple reflected cross-site scripting vulnerability in the **search** functionality.
- To solve the lab, **perform a cross-site scripting attack that calls the alert function.**
- Applicaiton URL : https://0abb0093034951bb8044c7d400ae00e8.web-security-academy.net/

#### Solution :

Here is application home page :

![Image](/img/apiintro.png)

Seach something in the application and analyse the result

![Image](/img/reflects1.png)

Application reflects searching parameter on the web page. Now try to search with html tag.

Search \<h1>test\</h1> and inspect page source

![Image](/img/html.png)

Application accepts html code. Now try to inject js code to the application. \<script>alert("xss")\</script>

![Image](/img/popup.png)
