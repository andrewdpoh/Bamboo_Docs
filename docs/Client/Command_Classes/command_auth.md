# `auth`

The auth class provides methods to interact with a server for user authentication and agent status management. It facilitates operations such as checking server availability, user login, user logout, and checking the status of agents. Each method in the class is designed to communicate with specific endpoints of the server API, handling tasks related to user authentication and session management.

## check

Determines if the server is online

### Endpoint

```
GET /auth/
```

#### Function argument

**This function does not require any argument**

### Description

This function attempts to connect to the server by sending a GET request to the `/auth/` endpoint. If the connection is successful, it returns "success." If the server cannot be reached, it prints an error message and returns "failed."

###

### Function return

| Field  | Type   | Description                                                    |
| ------ | ------ | -------------------------------------------------------------- |
| Status | String | Indicates whether the connection to the server was successful. |



## authentication

Authenticates the user

### Endpoint

```
POST /auth/login
```

### Description

This function sends a POST request to the `/auth/login` endpoint with the provided username and password. If the credentials are correct, the server returns a JSON response containing the login status and a JWT token. The function returns the login status and the JWT token if available.

#### Function argument

| Field    | Type   | Description      |
| -------- | ------ | ---------------- |
| username | String | Username of user |
| password | String | Password of user |

### Arguments Example

```
authentication("bambooUser", "adnap")
```

### Function return

| Field     | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| Status    | String | Status of login              |
| jwt_token | String | JWT token for authentication |



## logout

Logs out the user

### Endpoint

```
POST /auth/logout
```

### Description

This function sends a POST request to the `/auth/logout` endpoint with the provided username. If the server responds with a status code of 200, it prints a message indicating that the user has exited the server.

#### Function argument

| Field     | Type   | Description                  |
| --------- | ------ | ---------------------------- |
| username  | String | Username of user             |
| jwt_token | String | JWT token for authentication |

### Arguments Example

```
logout("bambooUser", jwt_token)
```

### Function Return

**The function does not return anything**



## check_agent_status

Checks the status of an agent.

### Endpoint

```
POST /auth/check_agent_status
```

### Description

This function sends a POST request to the `/auth/check_agent_status` endpoint with the provided username and agent identifier. The server responds with the status of the agent, which is returned as a JSON object.

#### Function argument

| Field            | Type   | Description                  |
| ---------------- | ------ | ---------------------------- |
| username         | String | Username of user             |
| agent_identifier | String | Identifier for the agent     |
| jwt_token        | String | JWT token for authentication |

### Arguments Example

```
check_agent_status("bambooUser", "5zrire9a", jwt_token)
```

### Function return

| Field    | Type   | Description     |
| -------- | ------ | --------------- |
| response | String | Status of Agent |
