# Collections

## Database

Bamboo Teamserver uses MongoDB as its database. MongoDB is an unstructured database that stores data in JSON format, which is what Bamboo Client and Bamboo Agent can work easily with. 

Bamboo Teamserver database is called "C2-Server". There are a total of 4 collections, agents, exploits, heartbeats, and user. exploits and user collection should be imported before running while agents and heartbeats collection will be created when certain functions are called.

## Collections

Each collection within the Bamboo Teamserver's C2-Server database serves a specific purpose. Below is a detailed description of each collection and the types of data it stores.

<!-- Collection agents -->
### agents

This collection will be created after the first Bamboo Agent is connected to Bamboo Teamserver. This collection stores all information of connected Bamboo Agents and can be displayed when using the command [`display`](../../Client/commands.md#display).

|Key|Value Type|Description|Examples|
|---|----------|-----------|--------|
|agent_identifier|String|Unique, 8 characters|5zrire9a|
|hostname|String|Hostname of infected machine|bambooComA|
|publicIP|String|Public IP address of infected machine|132.99.121.23|
|privateIP|String|Private IP address of infected machine|172.168.11.69|
|priv_lvl|String|Agent starting privilege level (Low, Medium, High, System)|Medium|

#### Example

```JSON
[
    {
        "agent_identifier": "5zrire9a",
        "hostname": "bambooComA",
        "publicIP": "18.136.14.9",
        "privateIP": "172.22.49.221",
        "priv_lvl": "Medium"
    },

    {
        "agent_identifier": "3tj0owfy",
        "hostname": "bambooComB",
        "publicIP": "198.250.6.31",
        "privateIP": "192.168.68.102",
        "priv_lvl": "System"
    }
]
```

#### Models and Endpoints related

The table below shows the models and Endpoints which interacts with this collection.

|Model|Endpoint|
|-----|--------|
|agents.add_agent|/agent/initial_connection/register|
|agents.show_agents|/handler_func/agent/display|
|agents.check_agent_identifier|/agent/initial_connection/register|
|agents.use_agent|/hander_func/handler/use_agent|
|agents.remove_agent|/hander_func/handler/remove_agent|

---

<!-- Collection exploits -->
### exploits

Bamboo offers multiple preloaded exploits and users should import the json file C2-Server.exploits.json for setting up.

|Key|Value Type|Description|Examples|
|---|----------|-----------|--------|
|name|String|Name of exploit|wacom.exe|
|app_version|String|App name and version|Wacom Tablet 6.3.45-1|
|LPE_start|String|Starting privilege (User/Admin)|user|
|LPE_end|String|Ending privilege (Admin/System)|system|
|uac_bypass|Boolean|If exploit requires uac_bypass|false|
|drop-to-disk|Boolean|If exploit can be drop-to-disk|true|
|inject|Boolean|If exploit can be injected|true|
|drop_file|String|If any dropping of files is required|<empty string>|

#### Example

```JSON
[
    {
        "name": "filmora.exe",
        "app_version": "Wondershare Filmora v11",
        "LPE_start": "admin",
        "LPE_end": "system",
        "uac_bypass": true,
        "drop-to-disk": true,
        "inject": true,
        "drop_file": "filmora.exe"
    },
    {
        "name": "wacom.exe",
        "app_version": "Wacom Tablet 6.3.45-1",
        "LPE_start": "user",
        "LPE_end": "system",
        "uac_bypass": false,
        "drop-to-disk": true,
        "inject": true,
        "drop_file": ""
    }
]
```

#### Models and Endpoints related

The table below shows the models and Endpoints which interacts with this collection.

|Model|Endpoint|
|-----|--------|
|exploits.view_all|/exploits/view_all|
|exploits.add_exploit|/exploits/add|
|exploits.del_exploit|/exploits/delete|
|exploits.find_one|/exploits/exist|
|exploits.modify|/exploits/modify|
|exploits.modify_gui|/exploits/modify_gui|

---

<!-- Collection heartbeats -->
### heartbeats

This collection is related to the agents collection. This contains all heartbeat related information of the agent. Bamboo Agents will send heartbeats to the Bamboo Teamserver in intervals to notify the server that they are still "alive" and running.

|Key|Value Type|Description|Examples|
|---|----------|-----------|--------|
|agent_identifier|String|Unique, 8 characters|5zrire9a|
|heartbeat|Integer|Next heartbeat in seconds|8|
|current_time|Date|Timestamp of current heartbeat|2024-07-08T17:00:36.778+00:00|
|expected_time|Date|Expected timestamp of next heartbeat|2024-07-08T17:00:44.778+00:00|
|status|String|Agent status|alive|

#### Example

```JSON
[
    {
        "agent_identifier": "5zrire9a",
        "heartbeat": 8,
        "current_time": 2024-07-08T17:00:36.778+00:00,
        "expected_time": 2024-07-08T17:00:44.778+00:00,
        "status": "alive"
    },
    {
        "agent_identifier": "3tj0owfy",
        "heartbeat": 10,
        "current_time": 2024-07-30T16:38:15.653+00:00
        "expected_time": 2024-07-30T16:38:25.653+00:00,
        "status": "dead"
    }
]
```

#### Models and Endpoints related

The table below shows the models and Endpoints which interacts with this collection.

|Model|Endpoint|
|-----|--------|
|agents.add_heartbeat|/agent/initial_connection/register, /agent/heartbeat|
|agents.get_heartbeat|/handler_func/agent/display|
|agents.status_dead|Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database|
|agents.find_dead_but_alive|Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database|
|agents.remove_agent|/hander_func/handler/remove_agent|
|agents.info_status|/handler_func/handler/info_status|
|agents.remove_inactive|Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database|
|authentication.obtain_status|/auth/check_agent_status|


---

<!-- Collection user -->
### users

Bamboo comes with one default user. For users to log in after setting up, users should import the json file C2-Server.user.json for setting up. They can then register new users using the command register.

As Bamboo is just a PoC, the password stored in the database will not be encrypted. Users can add in encryption for passwords using bcrypt. The file to edit will be /teamserver/api/authentication.py, under login to encrypt the password that the user entered to try to match, and /teamserver/api/handler_func.py, to upload encrypted password.

|Key|Value Type|Description|Examples|
|---|----------|-----------|--------|
|username|String|Username of user|bambooUser|
|password|String|Password of user|adnap|
|status|String|If the user is online or offline|online|

#### Example

```JSON
[
    {
        "username": "bambooUser",
        "password": "adnap",
        "status": "online"
    },
    {
        "username": "bambooUserTwo",
        "password": "paSswORd@111",
        "status": "offline"
    }
]
```

#### Models and Endpoints related

The table below shows the models and Endpoints which interacts with this collection.

|Model|Endpoint|
|-----|--------|
|users.view_users|/handler_func/handler/view_users|
|users.user_online|/auth/login|
|users.user_offline|/auth/logout|
|users.register_user|/handler_func/handler/register_user|
|users.delete_user|/handler_func/handler/delete_user|
|users.find_one|/handler_func/handler/register_user|
|auth.login_auth|/auth/login|