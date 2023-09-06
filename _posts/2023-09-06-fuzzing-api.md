## Fuzzing APIs

- **Fuzzing is simply sending diffrent data in a number of requets and seeing what comes back**
- **It can be very useful to discover content**
- There are may diffrent fuzzing tools ;
  - Burp suite
  - wfuzz
  - ffuf
  - gobuster
  - dirbuster
  - list goes on...

https://tryhackme.com/room/bookstoreoc -----> fuzzing endponit with this app from thm which is free room.

- http://10.10.70.164:5000/api --> api documentation

![Image](/img/api-docum.png)

## Fuzz With Burp

- http://10.10.70.164:5000/api/v2/resources/books?published=1993 send this request to burp repeater and burp intruder

![Image](/img/fuzzy.png)

![Image](/img/resp.png)

Firstly fuzz v2 field with manuellay, may be there is available v1 field ?

![Image](/img/fuzzzv1.png)

![Image](/img/resuts.png)

- fuzz books section with the burp intruder , wordlist is common.txt /usr/share/wordlists/dirb/common.txt

![Image](/img/fuzzbooksv1.png)

- fuzz published field

when we take care status code and response length , **show** value is given 500 error, this say us value is real but parameter is not compatible

![Image](/img/showfuzz.png)

lastly we can fuzz paramter

![Image](/img/showfuzz.png)

![Image](/img/fuzzparamres.png)

- we find /api/v1/resources/books?show=%2ebash_history lfi vulnerable end point with fuzzing

![Image](/img/fuzzlfi.png)

## Fuzz with **wfuzz**

```
wfuzz -c -z file,/usr/share/wordlists/dirb/common.txt "http://10.10.118.77/api/v1/resources/books?show=FUZZ"
```

to filter response code we can use --sc=200

```
wfuzz -c -z file,/usr/share/wordlists/dirb/common.txt --sc=200 "http://10.10.118.77/api/v1/resources/books?show=FUZZ"
```

![Image](/img/wfuzz.png)
