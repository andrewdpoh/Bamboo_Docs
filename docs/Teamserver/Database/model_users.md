# Model Class - users

<!-- models, collections, and global_var with back ticks is to be link (n remove back ticks) -->
<!-- commands within braces {} are to be link as well -->

This class contains all models related to users. Bamboo Teamserver will make use of the functions within this class to find, update, add, and delete user information stored in the database according to Bamboo Client command. This class will be interacting with the [users](../Database/collections.md#users) collection only

<!-- Func 1 -->

## view_users

Retrieve all users information

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/handler/view_users
```

### Description

view_users retrieves all user information stored in the database from the [users](../Database/collections.md#users) collection. After retrieving the information, the model will delete the password column, making only the username and status return.

#### Function Arguments

**Does not require any arguments**

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|user|List of user information excluding password|

### Function Return

|Type|Description|
|----|-----------|
|List|List of all user information excluding password|

### Return Example

```
[
    [
        "bambooUser",
        "offline"
    ],
    [
        "bambooUserTwo",
        "online"
    ]
]
```

<!-- Func 2 -->
<br>

## user_online

Updates user status to online

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /auth/login
```

### Description

When a Bamboo Client user log ins, Bamboo Teamserver will call this model to update the username status to "online" in the [users](../Database/collections.md#users) collection.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of Bamboo Client user|

### Arguments Example

```
user_online("bambooUser")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|update_many|user|Status of update|

### Update Example

```JSON
{
    "username": "bambooUser"
}, 
{"$set": 
    {
        "status": "online"
    }
}
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Status of update|

### Return Example

```JSON
{"status": "done"}
```

<!-- Func 3 -->
<br>

## user_offline

Updates user status to offline

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /auth/logout
```

### Description

When a Bamboo Client user log outs, Bamboo Teamserver will call this model to update the username status to "offline" in the [users](../Database/collections.md#users) collection.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of Bamboo Client user|

### Arguments Example

```
user_offline("bambooUser")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|update_many|user|Status of update|

### Update Example

```JSON
{
    "username": "bambooUser"
}, 
{"$set": 
    {
        "status": "offline"
    }
}
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Status of update|

### Return Example

```JSON
{"status": "done"}
```

<!-- Func 4 -->
<br>

## register_user

Insert new user into the database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/handler/register_user
```

### Description

register_user is called when the Bamboo Client wants to register a set of new credentials into Bamboo Teamserver in the [users](../Database/collections.md#users) collection.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|New username|
|password|String|New password|

### Arguments Example

```
register_user("bambooUserNew", "paSsWOrd@111")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|insert_one|user|Status of insertion|

### Insert Example

```JSON
{
    "username": "bambooUserNew",
    "password": "paSsWOrd@111",
    "status": "offline"
}
```

### Function Return

|Type|Description|
|----|-----------|
|Boolean|Status of insertion|

### Return Example

```
True
```

<!-- Func 5 -->
<br>

## delete_user

Remove existing user from the database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/handler/delete_user
```

### Description

delete_user is called when a Bamboo Client wants to remove a set of credentials from Bamboo Teamserver [users](../Database/collections.md#users) collection. Before deleting the credential, the model will determine if the username given exist, if it exist, Bamboo Teamserver will delete that set of credential.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username to delete|

### Arguments Example

```
delete_user("bambooUserNew")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|user|Determine if the username exist|
|delete_many|user|Delete credentials from the database|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Status of insertion|

### Return Example

```JSON
{"status": "success"}
```

<!-- Func 6 -->
<br>

## find_one

Retrieve a specific user information

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/handler/register_user
```

### Description

find_one main objective is to determine if a username exist in the database. It will determine if the user exist in the database, [users](../Database/collections.md#users) collection, before returning the status back to Bamboo Teamserver.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username to find|

### Arguments Example

```
find_one("bambooUserNew")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|user|Determine if the username exist|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Existence of user|

### Return Example

```JSON
{"status": "success"}
```