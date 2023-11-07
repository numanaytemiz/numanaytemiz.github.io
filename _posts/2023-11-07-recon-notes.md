## Reconnaissance and Information Gathering Notes

**Tool is nothing, understanding methodolgy is everyting!!!**

## Initial Informating Gathering

```
- https://builtwith.com
- **wappalyzer browser add ons**
- curl -I https://azena.com
- curl -I -L https://azena.com  // -L means follow redirect
- https://securityheaders.com
- nmap -p 80,443 -A azena.com
```

## Directory Enumeration And Brute Forcing

```
ffuf --help
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://10.10.10.10/FUZZ // non recursive by default
dirb http://10.10.10.10   // use own wordlists, scan recusively
dirbuster ---> GUI
```

## Subdomain Enumeration

```
google :
   site:azena.com -www
   site:azena.com -www -store
   site:azena.com filetype:pdf
   site:azena.com filetype:pdf password

https://crt.sh ----> %.azena.com
```

```
subfinder -d azena.com
```

```
assetfinder azena.com | grep azena.com | sort -u > azenasubdomain.txt
```

```
amass enum -d azena.com > azenasubdomain2.txt
```

```
is subdomain alive ? ---> cat azenasubdomain.txt | grep azena.com | sort -u | httprobe -prefer-https | grep https > azenaalive.txt
```

```
mkdir azenapics
gowitness file -f azenaalive.txt -P azenapics --no-http //not not use https:// in the domain file just write hostname
```
