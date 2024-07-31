# /handler_func

<!-- Endpoint 1 -->
## Display Agents

Extract all Bamboo Agent information from database

### Endpoint

```
POST /handler_func/agent/display
```

### Description

This endpoint is called when a Bamboo Client user wants to view all current Bamboo Agents registered in Bamboo Teamserver using the command [`display`](../Client/commands.md#display). Using the model [show_agents](../Database/model_agents.md#show_agents) and model [get_heartbeat](../Database/model_agents.md#get_heartbeat), Bamboo Teamserver will be able to extract all register Bamboo Agents information and status from the database.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|

### Request example

```JSON
{
    "username": "bambooUser"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "agent": agent, "heartbeat": heartbeat}|Success|
|`404`|{"status": "failed"}|Invalid Body|
|`500`|{"status": "failed"}|Something went wrong|

### Response example

```JSON
{
    "status": "success",
    "agent": <list of agent information>,
    "heartbeat": <list of agent's heartbeat information>
}
```

<!-- Endpoint 2 -->
<br>

## Using Agents

Extract specified agent information

### Endpoint

```
POST /handler_func/handler/use_agent
```

### Description

This endpoint is called when a Bamboo Client user wants to start using a Bamboo Agent to interact with using the command [`use [agent]`](../Client/commands.md#use). Using the model [use_agent](../Database/model_agents.md#use_agent), Bamboo Teamserver will be able to identify if the Bamboo Agent specified exist. If it does, the data of that Bamboo Agent will be return.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "agent_data": agent_data}|Success|
|`404`|{"status": "failed"}|Invalid Body|
|`500`|{"status": "failed"}|Something went wrong|

### Response example

```JSON
{
    "status": "success",
    "agent_data": <list of specified Bamboo Agent data>
}
```


<!-- Endpoint 3 -->
<br>

## Stop Using Agents

Stop using agents, for logging purposes

### Endpoint

```
POST /handler_func/handler/stop_agent
```

### Description

This endpoint is called when a Bamboo Client user wants to stop using a Bamboo Agent using the command [`stop`](../Client/commands.md#stop). It is for logging purposes

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"message": "stop"}|Success|
|`404`|{"message": "failed"}|Invalid Body|

### Response example

```JSON
{
    "status": "success",
    "agent_data": <list of specified Bamboo Agent data>
}
```


<!-- Endpoint 4 -->
<br>

## Remove Agent

Remove specified Bamboo Agent

### Endpoint

```
POST /handler_func/handler/remove_agent
```

### Description

This endpoint is called when a Bamboo Client user wants to remove a Bamboo Agent from Bamboo Teamserver using the [`delete [agent]`](../Client/commands.md#delete). Using the model [remove_agent](../Database/model_agents.md#remove_agent), Bamboo Teamserver will delete all instances of the specified Bamboo Agent if it exist. Additionally, if the Bamboo Agent is still running, Bamboo Teamserver will send a [`kill`](../Client/commands.md#kill) command to stop the Bamboo Agent.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Success|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "fail"}|Invalid Body|
|`500`|{"status": "fail"}|Something went wrong|

### Response example

```JSON
{
    "status": "success"
}
```


<!-- Endpoint 5 -->
<br>

## Agent Information

Retrieve a specific Bamboo Agent information

### Endpoint

```
POST /handler_func/handler/info_status
```

### Description

This endpoint is called when a Bamboo Client user wants to the Bamboo Agent in use information using the command [`info`](../Client/commands.md#info). Using the model [info_status](../Database/model_agents.md#info_status), Bamboo Teamserver will be able to extract the information of the requested Bamboo Agent.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "alive"}|Retrieved information and Bamboo is 'alive'|
|`200`|{"status": "dead"}|Retrieved information and Bamboo is 'dead'|
|`404`|{"status": "fail"}|Invalid Body|
|`500`|{"status": "fail"}|Something went wrong|

### Response example

```JSON
{
    "status": "alive"
}
```

<!-- Endpoint 6 -->
<br>

## View all Users

Retrieve all users in Bamboo Teamserver

### Endpoint

```
POST /handler_func/handler/view_users
```

### Description

This endpoint is called when a Bamboo Client user wants to view all registered users in Bamboo Teamserver using the [`users`](../Client/commands.md#users). Using the model [view_users](../Database/model_users.md#view_users), Bamboo Teamserver will be able to extract the username and status of the registered users.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|

### Request example

```JSON
{
    "username": "bambooUser"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "user_data": user_data}|Successfully retrieved all registered user information|
|`404`|{"status": "fail"}|Invalid Body|
|`500`|{"status": "fail"}|Something went wrong|

### Response example

```JSON
{
    "status": "success",
    "user_data": <list of usernames and status>
}
```

<!-- Endpoint 7 -->
<br>

## Add new Users

Resgiter new users into the Bamboo Teamserver

### Endpoint

```
POST /handler_func/handler/register_user
```

### Description

This endpoint is called when a Bamboo Client user wants to register a new user into Bamboo Teamserver using the [`register`](../Client/commands.md#register). Using the model [find_one](../Database/model_users.md#find_one), Bamboo Teamserver will be able to determine if there will be any duplicates of username. After that, it will use the model [register_user](../Database/model_users.md#register_user) to add the information of the new user into the database.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|new_username|String|New user username|
|new_password|String|New user password|

### Request example

```JSON
{
    "username": "bambooUser",
    "new_username": "bambooUserTwo",
    "new_password": "ilovePandas213"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully registered a new user|
|`404`|{"status": "fail"}|Invalid Body|
|`422`|{"status": "duplicate"}|Username already exist|
|`500`|{"status": "fail"}|Something went wrong|

### Response example

```JSON
{
    "status": "success",
}
```

<!-- Endpoint 8 -->
<br>

## Remove Users

Remove Bamboo Client users from Bamboo Teamserver

### Endpoint

```
POST /handler_func/handler/delete_user
```

### Description

This endpoint is called when a Bamboo Client user wants to remove a user from Bamboo Teamserver using the [`remove [username]`](../Client/commands.md#remove). Using the model [delete_user](../Database/model_users.md#delete_user), Bamboo Teamserver will be able to delete the specified user.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|del_username|String|Username to remove|

### Request example

```JSON
{
    "username": "bambooUser",
    "del_username": "bambooUserTwo"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully deleted information of specified username|
|`404`|{"status": "fail"}|Username not found|
|`404`|{"status": "fail"}|Invalid Body|
|`500`|{"status": "fail"}|Something went wrong|

### Response example

```JSON
{
    "status": "success"
}
```

<!-- Endpoint 9 -->
<br>

## Command Prompt

Sends commands to Bamboo Agent

### Endpoint

```
POST /handler_func/cmd
```

### Description

This endpoint is called when a Bamboo Client user wants to start a shell session with a Bamboo Agent using the [`cmd`](../Client/commands.md#cmd). Bamboo Teamserver will use WebSocket to broadcast the command to the specified Bamboo Agent.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|command|String|Command to forward to Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a",
    "command": "whoami"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully broadcast command to Bamboo Agent|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "fail"}|Invalid Body|

### Response example

```JSON
{
    "status": "success"
}
```

### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|command|String|cmd|
|cmd|String|Command that Bamboo Client user input|

### WebSocket example

```JSON
{
    "command": "cmd",
    "cmd": "whoami"
}
```


<!-- Endpoint 10 -->
<br>

## Command Output

Receives reponse from Bamboo Agent during command

### Endpoint

```
POST /handler_func/handler_output
```

### Description

After the Bamboo Client sends a command over to a Bamboo Agent using the [`cmd`](../Client/commands.md#cmd), the Bamboo Client will request for this endpoint and wait for a response. To prevent users for waiting indefinitely, there is a timeout mechanism. Every 10 second, Bamboo Teamserver will check if the command response have been sent every second. If none have been sent, the user will get timeout.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{agent_identifier: response}|Receive response|
|`404`|{"status": "fail"}|Invalid Body|
|`408`|{"status": "timeout"}|User timeout|

### Response example

```JSON
{
    "5zrire9a": "bambooMachine\panda"
}
```

<!-- Endpoint 11 -->
<br>

## Teamchat

Broadcast teamchat message to all other Bamboo Client

### Endpoint

```
POST /handler_func/teamchat
```

### Description

This endpoint is called everytime a Bamboo Client user sends a message in the Teamchat using the [`chat`](../Client/commands.md#chat) in CLI or using the `TEAMCHAT tab` in GUI. Bamboo Teamserver will relay the message from the Bamboo Client to all Bamboo Client using WebSocket broadcast.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|message|String|Message sent into teamchat|

### Request example

```JSON
{
    "username": "bambooUser",
    "message": "hello everyone"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully broadcast command to Bamboo Agent|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "fail"}|Invalid Body|

### Response example

```JSON
{
    "status": "success"
}
```

### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|chatMsg|String|Bamboo Client Message|

### WebSocket example

```JSON
{
    "chatMsg": "hello everyone"
}
```