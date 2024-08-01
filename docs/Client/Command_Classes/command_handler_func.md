# `handler_func`

The handler_func class provides methods that are handy for the user but are not related to commands, exploits, and authorization. This includes processes such as displaying all agents, displaying all users, and more.



## display

Retrieves information from the database

### Endpoint

```
POST /handler_func/agent/display
```

### Description

This function sends a POST request to retrieve agent and heartbeat status data from the server. It then formats and displays this data in a table with color-coded statuses.

### Function Argument

| Field     | Type   | Description                       |
| --------- | ------ | --------------------------------- |
| username  | String | Username of the user              |
| jwt_token | String | JSON Web Token for authentication |

### Arguments Example

```
display("bambooUser", jwt_token)
```

### Function Return

| Field | Type | Description                            |
| ----- | ---- | -------------------------------------- |
| table | List | List containing headers and table data |



## use_agent

Obtains agent information and caches it for future use

### Endpoint

```
POST /handler_func/handler/use_agent
```

### Description

This function requests agent data using its identifier and caches the data for future use. It also handles cases where the agent does not exist.

### Function Argument

| Field            | Type   | Description                       |
| ---------------- | ------ | --------------------------------- |
| username         | String | Username of the user              |
| agent_identifier | String | Identifier of the agent           |
| jwt_token        | String | JSON Web Token for authentication |

### Arguments Example

```
use_agent("bambooUser", "5zrire9a", jwt_token)
```

### Function Return

| Field      | Type | Description                                      |
| ---------- | ---- | ------------------------------------------------ |
| agent_data | Dict | Dictionary containing agent information or empty |



## stop_agent

Clears the cache and stops using the specified agent

### Endpoint

```
POST /handler_func/handler/stop_agent
```

### Description

This function sends a request to stop using a specified agent and clears any cached data related to that agent.

### Function Argument

| Field            | Type   | Description                       |
| ---------------- | ------ | --------------------------------- |
| username         | String | Username of the user              |
| agent_identifier | String | Identifier of the agent           |
| jwt_token        | String | JSON Web Token for authentication |

### Arguments Example

```
stop_agent("bambooUser", "5zrire9a", jwt_token)
```

### Function Return

| Field  | Type   | Description                  |
| ------ | ------ | ---------------------------- |
| Status | String | Status of the stop operation |



## remove_agent

Removes an agent from the database

### Endpoint

```
POST /handler_func/handler/remove_agent
```

### Description

This function sends a request to remove an agent from the database and handles success or failure responses. If the agent is still running, it will sent server will send a `kill` command to stop the agent from running.

### Function Argument

| Field            | Type   | Description                       |
| ---------------- | ------ | --------------------------------- |
| username         | String | Username of the user              |
| agent_identifier | String | Identifier of the agent           |
| jwt_token        | String | JSON Web Token for authentication |

### Arguments Example

```
remove_agent("bambooUser", "5zrire9a", jwt_token)
```

### Function Return

| Field  | Type   | Description                  |
| ------ | ------ | ---------------------------- |
| Status | String | Status of the stop operation |



## info_status

Checks the status of a specific agent

### Endpoint

```
POST /handler_func/handler/info_status
```

### Description

This function checks the status of a specified agent by sending a request to the server.

### Function Argument

| Field            | Type   | Description                       |
| ---------------- | ------ | --------------------------------- |
| username         | String | Username of the user              |
| agent_identifier | String | Identifier of the agent           |
| jwt_token        | String | JSON Web Token for authentication |

### Arguments Example

```
info_status("bambooUser", "5zrire9a", jwt_token)
```

### Function Return

| Field  | Type   | Description         |
| ------ | ------ | ------------------- |
| Status | String | Status of the agent |



## view_users

Views and displays all users in the database

### Endpoint

```
POST /handler_func/handler/view_users
```

### Description

This function retrieves and displays user information from the database, showing their status as well.

### Function Argument

| Field     | Type   | Description                       |
| --------- | ------ | --------------------------------- |
| username  | String | Username of the user              |
| jwt_token | String | JSON Web Token for authentication |

### Arguments Example

```
view_users("bambooUser", jwt_token)
```

### Function Return

| Field | Type | Description                           |
| ----- | ---- | ------------------------------------- |
| Table | List | List containing headers and user data |



## register_user

Registers a new user in the database

### Endpoint

```
POST /handler_func/handler/register_user
```

### Description

This function sends a request to register a new user and handles responses based on the result of the registration attempt.

### Function Argument

| Field        | Type   | Description                       |
| ------------ | ------ | --------------------------------- |
| username     | String | Username of the user              |
| new_username | String | Username of the new user          |
| new_password | String | Password of the new user          |
| jwt_token    | String | JSON Web Token for authentication |

### Arguments Example

```
register_user("bambooUser", "bambooUserTwo", "paSswORd@111", jwt_token)
```

### Function Return

| Field  | Type   | Description                |
| ------ | ------ | -------------------------- |
| Status | String | Status of the registration |



## delete_user

Deletes a user from the database

### Endpoint

```
POST /handler_func/handler/delete_user
```

### Description

This function sends a request to delete a specified user from the database.

### Function Argument

| Field        | Type   | Description                       |
| ------------ | ------ | --------------------------------- |
| username     | String | Username of the user              |
| del_username | String | Username of the user to delete    |
| jwt_token    | String | JSON Web Token for authentication |

### Arguments Example

```
delete_user("bambooUser", "bambooUserTwo", jwt_token)
```

### Function Return

| Field  | Type   | Description                      |
| ------ | ------ | -------------------------------- |
| Status | String | Status of the deletion operation |
