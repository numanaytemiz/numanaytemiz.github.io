#### EWPT Introduction

- **We need some informtion before begin web application security testing**
  - **HTTP/HTTPS Protocol Basics**
  - **Encoding**
  - **Same Origin**
  - **Cookies**
  - **Session**
  - **Web Application Proxies**

#### HTTP Protocol Basics

- **Hypertext Transfer Protocl (HTTP) is the basic protocol used for web browsing and for most other communication on the web.**
- **HTTP is client-server protocol used to transfer web pages and web application data. The client is ususalyy a web browser that starts a connection to a server web such as MS IIS or Apache HTTP Server.**
- **During an HTTP communication , the client and the server exchage messages. The client send `requests` to the server and get back `responses`. The format of an HTTP message is:**

```
HEADERS\r\n
\r\n

MESSAGE BODY\r\n
```

`\r\n: same of hitting enter`

#### HTTP Request

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
