# /postexp

<!-- Endpoint 1 -->
## Keylogging

Start/Stop keylogging activity of specified Bamboo Agent

### Endpoint

```
POST /postexp/keylog
```

### Description

Bamboo Client calls this endpoint when they want to start/stop keylogging activity. All activities will be recorded down into a global variable: [`keylog_status`](../global_variables.md). keylog_status is a dictionary that keeps track of all keylog activity within Bamboo Teamserver. Therefore, with this global variable, the Bamboo Teamserver will be able to tell if the Bamboo Client user is starting or stopping the keylogging. After the Bamboo Teamserver knows the action to command, a WebSocket broadcast will be made to the Bamboo Agent Specified. This command can be called by any Bamboo Agent with any privilege level.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (keylog)|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a",
    "method": "keylog"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success", "action": status}|Successfully command Bamboo Agent|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "failed"}|Invalid Body|

### Response example

```JSON
{
    "status": "success",
    "action": "start"
}
```

### WebSocket schema

<h4>Websocket body</h4>

|Field|Type|Description|
|-----|----|-----------|
|command|String|post exploit|
|method|String|Keylogging|
|handler|String|User that commanded|
|status|String|To start/stop keylogging|

### WebSocket example

```JSON
{
    "command": "post exploit",
    "method": "keylog",
    "handler": "bambooUser",
    "status": "start"
}
```


<!-- Endpoint 2 -->
<br>

## Enumeration

Start enumerating an target machine

### Endpoint

```
POST /postexp/enum
```

### Description

Bamboo Client calls this endpoint when they want to enumerate the target machine remotely using the specified Bamboo Agent. The Bamboo teamserver will send a WebSocket broadcast to the Bamboo Agent specified and command it to start enumerate the target machine. This command can be called by any Bamboo Agent with any privilege level.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (enumerate)|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a",
    "method": "enum"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully command Bamboo Agent|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "failed"}|Invalid Body|

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
|command|String|post exploit|
|method|String|Enumerate|
|handler|String|User that commanded|

### WebSocket example

```JSON
{
    "command": "post exploit",
    "method": "enumerate",
    "handler": "bambooUser"
}
```

<!-- Endpoint 3 -->
<br>

## SSS_Retrieve

Retrieve registry hive of target machine

### Endpoint

```
POST /postexp/retrieve
```

### Description

Bamboo Client calls this endpoint when they want to retrieve the registry hive of the target machine remotely using the specified Bamboo Agent. This command can only be called by Bamboo Agent with `High` or `System` level privilege. If the requirements are met, the Bamboo teamserver will send a WebSocket broadcast to the Bamboo Agent specified and command it to start retrieving the registry hive of the target machine.

### Request schema

<h4>Request body</h4>

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (retrieve)|
|priv_lvl|String|Privilege level of Bamboo Agent|

### Request example

```JSON
{
    "username": "bambooUser",
    "agent_identifier": "5zrire9a",
    "method": "enum",
    "priv_lvl": "System"
}
```

### Response schema

|Status Code|Schema|Description|
|-----------|------|-----------|
|`200`|{"status": "success"}|Successfully command Bamboo Agent|
|`400`|{"status": "Agent is not connected to C2 WS"}|Failed to broadcast to Bamboo Agent|
|`404`|{"status": "failed"}|Invalid Body|

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
|command|String|post exploit|
|method|String|Retrieve|
|handler|String|User that commanded|

### WebSocket example

```JSON
{
    "command": "post exploit",
    "method": "sss retrieve",
    "handler": "bambooUser"
}
```