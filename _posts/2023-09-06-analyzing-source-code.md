#### Analyzing Source Code To Enumerate APIs

- **SIMPLE APPROACH IS THE BEST**
- **We can analyze application source code especially js file to enumerate and expand attack surface.**
- [Great site to view java script codes nicer format](https://beautifier.io/)
- Firstly up an running test site

```
cd crAPI/deploy/docker
sudo docker-compose up
```

- Create user on the http://localhost:8888 , then open web developer (F12) -> debugger -> static -> sagas -> config.js , we will see some tld , this is great to expand attack surface

![Image](/img/sourcejs.png)

- then contine examine source code , debugger -> static -> sagas -> main.ccf90738.chunk.js

![Image](/img/sourcebeau.png)

- copy this code then paste to https://beautifier.io/

![Image](/img/beautyjs.png)

**we find new attack surface and enumerate app without fuzzing via analyzing applicatiaon js codes**
