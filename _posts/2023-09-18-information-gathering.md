#### Information Gathering

- Gathering Information on Your Targets
- Infrastructure
- Fingerprinting Frameworks and Applications
- Fingerprinting Custom Applicatins
- Enumerating Resources
- Information Disclosure Through Misconfiguration
- Google Hacking
- Shodan

#### Gathering Information on Your Targets

- Information gathering is the very first and most critical step of every penetration test. It does not matter if you have to assess the security of an entire network or a single web application, we need to know our target in as much detail as possible.
- At information gathering stage , there is no unnecessary information; everything you collect should be noted for future use. The wealth of information you collect will become useful in both understanding application logic and during the attack phase.
- What sorts of information are we going after?

  - Infrastructure (Web Server , CMS, Database...)
  - DNS
  - Application Logic
  - IPs, Domains and subdomains
  - Virtual hosts

#### Finding Owner, IP Addresses and E-mail

- For simplicity, we will pretend to be unaware of what systems and individuals are behind a given website.
- The first step to take when assesing a website is to gather information about the organization.

#### Whois

`whois google.com`

![Image](/img/whois.png)

- There are also web based whois tools on internet, like whois.domaintools.com
- with whois we get administrative contact information, technical contact information, Ip address range, dns server list etc...

#### Nslookup

- Nslookup is very handy tool that lets you translate hostnames to IP address and vice versa.

```
nslookup
> google.com
```

![Image](/img/nslookup.png)

- Reverese nslookup (PTR)

`nslookup -type=PTR 8.8.8.8`

![Image](/img/ptr.png)

- all records (name servers, CNAME's, A recods, MX records...)

`nslookup -type=ANY google.com`

![Image](/img/allrecors.png)

#### Finding Traget ISP's

- We want to know which ISP's , hosting and IP addresses our target organization uses.
- Using nslookup we get the IP addresses associated to each subdomain. We will perform a whois request for each of these IP addresses ton uncover the ISP's that these IP addresses belong to.
  - nslookup
  - whois
  - https://arin.net

`nslookup statcounter.com`  
`nslookup www.statcounter.com`
`whois 104.20.219.77`

![Image](/img/nslookups.png)
![Image](/img/whoiss.png)
![Image](/img/arinnet.png)
