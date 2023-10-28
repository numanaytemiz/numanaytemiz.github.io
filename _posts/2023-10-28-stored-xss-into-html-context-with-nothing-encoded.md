## Web Security Academy Labs : Stored XSS into HTML context with nothing encoded

- This lab contains a stored cross-site scripting vulnerability in the comment functionality.
- To solve this lab, submit a comment that calls the alert function when the blog post is viewed.
- Application URL : https://0ae6000f03fc431980a917d300bd0032.web-security-academy.net/

#### Solution :

Leave a comment to the any post in the web application and analyze it

![Image](/img/comment.png)

Application stored commenst in the application and show it to the user.

![Image](/img/comments2.png)

when we type html comment on the application we will see we can succeffuly inject html to the application. Then we will try js code.

![Image](/img/stored5.png)

![Image](/img/xss-stored.png)
