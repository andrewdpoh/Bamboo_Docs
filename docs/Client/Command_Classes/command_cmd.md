# `commands`

The commands class provides methods for interacting with an agent through various server endpoints. This includes processes like exploiting an agent, sending commands, enumerating system information, and performing post-exploitation activities.



## exploit_process

Starts an exploit process on the specified agent

### Endpoint

```
POST /exploit/quit
POST /exploit/view_all
POST /exploit/send_config
```

### Description

This function first retrieves all available exploits from the Bamboo Teamserver using the `/exploit/view_all` endpoint. The user will select an exploit, and start configuring it. This function is dynamic in a way that only shows what can be chosen to the user. As different exploits have different configurations, each exploit configuration steps may be different. If during the configuration, the user wants to stop the process, the `/exploit/quit` endpoint will be called for logging purposes. The `/exploit/send_config` endpoint will be called to proceed once the user confirms the exploitation.

### Function Argument

| Field            | Type   | Description                       |
| ---------------- | ------ | --------------------------------- |
| username         | String | Username of the user              |
| agent_identifier | String | Identifier of the agent           |
| jwt_token        | String | JSON Web Token for authentication |

### Arguments Example

```
exploit_process("bambooUser", "5zrire9a", jwt_token)
```

### Function Return

| Field  | Type   | Description                              |
| ------ | ------ | ---------------------------------------- |
| Status | String | Status of the exploit process initiation |



## command_prompt

Sends a command to the agent and retrieves the output

### Endpoint

```
POST /handler_func/cmd
```

### Description

This function will send the command input by the user and then continuously checks for the response until it is received or a timeout occurs.

### Function Argument

| Field            | Type   | Description                         |
| ---------------- | ------ | ----------------------------------- |
| username         | String | Username of the user                |
| agent_identifier | String | Identifier of the agent             |
| cmd              | String | Command to be executed on the agent |
| jwt_token        | String | JSON Web Token for authentication   |

### Arguments Example

```
command_prompt("bambooUser", "5zrire9a", "whoami", jwt_token)
```

### Function Return

| Field  | Type   | Description                                   |
| ------ | ------ | --------------------------------------------- |
| Output | String | Output from the command executed on the agent |



## enum

Enumerates information about the target machine

### Endpoint

```
POST /postexp/enum
```

### Description

This method requests the enumeration of an target machine and indicates that the result is back and can be viewed.

### Function Argument

| Field            | Type   | Description                         |
| ---------------- | ------ | ----------------------------------- |
| username         | String | Username of the user                |
| agent_identifier | String | Identifier of the agent             |
| priv_lvl         | String | Privilege level for the enumeration |
| jwt_token        | String | JSON Web Token for authentication   |

### Arguments Example

```
enum("bambooUser", "5zrire9a", "High", jwt_token)
```

### Function Return

| Field  | Type   | Description                       |
| ------ | ------ | --------------------------------- |
| Status | String | Status of the enumeration request |



## postexp

Command post exploitation tools provided

### Endpoint

```
POST /postexp/{method}

POST /postexp/keylog
POST /postexp/retrieve
```

### Description

This function will send the command to the Bamboo Agent and depending on the method (keylog/retrieve), there will be different outputs. SSS_Retrieve can only be used if the Bamboo Agent privilege is "High" or "System".

### Function Argument

| Field            | Type   | Description                               |
| ---------------- | ------ | ----------------------------------------- |
| username         | String | Username of the user                      |
| agent_identifier | String | Identifier of the agent                   |
| method           | String | Post-exploitation method to be executed   |
| priv_lvl         | String | Privilege level for the post-exploitation |
| jwt_token        | String | JSON Web Token for authentication         |

### Arguments Example

```
postexp("bambooUser", "5zrire9a", "keylog", "Medium", jwt_token)
```

### Function Return

| Field  | Type   | Description                            |
| ------ | ------ | -------------------------------------- |
| Status | String | Status of the post-exploitation action |
