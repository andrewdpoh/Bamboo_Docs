# /agent

<!-- Endpoint 1 -->
## Agent Heartbeats

Record Bamboo Agent heartbeat

### Endpoint

```
POST /agent/heartbeat
```

### Description

Agent heartbeats endpoint is for Bamboo Agents to 'ping' after their initial connection. This API helps determine if a Bamboo Agent is still 'alive' and running. Heartbeat, is a mechanism used in Bamboo to ensure that an individual Bamboo Agent is still 'alive' and running. The initial connection will give Bamboo Agents 5 seconds before the next heartbeat is expected. After that, the Bamboo Agent will continue sending their heartbeat at random between 5 to 10 seconds. This endpoint will use the `model add_heartbeat` to repeatedly update the `collection heartbeats`.

After obtaining the 2 data in the request body from Bamboo Agent, Bamboo Teamserver will take the time that the request was made and compare it with the expected_heartbeat column in the database. Refer to db collection heartbeats for more information.

If the current time is later than the expected time, it would mean that the Bamboo Agent was 'dead' and it became 'alive' after a while. While if the current time matches the expected time for the next heartbeat, it would mean that the Bamboo Agent is 'punctual' and still alive.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|heartbeat|Integer|Seconds before the next heartbeat|

### Request example

```
{
    "agent_identifier": "5zrire9a",
    "heartbeat": 8
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "alive"}|Success|
|`404`|{"message": "Invalid Body"}|Invalid Body|

### Response example

```
{
    "status": "alive"
}
```

<!-- ENDPOINT 2 -->
<br>

## Registering Agent

Register new Bamboo Agent

### Endpoint

```
POST /agent/initial_connection/register
```

### Description

The Register Agent endpoint is called when a Bamboo Agent is executed. The Bamboo Agent will request for this endpoint to register itself into Bamboo Teamserver and using the `model check_agent_identifier`, Bamboo Teamserver will be able to generate unique agent identifiers and avoid duplicates.

Bamboo Teamserver will create a new unique agent identifier for all Bamboo Agent. Once the agent identifier is created, Bamboo Teamserver will update the database in the `agents collection` using  the `model add_agent` with the new Bamboo Agent information. Not only that, also update the `heartbeat collection` using the `model add_heartbeat` and give the agent 5 seconds buffer time to request for the next heartbeat. For more details for the collections, do refer here for the `heartbeat collection` and here for the agents collection.

After the procedure is completed, Bamboo Teamserver will broadcast to all connected Bamboo Clients that a new Bamboo Agent is connected, with its agent identifier. From there, Bamboo Client users will be able to interact and view the information using commands. For more information on commands, do refer to command.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|hostname|String|Hostname if infected machine|
|publicIP|String|Public IP address of infected machine|
|privateIP|String|Private IP address of infected machine|
|Integrity|String|Privilege level of Bamboo Agent|

### Request example

```
{
    "hostname": "bambooMachine",
    "publicIP": "39.100.49.231",
    "privateIP": "192.168.45.7",
    "Integrity": "medium"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"listener_status": "connected", "agent_identifier", "5zrire9a"}|Success|
|`404`|{"message": "Invalid Body"}|Invalid Body|

### Response example

```
{
    "listener_status": "connected",
    "agent_identifier": "5zrire9a"
}
```


<!-- ENDPOINT 3 -->
<br>

## Command Response

Store response of command for `cmd` Bamboo Client command

### Endpoint

```
POST /agent/agent_response
```

### Description

Command Response endpoint is part of the {`cmd` command} component. This endpoint receives the response of the Bamboo Agent after the Bamboo Client user sends a command over. Bamboo Teamserver will then update a dictionary in the global variable for /handler/handler_output API to receive it, which details are in here. 

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|response|String|Result of command (e.g. `whoami`)|

### Request example

```
{
    "agent_identifier": "5zrire9a",
    "response": "bambooMachine\panda"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "response", "bambooMachine\panda"}|Success|
|`404`|{"message": "Invalid Body"}|Invalid Body|

### Response example

```
{
    "status": "success",
    "response": "bambooMachine\panda"
}
```


<!-- ENDPOINT 4 -->
<br>

## File Download

Download exploit files by name

### Endpoint

```
GET /agent/download/&lt;filename&gt;
```

### Description

During exploiting phrase, if drop file is required, Bamboo Agent will request for this API to download the exploit file. All exploit files is located in `/exploits` folder


### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|File|Success|
|`404`|Null|Invalid Body|



<!-- ENDPOINT 5 -->
<br>

## Keylog Result

Store post exploit (`keylog`) result (keystrokes)

### Endpoint

```
POST /agent/post_exploit/keylog
```

### Description

Keylog Result will be called by Bamboo Agent when Bamboo Client command the Bamboo Agent to stop recording keystrokes. There will be error checking to determine if there were any error, if there are no errors, Bamboo Teamserver will send the keystroke to the user via WebSocket.


### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|status|String|State of agent: `done`, `start`, `error`|
|keystroke|String|Key strokes recorded|
|handler|String|Bamboo Client user that started the keylogging|
|error|String|If status is error, will state error|

### Request example

```
{
    "agent_identifier": "5zrire9a",
    "status": "done":,
    "keystroke": "keystrokesrecorded",
    "handler": "Bamboo User A",
    "error": ""
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"message": "success"}|Successfully sent broadcasted to Bamboo Client|
|`400`|{"message": "failed"}|Failed to broadcast to Bamboo Client|
|`404`|{"message": "error"}|There was an error when logging keystrokes|

### Response example

```
{
    "message": "success"
}
```


### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|keylogMsg|String|Keystrokes recorded|
|agent_identifier|String|Identifier of Bamboo Agent|

### WebSocket example

```
{
    "keylogMsg": "keystrokesrecorded",
    "agent_identifier": "5zrire9a"
}
```


<!-- Endpoint 6 -->
<br>

## Enumerate Result

Store enumeration (`enum`) result

### Endpoint

```
POST /agent/post_exploit/enumerate
```

### Description

Enumerate Result will be called by Bamboo Agent when Bamboo Client command the Bamboo Agent to enumerate the infected machine. There will be error checking to determine if there were any error, if there are no errors, Bamboo Teamserver will send the enumerate results to the user via WebSocket.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|status|String|State of agent: `done`, `error`|
|result|String|Enumerate Result|
|handler|String|Bamboo Client user that started the keylogging|
|error|String|If status is error, will state error|

### Request example

```
{
    "agent_identifier": "5zrire9a",
    "status": "done":,
    "result": <a very long list of string>,
    "handler": "Bamboo User A",
    "error": ""
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"message": "success"}|Successfully sent broadcasted to Bamboo Client|
|`400`|{"message": "failed"}|Failed to broadcast to Bamboo Client|
|`404`|{"message": "error"}|There was an error when enumerating|

### Response example

```
{
    "message": "success"
}
```


### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|enumerateMsg|String|Enumerated result|
|agent_identifier|String|Identifier of Bamboo Agent|

### WebSocket example

```
{
    "enumerateMsg": <a very long list of string>,
    "agent_identifier": "5zrire9a"
}
```



<!-- Endpoint 7 -->
<br>

## SSS_Retrieve Result

Store SSS_Retrieve (`retrieve`) result

### Endpoint

```
POST /agent/post_exploit/sss_retrieve
```

### Description

SSS_Retrieve Result will be called by Bamboo Agent when Bamboo Client command the Bamboo Agent to Retrieve registry hives from the infected machine. There will be error checking to determine if there were any error, if there are no errors, Bamboo Teamserver will send the retrieved results to the user via WebSocket.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|status|String|State of agent: `done`, `error`|
|files|String|Dictionary of binary|
|handler|String|Bamboo Client user that started the keylogging|
|error|String|If status is error, will state error|

### Request example

```
{
    "agent_identifier": "5zrire9a",
    "status": "done":,
    "result": <dictionary of binary>,
    "handler": "Bamboo User A",
    "error": ""
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"message": "success"}|Successfully sent broadcasted to Bamboo Client|
|`400`|{"message": "failed"}|Failed to broadcast to Bamboo Client|
|`404`|{"message": "error"}|There was an error when enumerating|

### Response example

```
{
    "message": "success"
}
```


### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|retrieveMsg|String|Enumerated result|
|agent_identifier|String|Identifier of Bamboo Agent|

### WebSocket example

```
{
    "retrieveMsg": <dictionary of binary>,
    "agent_identifier": "5zrire9a"
}
```