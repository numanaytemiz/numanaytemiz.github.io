#### **EWPT Introduction**

- **We need some informtion before begin web application security testing**
  - **HTTP/HTTPS Protocol Basics**
  - **Encoding**
  - **Same Origin**
  - **Cookies**
  - **Session**
  - **Web Application Proxies**

#### **HTTP Protocol Basics**

- **Hypertext Transfer Protocl (HTTP) is the basic protocol used for web browsing and for most other communication on the web.**
- **HTTP is client-server protocol used to transfer web pages and web application data. The client is ususalyy a web browser that starts a connection to a server web such as MS IIS or Apache HTTP Server.**
- **During an HTTP communication , the client and the server exchage messages. The client send `requests` to the server and get back `responses`. The format of an HTTP message is:**

```
HEADERS\r\n
\r\n

MESSAGE BODY\r\n
```

`\r\n: same of hitting enter`

#### **HTTP Request**

![Image](/img/http_request.png)

- **Examine an HTTP request in detail. The following is the content of the request that we send when we open web browser and navigate to numanaytemiz.github.io**

```
GET / HTTP/1.1
Host: numanaytemiz.github.io
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

- **we see here `http request headers`**
- **REQUEST METHOD**
  - **`GET` is our requet type (also known as an HTTP `Verb` ). GET is the default request type when we type a URL into the location bar of our web browser and hit Enter.**
  - **Other `Verbs` are `POST, PUT,DELETE, OPTIONS, TRACE...`**
- **PATH**
  - **`/` path is the file we are requesting. The home page of a website is always `/`. Other pages can be requested, such as : `/downloads/index.php`. Our request always refers to the root folder to specify the requested file (hence the leading `/`)**
- **PROTOCOL**
  - **`HTTP/1.1` is the HTTP protocol version that our browser wants to talk with. This basically informs the web server about which version of HTTP we would like to use in any further communication.**
- **HOST HEADER**
  - **`Host:` is the beginnig of HTTP request headers. HTTP headers have the following structure: `Header-name:Header-Value`**
  - **The `Host` header allows a web server to host multiple websites at a singel IP address. Our browser is specifying in the Host header which website you are interested in.**
- **HOST VALUE**
  - **`numanaytemiz.github.io` is the Host Value. After each request header, we will find its corresponding value. In this case we want to reach the Host numanaytemiz.github.io**
  - **`Host Value + Path = URL` define we are requesting**
- **USER-AGENT**
  - **The `User-Agent` reveals your browser version, operating system and language to the remote web server. All browsers have their own user-agent identification string.**
- **ACCEPT**
  - **The Accept header is used by our browser to specify which document type is expected to be returned as a result of this request.**
- **ACCEPT-ENCODING**
  - **The `Accept-Encoding` is similar to Accept, but it is restricts the content codings that are acceptable in the response. Content codings are primary used to allow a document to be compressed or transformed without losing the identity of its media type and without loss of information.**
- **CONNECTION**
  - **With HTTP 1.1 we can keep our connection to the remote web server open for an unspecified amount of time using the value `keep-alive` This indicates that all requests to the web server will continue to be sent through this connection without initiating a new connection every time (as in HTTP 1.0)**

---

#### **HTTP Response**

![Image](/img/http_response.png)

```
HTTP/2 200 OK
Date: Sun, 10 Sep 2023 10:12:01 GMT
Cache-Control: max-age=600
Content-Type: text/html; charset=utf-8
Content-Encoding: gzip
Server: GitHub.com
Content-Length: 7145

<PAGE CONTENT>
```

- **let us examine web server response**
- **In response to the HTTP request, the web server will respond with the requested resource, preceded by a bunch of new heders.**
- **These new headers from the server will be used by your web browser to interpret the content contained in the Response content.**

- **STATUS LINE**
  - **The first line of the response message is the Status-Line, consisting of the protocol version (HTTP 1.1) followed by a numeric status code (200) and it is relative textual meaning (OK).**
  - **The more common status code are:**
    - **200 OK, the resource is found.**
    - **301 Moved Permanently, the requested resourse has been assigned a new permanent URI**
    - **302 Found, the resource is temporarily under another URI**
    - **403 Forbidden, the client does not have enough privileges and the server refuse to fulfill request.**
    - **404 Not Found, the server cannot find a resource matching the request**
    - **500 Internal Server Error, the server does not support the functionality required to fullfill the request.**
- **DATE**
  - **Date represents the date and time at which the message was originated.**
- **Cache Header**
  - **The Cache Headers allow the Browser and the Server to agree about caching rules. Cached contents save bandwith because they prevent our browser from re-requesting contents that have not changed when the same resource is to be used.**
- **Content-Type**
  - **Content-Type lets the client know how to interpret the body of the message.**
- **Content-Encoding**
  - **Content-Encoding extends Content-Type. In this case the message body is compressed with gzip.**
- **SERVER HEADER**
  - **The Server header displays the web server banner. Apache and IIS are common web servers. Github uses a custom webserver banner: GitHub.com**
- **Content Length**
  - **Content-Length indicates the length, in bytes, of the message body.**
- **Content**

  - **This is the actual content of the requested resource. The content can be an HTML page, a document, or even a binary file. The type of the content is , of course, contained in the Content-Type header.**

  ***

  - **The best way to understand something is to play around with it a bit. Firefox (as well as other web browser) already have some features that allow us to inspect HTTP Headers on the fly.**
  - **Once Firefox Starts, open the options menu and select More Tools > Web Developer Tools > Network to inspect http requests and responses**

![Image](/img/reqres.png)

---

#### **HTTPS**

- **HTTP content , as in every clear-text protocol, can be easily intercepted or mangled by an attacker on the way to its destination. Moreover, HTTP does not provide strong authentication between two communicating parties.**
- **we will see how to protect HTTP by means of an encrytion layer.**
- **HTTP Sercure (HTTPS) or HTTP over SSL/TLS is a method to run HTTP, which is a clear-text protocol, over SSL/TLS, a cryptographic protocol**
- **This layering technique provides confidentiality, integrity protection and authentication to the HTTP protocol.**

![Image](/img/attacker.png)

- **When using HTTPS**

  - **An attacker on the path cannot sniff the application layer communication**
  - **An attacker on the path cannot alter the application layer data**
  - **The client can tell the real identity of the server and vice-versa**

- **HTTPS does not PROTECT AGAINST WEB APPLICATION FLAWS!. The extra encriytion layer just protects data exchange between the client and the server. It does not protect from an attack against application itself. Attacks such as XSS and SQL Injectons will still work.**

---

#### **ENCODING**

- **Information encoding is a critical component of information technology.Its main function is to represent the low-level mapping of the information being handled.**
- **The encoding process, often invisible to end users, occurs each time an application needs to be elaborate on any data. Web applications are not excluded from this. Like many other applications, they continuously process thousands of pieces of informaion even for simple requests.**
- **Understanding encoding schemes used by a web application can give you a big advantage during the detection and exploitation of a vulnerability.**

- **CHARSET**

  - **Internet users, via their browsers, request billions of pages everyday. All of the content of these pages are displayed according to a charset.But What is charset?**
  - **Charset contains a set of characters, they represent the set of all symbols that the end user can display in their browser window. In technically, a charset consists of pairs of symbols and code points.**
  - **The sysmbol is what the user reads, as he sees it on the screen. The code point is a numeric index, used to distinguish, the symbol within a charset. A sysbol can be shown only if it exists in the charset.**
  - **Example of charsets are: ASCII, Unicode, Latin-1 and so on**

  - **ASCII CHARSET**

    - **The ASCII (American Standart Code for Information Interchange) charset contains a small set of symbols. Originally it was 128 only, but now it is usually defined with its extended version for a total of 255. It is old and it was designed to support only US symbols.For example ASCII cannot be used to display Chinese symbols amnong many others.**
    - **Here is some exaple**

    | CODE | HEX | SYMBOL |
    | ---- | --- | ------ |
    | 65   | 41  | A      |
    | 66   | 42  | B      |
    | 67   | 43  | C      |
    | 68   | 44  | D      |
    | 69   | 45  | E      |
    | 70   | 46  | F      |
    | 71   | 47  | G      |
    | 72   | 48  | H      |

  - **UNICODE**
    - **UNICODE (Universal Character Set) is the character encoding standart created to enable people around world to use computers in any language. It supports all the world's writing systems.**
