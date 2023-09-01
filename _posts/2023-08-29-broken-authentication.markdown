- Authentication mechanism is the key to identify the users.
- Incorrectly implemented authentication mechanisms in REST APIs can lead to various problems, which include :
  - Complete compromise of API
  - Compromising system's ability to identify user

## Bypass Authentication With Sql Injection

Send login request with which not exists in the application.

![Image](/img/usernotexists.png)

Send sql injection payload to the username parameter : `' or '1'='1'-- ` (url encode)

![Image](/img/sqlinjectionpayload.png)

## Vulnerable Code

```
//LOGIN and VIEW PROFILE CODE

if( $_SERVER['REQUEST_METHOD'] == "GET"){

    if(isset($_GET['token'])){

        $token = $_GET['token'];

        $selectquer = $mysqli->query("SELECT * FROM user WHERE token='".$token."'");
         if($selectquer->num_rows > 0) {

             while($row = $selectquer->fetch_assoc()) {


             $username = $row['username'];
             $email = $row['email'];
             $token = $row['token'];
             $password = $row['password'];

             $response['code'] = 1;
             $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
             $response['data'] =  array(
                 username => $username,
                 emailid => $email,
                 token => $token,
                 password => $password);
             }
        }
        else{

    $response['code'] = 4;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data'] = 'No Data found with this token';

        }


    }
    else{

    $username = $_GET['username'];
    $password = $_GET['password'];

    if(!empty($username)&&!empty($password))
    {
    $selectquer = $mysqli->query("SELECT * FROM user WHERE username='".$username." 'and password='".$password." ' ");

        if($selectquer->num_rows > 0) {

        while($row = $selectquer->fetch_assoc()) {

             $name = $row['username'];
             $email = $row['email'];
             $token = $row['token'];

             $response['code'] = 1;
             $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
             $response['data'] =  array(
                 username => $username,
                 emailid => $email,
                 token => $token);
        }


    }
     else{

    $response['code'] = 4;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data'] = 'Invalid Username or Password';
     }
    }
    else
    {
    $response['code'] = 0;
    $response['status'] = $api_response_code[ $response['code'] ]['HTTP Response'];
    $response['data']['user'] = 'unknown';
    $response['data']['message'] = 'incomplete';
    }
    }
}

```
