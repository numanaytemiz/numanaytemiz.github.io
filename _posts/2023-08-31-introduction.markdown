---
layout: post
title: "Web APIs Penetration Test Introduction"
date: 2023-08-31 15:36:27
categories: web api pen test
---

#### What is API

- **API** : Application Programming Interface, api allow us to connects applications together. It set the rules which two entities can share the information between one application and another.

![Image](/img/apiintro.png)

![Image](/img/apikitchen.png)

#### Interacting With API

API address : https://catfact.ninja/

- we have documentetaion here and there are two main section here , Breeds and Facts

![Image](/img/catfact.png)

- /fact url generates random fact we can reach it with https://catfact.ninja/fact

firts request

![Image](/img/frstreq.png)

second request

![Image](/img/secondreq.png)

- /fact url takes max_length parameter with get request ----> https://catfact.ninja/fact?max_length=40

![Image](/img/maxparameter.png)

- we can interact with api with using **burp suite** , and with burp repeater we can play with request and response easily....

Here is classic request

![Image](/img/normal-request.png)

for example : What if max_length is taken -1 , this is good point to start to test an api

![Image](/img/minisone.png)

- we can interact with api with using **postman**

![Image](/img/postman.png)

- we can interact with api with using **curl**

```
curl -X 'GET' \
  'https://catfact.ninja/fact?max_length=30' \
  -H 'accept: application/json' \
  -H 'X-CSRF-TOKEN: v9q8arv7Vvva8mkcksdKbKfv2ETOHFlrmtahWJhE'
```

![Image](/img/curlinteract.png)

#### Types of APIs

- **Public** , **Partner** and **Private** api

- **REST APIs**

  - Client-server architecture
  - statelessness
  - cacheability
  - layered system
  - use of http methods (GET, POST , etc...)
  - use of URIs to identify resources

- **SOAP API**
- **RPC API**

- [here is nice documentation](https://konghq.com/learning-center/api-management/different-api-types-and-use-cases)

- ## **Endpoints**
  - [what is endpoints](https://www.techtarget.com/searchapparchitecture/definition/API-endpoint)

#### Common APIs Attacks

- SQL injection
- Command injection
- IDOR, Broken Access Control
- XXE - if XML is processed by the server
- Lack of output encoding
- Insecure direct object references

and the list goes on...
