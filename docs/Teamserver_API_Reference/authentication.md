# /auth

<!-- Endpoint 1 -->
## Server Status

Check if server is up

### Endpoint

```
POST /auth/
```

### Description

Bamboo Client will always request for this endpoint before requesting for credentials. A simple endpoint that allows Bamboo Client to determine if the Bamboo Teamserver hosted in the address input is online.


### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "online"}|Server is online|

### Response example

```
{
    "status": "online"
}
```

<!-- Endpoint 2 -->
<br>

## User Login

Authenticates user credentials for access

### Endpoint

```
POST /auth/login
```

### Description

This endpoint validates the credential sent by the user from Bamboo Client. Using the `model login_auth`, Bamboo Teamserver will determine if the credentials are valid. If it is valid, Bamboo Teamserver will generate a JSON Web Token (JWT) for the Bamboo Client user and respond back to the user.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username input by user|
|password|String|Password input by user|

### Request example

```
{
    "username": "bambooUser",
    "password": "adnap"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "message": "Login successful", "jwt_token": jwt_token}|Successfully Login|
|`400`|{"status": "error", "message": "User not found"}|Invalid Username|
|`401`|{"status": "error", "message": "Incorrect password"}|Incorrect Password|
|`404`|{"status": "error", "message": "Something went wrong!"}|Invalid Body|

### Response example

```
{
    "status": "success",
    "message": "Login successful",
    "jwt_token": jwt_token
}
```

<!-- Endpoint 3 -->
<br>

## User Logout

Notifies Bamboo Teamserver that user have log out

### Endpoint

```
POST /auth/logout
```

### Description

This endpoint is called when the Bamboo Client user want to log off using `exit`/`quit` command. Bamboo Teamserver will update the user status in the database using the `model users` and will generate a log. Bamboo Teamserver will also remove the username from the WebSocket Client dictionary.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|


### Request example

```
{
    "username": "bambooUser"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"message": "logout"}|Successfully Logout|
|`404`|{"message": "failed"}|Invalid Body|

### Response example

```
{
    "message": "logout"
}
```


<!-- Endpoint 4 -->
<br>

## Check Agent Status

Determing agent status and return back to Bamboo Client

### Endpoint

```
POST /auth/check_agent_status
```

### Description

When Bamboo Client user uses commands such as {`exploit` and `cmd`}, Bamboo Client will need to determine if the Bamboo Agent in use is online. This endpoint uses the `model obtain_status` and will return the status of the specific Bamboo Agent.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|


### Request example

```
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "agent_status": agent_status}|Successfully Logout|
|`404`|{"status": "failed"}|Invalid Body|

### Response example

```
{
    "status": "success",
    "agent_status": "online"
}
```