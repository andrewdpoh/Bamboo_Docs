# ALDEN API - Post Exploit

<!-- Endpoint 1 -->
<br>

## Keylogging

Start/Stop keylogging activity of specified Bamboo Agent

### Endpoint

```
POST /postexp/keylog
```

### Description

Bamboo Client calls this endpoint when they want to start/stop keylogging activity. All activities will be recorded down into a `global variable: keylog_status`. keylog_status is a dictionary that keeps track of all keylog activity within Bamboo Teamserver. Therefore, with this global variable, Bamboo Teamserver will be able to tell if the Bamboo Client user is starting or stopping the keylogging. After Bamboo Teamserver know the action to command, a WebSocket broadcast will be made to the Bamboo Agent Specified. This command can be called by any Bamboo Agent with any privilege level.

### Request schema

#### Request body

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (keylog)|

### Request example

```
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

```
{
    "status": "success",
    "action": "start"
}
```

### WebSocket schema

#### WebSocket body

|Field|Type|Description|
|-----|----|-----------|
|command|String|post exploit|
|method|String|Keylogging|
|handler|String|User that commanded|
|status|String|To start/stop keylogging|

### WebSocket example

```
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

Start enumerating an infected machine

### Endpoint

```
POST /postexp/enum
```

### Description

Bamboo Client calls this endpoint when they want to enumerate the infected machine remotely using the specified Bamboo Agent. Bamboo teamserver will send a WebSocket broadcast to the Bamboo Agent specified and command it to start enumerate the infected machine. This command can be called by any Bamboo Agent with any privilege level.

### Request schema

#### Request body

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (enumerate)|

### Request example

```
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

```
{
    "status": "success"
}
```

### WebSocket schema

#### WebSocket body

|Field|Type|Description|
|-----|----|-----------|
|command|String|post exploit|
|method|String|Keylogging|
|handler|String|User that commanded|

### WebSocket example

```
{
    "command": "post exploit",
    "method": "enumerate",
    "handler": "bambooUser"
}
```

<!-- Endpoint 3 -->
<br>

## SSS_Retrieve

Retrieve registry hive of infected machine

### Endpoint

```
POST /postexp/reteive
```

### Description

Bamboo Client calls this endpoint when they want to retrieve the registry hive of the infected machine remotely using the specified Bamboo Agent. This command can only be called by Bamboo Agent with `High` or `System` level privilege. If the requirements are met, Bamboo teamserver will send a WebSocket broadcast to the Bamboo Agent specified and command it to start retrieving the registry hive of the infected machine.

### Request schema

#### Request body

|Field|Type|Description|
|-----|----|-----------|
|username|String|Username of user|
|agent_identifier|String|Identifier of Bamboo Agent|
|method|String|Tool used (enumerate)|
|priv_lvl|String|Privilege level of Bamboo Agent|

### Request example

```
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

```
{
    "status": "success"
}
```

### WebSocket schema

#### WebSocket body

|Field|Type|Description|
|-----|----|-----------|
|command|String|post exploit|
|method|String|Keylogging|
|handler|String|User that commanded|

### WebSocket example

```
{
    "command": "post exploit",
    "method": "sss retrieve",
    "handler": "bambooUser"
}
```