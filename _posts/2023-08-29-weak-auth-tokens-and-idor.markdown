# Weak Token and IDOR

- Observe the response to login requests
- Analyze how authentication tokens are generated
- Check how this can be abused by an attacker.

  ![Image](/img/request1.png)

Take md5 hash of the securestore and compare it with token, we will see it is the same value.

![Image](/img/md5sum.png)

take md5 sum of the attacker user and send request with that token.

![Image](/img/attacker_md5sum.png)

![Image](/img/attacker_login.png)
