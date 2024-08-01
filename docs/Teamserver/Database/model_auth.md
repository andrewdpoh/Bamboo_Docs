# Model Class - authentication

<!-- models, collections, and global_var with back ticks is to be link (n remove back ticks) -->
<!-- commands within braces {} are to be link as well -->

This class contains all models that will be related to authentication. Therefore, it will only use the find method as the other methods are not needed for authentication related actions. This class will be interacting with the [user](../Database/collections.md#users) collection and the [heartbeats](../Database/collections.md#heartbeats) collection.

<!-- Func 1 -->

## login_auth

Authenticates Bamboo Client user credentials

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /auth/login
```

### Description

login_auth will be called every time a Bamboo Client user wants to log in. This model will first determine if the username exist in the `collection users`. If it exist, it will then compare between the password one provided by the user and the password in the database and return the status accordingly. 

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username input by user|
|password|String|Password input by user|

### Arguments Example

```
login_auth("bambooUser", "adnap")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|user|List of specified user information|

### Find Example

```
[
    "username": "bambooUser",
    "password": "adnap",
    "status": "offline"
]
```

### Function Return

|Type|Description|
|----|-----------|
|String|Notify Bamboo Teamserver of status|

### Return Example

```
Welcome
```

```
Invalid-User
```


<!-- Func 2 -->
<br>

## obtain_status

Helps Bamboo Teamserver to determine spe

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /auth/check_agent_status
```

### Description

obtain_status helps Bamboo Teamserver to obtain the status of the specified Bamboo Agent in the `collection heartbeats`. This is used when Bamboo Client user want to use a command that requires the Bamboo Agent to be "alive". It only returns that Bamboo Agent status.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
obtain_status("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|heartbeats|List of specified Bamboo Agent information|

### Find Example

```
[   
    "agent_identifier": "5zrire9a",
    "heartbeat": 6,
    "current_time": "2024-07-30T16:38:15.653+00:00",
    "expected_time": "2024-07-30T16:38:21.653+00:00",
    "status": "dead"
]
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Notify Bamboo Teamserver of Bamboo Agent status|

### Return Example

```
"agent_status": "alive"
```