- If a REST api does not impose any restrictions on number of requested that can be made by the client/user, it can lead to attacks like :
  - Denial of service
  - brute force

Lets brute force attack to the username and password parameter with burp intruder with cluster bomb attack type

![Image](/img/intruder_user_pass.png)

![Image](/img/results_intruder)

To prevent this type of attack developer need to implement rate limiting to the application for instance if there are more than three fail attemtp given time on valid account , account can be locked out or implement captcha protection.

#### Other Tips

if you see an API invoked by your client using GET method, try other methods on the same API endpoint.

- GET - http://sample.com/api/profilepic/user123
- DELETE - http://sample.com/api/profilepic/user123
