# Model Class - agents

This class contains all models related to Bamboo Agent. Bamboo Teamserver will make use of the functions within this class to find, update, add, and delete Bamboo Agents according to the needs of Bamboo Client. This class will be interacting with the [agents](../Database/collections.md#agents) collection and the [heartbeats](../Database/collections.md#heartbeats) collection

<!-- Func 1 -->

## add_agent

Add new Bamboo Agent information into the database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /agent/initial_connection/register
```

### Description

add_agent is used when a new Bamboo Agent is registered and Bamboo Teamserver wants to insert the new Bamboo Agent information into the `collection agents`

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|hostname|String|Hostname if infected machine|
|publicIP|String|Public IP address of infected machine|
|privateIP|String|Private IP address of infected machine|
|priv_lvl|String|Privilege level of Bamboo Agent|

### Arguments Example

```
add_agent("5zrire9a", "bambooMachine", "39.100.49.231", "192.168.45.7", "medium")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|insert_one|agents|Null|

### Insertion Example

```
new_agent = {
    "agent_identifier": "5zrire9a",
    "hostname": "bambooMachine",
    "publicIP": "39.100.49.231",
    "privateIP": "192.168.45.7",
    "Integrity": "Medium"
}
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Notify Bamboo Teamserver of status|

### Return Example

```JSON
{"status": "success"}
```

<!-- Func 2 -->
<br>

## show_agents

Retrieve all information of registered Bamboo Agent

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/agent/display
```

### Description

show_agents extracts all registered Bamboo Agent data from the `collection agents`. It will then loop through all the data and append them into a list, returning the list to Bamboo Teamserver.

#### Function Arguments

**Does not require any arguments**

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|agents|List of data|

### Function Return

|Type|Description|
|----|-----------|
|Nested List|All Bamboo Agent data|

### Return Example

```
data = [
    [
        "agent_identifier": "5zrire9a",
        "hostname": "bambooMachine",
        "publicIP": "39.100.49.231",
        "privateIP": "192.168.45.7",
        "Integrity": "Medium"
    ],
    [
        "agent_identifier": "ysa903nq",
        "hostname": "bambooMachine2",
        "publicIP": "84.120.93.211",
        "privateIP": "192.168.88.110",
        "Integrity": "High"
    ]
]
```


<!-- Func 3 -->
<br>

## check_agent_identifier

Determines if Bamboo Agent specified exist in the database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /agent/initial_connection/register
```

### Description

check_agent_identifier attempts to find specified agent identifier in `collection agents`, and determines if it exist in the database

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
check_agent_identifier("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|agents|Boolean (True of exist)|

### Function Return

|Type|Description|
|----|-----------|
|Boolean|If specified Bamboo Agent exist|

### Return Example

```
True
```

<!-- Func 4 -->
<br>

## add_heartbeat

Add new Bamboo Agent heartbeat information into database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /agent/initial_connection/register
POST /agent/heartbeat
```

### Description

add_heartbeat will allows Bamboo Teamserver to keep track of all Bamboo Agent status. It will be called when a new Bamboo Agent is registered or existing registered Bamboo Agent send their heartbeat. Only `collection heartbeats` will be affected.

The model will first attempt to find the Bamboo Agent using their agent identifier to determine if the Bamboo Agent is new by extracting data. It will be empty if the Bamboo Agent is new. If the Bamboo Agent is new, it will insert the data into the collection. If the Bamboo Agent already exist, it will determine if the Bamboo Agent heartbeat was "late" or not and update the existing information. It will return different values depending on it.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|
|heartbeat|String|Seconds before the next heartbeat|
|current_time|Date|Current timestamp|
|expected_time|Date|Expected timestamp to receive heartbeat (current_time + heartbeat)|
|status|String|Update it to "alive"|

### Arguments Example

```
add_heartbeat("5zrire9a", "6", "2024-07-30T16:38:15.653+00:00", "2024-07-30T16:38:21.653+00:00", "alive")
```

### Database Method

|Method|Collection|Return|Usage|
|------|----------|------|-----|
|find|heartbeats|Data of Bamboo Agent. Empty if does not exist|Determine if Bamboo Agent is new|
|insert_one|heartbeats|Null|Insert new Bamboo Agent information|
|update_many|heartbeats|True for success, False for failed|If Bamboo Agent heartbeat Bamboo Teamserver after expected_time|
|update_many|heartbeats|True for success, False for failed|Bamboo Agent heartbeat is punctual|

### Insertion Example

```
new_heartbeat = {
    "agent_identifier": "5zrire9a",
    "heartbeat": 6,
    "current_time": "2024-07-30T16:38:15.653+00:00",
    "expected_time": "2024-07-30T16:38:21.653+00:00",
    "status": "alive"
}
```

### Update Example

```JSON
{"agent_identifier": "5zrire9a"}, 
{"$set": {
    "heartbeat": 6, 
    "current_time": "2024-07-30T16:38:15.653+00:00", 
    "expected_time": "2024-07-30T16:38:21.653+00:00", 
    "status": "alive"
    }
}
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Added new heartbeat|
|Dictionary|Updated heartbeat|

### Function Example

```JSON
{"agent": "new"}
```

```JSON
{"agent": "punctual"}
```

<!-- Func 5 -->
<br>

## get_heartbeat

Retrieve Bamboo Agent status from heartbeats

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/agent/display
```

### Description

get_heartbeat objective is to extract the status of the Bamboo Agent to determine if they are "dead" or "alive" from the `collection heartbeats`. It will then loop through all the data and append only the status into a list, returning the list to Bamboo Teamserver.

#### Function Arguments

**Does not require any arguments**

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|heartbeats|List status|

### Function Return

|Type|Description|
|----|-----------|
|List|Status of all Bamboo Agent in database|

### Return Example

```
data = [
    "dead",
    "dead",
    "alive"
]
```

<!-- Func 6 -->
<br>

## status_dead

Update Bamboo Agent status to dead

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database
```

### Description

status_dead will update the specified Bamboo Agent status to dead in the `collection heartbeats`.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
status_dead("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|update_many|heartbeats|Status of update (boolean)|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Status of update|

### Return Example

```JSON
{"status": "done"}
```

<!-- Func 7 -->
<br>

## find_dead_but_alive

Extract all Bamboo Agent who are "alive"

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database
```

### Description

find_dead_but_alive will retrieve all registered Bamboo Agent status which are "alive" in the `collection heartbeats`.

#### Function Arguments

**Does not require any arguments**

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|heartbeats|List of agent identifier that match the criteria|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Contains a list of agent identifier|

### Return Example

```JSON
{"alive_agents": ["5zrire9a", "62yb10jd", "p12ls3da"]}
```

<!-- Func 8 -->
<br>

## use_agent

Extract all information of specified Bamboo Agent

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /hander_func/handler/use_agent
```

### Description

use_agent retrieve the information of the specified Bamboo Agent in `agents collection`.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
use_agent("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|agents|List information of specified Bamboo agent (agent_data)|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Contains a dictionary of agent information|
|Dictionary|None (no such agent)|

### Return Example

```JSON
{"agent_data": {
        "agent_identifier": "5zrire9a",
        "hostname": "bambooMachine",
        "publicIP": "39.100.49.231",
        "privateIP": "192.168.45.7",
        "Integrity": "Medium"
}
}
```

<!-- Func 9 -->
<br>

## remove_agent

Remove all information of specified Bamboo Agent

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /hander_func/handler/remove_agent
```

### Description

remove_agent will completely remove the specified Bamboo Agent information, from both `collection agents and heartbeats`. It will first check if the specified Bamboo Agent exist first before deleting the data.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
remove_agent("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|agents|Boolean value|
|delete_many|agents|Boolean value|
|delete_many|heartbeats|Boolean value|

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Success|
|Dictionary|Failed|

### Return Example

```JSON
{
    "status": "success"
}
```

<!-- Func 10 -->
<br>

## info_status

Retrieve and update database (if needed) of Bamboo Agent status when command [`info`](../../Client/commands.md#info) is called

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
POST /handler_func/handler/info_status
```

### Description

info_status main objective is to return the status of the specified Bamboo Agent. This model will check if the specified Bamboo Agent is "dead" by comparing the `current timestamp` with the `expected timestamp` before returning the status of the specified Bamboo Agent.

#### Function Arguments

|Field|Type|Description|
|-----|----|-----------|
|agent_identifier|String|Identifier of Bamboo Agent|

### Arguments Example

```
info_status("5zrire9a")
```

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find_one|heartbeats|List of information of specified Bamboo Agent|

### Find Return Example

```
[
    "agent_identifier": "5zrire9a",
    "heartbeat": 6,
    "current_time": "2024-07-30T16:38:15.653+00:00",
    "expected_time": "2024-07-30T16:38:21.653+00:00",
    "status": "alive"
]
```

### Function Return

|Type|Description|
|----|-----------|
|Dictionary|Notify Bamboo Teamserver on specified Bamboo Agent status|

### Return Example

```JSON
{"agent_status": "alive"}
```

<!-- Func 11 -->
<br>

## remove_inactive

Remove all "dead" registered Bamboo Agent from the database

### Usage
<!-- should link both endpoint n command to their respective pages -->
```
Automatic function in Bamboo Teamserver that cleans up Bamboo Agent in database
```

### Description

remove_inactive is used in the function that automatically remove data from the database. This model will help the function to automatically remove all "dead" Bamboo Agent from the database.

#### Function Arguments

**Does not require any arguments**

### Database Method

|Method|Collection|Return|
|------|----------|------|
|find|heartbeats|List of information of "dead" Bamboo Agents|


### Function Return

|Type|Description|
|----|-----------|
|Dictionary|List of "dead" Bamboo Agent|

### Return Example

```
[
    [   
        "agent_identifier": "5zrire9a",
        "heartbeat": 6,
        "current_time": "2024-07-30T16:38:15.653+00:00",
        "expected_time": "2024-07-30T16:38:21.653+00:00",
        "status": "dead"
    ],
    [   
        "agent_identifier": "wohw193j",
        "heartbeat": 9,
        "current_time": "2024-07-30T16:42:20.653+00:00",
        "expected_time": "2024-07-30T16:42:29.653+00:00",
        "status": "dead"
    ]
]
```