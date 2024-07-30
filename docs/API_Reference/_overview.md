# Overview

## Introduction
This section documents the Teamserver's endpoints. One of the main forms of communication that the Teamserver uses is Hypertext Transfer Protocol Secure (HTTPS). By using flask, blueprint, and flask_jwt_extended library for Secure Sockets Layer (SSL) and JSON Web Token (JWT), this ensures that all data exchanged between clients and the server is encrypted and secure, protecting sensitive information from unauthorized access. 

Flask Blueprint allows related APIs to be grouped together in the same file, under a common prefix. Flask flask_jwt_extended on the other hand provides an easy and secure way to handle JSON Web Tokens (JWTs) for authentication and authorization.

## Base URL

```
https://[teamserver_ip]:[port]
```
For example, if your teamserver is hosted locally on port 4000, your base URL would be

```
https://127.0.0.1:4000
```

## List of Endpoints

The table below shows the list of all RESTful APIs in Bamboo Teamserver, which can be found in /teamserver/api.

|Endpoint|Description|
|--------|-----------|
|POST /agent/heartbeat|For agent to ping at regular intervals to indicate that it is alive|
|POST /agent/initial_connection/register|For agent to register initial connection|
|POST /agent/agent_response|For agent to send back the response of a command|
|POST /download/<filename>|For agent to download a file from server|
|GET /auth/|For clients to check if server is online|
|POST /auth/login|For user to log in to the server|
|POST /auth/logout|For user to log out of server|
|POST /auth/check_agent_status|To check an agent’s status (dead, alive)|
|POST /exploit/quit|For user to exit the [exploit] command|
|POST /exploit/send_config|For user to send configurations for an exploit when using the [exploit] command|
|POST /exploit/view_all|For user to view all exploits in the database using the [exp] command|
|POST /exploit/add|For user to add exploits using the [add] command|
|POST /exploit/delete|For user to delete exploits using the [delete] command|
|POST /exploit/exist|To check if exploit exists|
|POST /exploit/modify|For user to modify an existing exploit in the database|
|POST /handler_func/agent/display|For user to view all agents using the [display] command|
|POST /handler_func/use_agent|For user to use an agent|
|POST /handler_func/stop_agent|For user to stop using an agent|
|POST /handler_func/remove_agent|For user to remove an agent from database|
|POST /handler_func/handler/info_status|For user to check the status of an agent|
|POST /handler_func/handler/view_users|For user to view all users in database|
|POST /handler_func/handler/register_user|For user to register a new user|
|POST /handler_func/handler/delete_user|For user to delete a user|
|POST /handler_func/cmd|For user to send commands to an agent to run in the target’s terminal|
|POST /handler_func/handler_output|For user to print the response of a command from the agent|
|POST /handler_func/teamchat|For user to send a message to teamchat|

There are a total of 5 prefixes used in Bamboo Teamserver with the flask blueprint library for all HTTPS APIs. All of the prefixes are organised together as they are for easier management.

|Prefix|Description|Examples|
|------|-----------|--------|
|/auth|For authentication and status related|/login, /check_agent_status|
|/agent|Only for Bamboo Agent to request|/heartbeat, /post_exploit/keylog|
|/handler_func|For Bamboo Client to request, does not involve Bamboo Agent|/agent/display, /handler/delete_user|
|/exploit|For exploit related|/send_config, /delete|
|/postexp|For post exploit related|/keylog, /retrieve|
