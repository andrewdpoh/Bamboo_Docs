# agent
 
The main package for the agent 

## Global Variables

|Parameter|Type|Description|Default Value|
|-----|----|-----------|---------|
|DEFAULT_TEAMSERVER_IP|string|Default IP address to query Teamserver, declared with a go:embed directive|The value in default-ip.txt|
|TEAMSERVER_URL|string|Used to store the full address of the Teamserver, in format ip:port||
|SKIP_PRIV|bool|Used to store whether the -skip-priv parameter was used||
|keylogHandler|string|Used to store which handler started the keylogging||
|keyloggingStatus|bool|Indicate whether the keylogger is currently running or not|false|
|keystrokesChan|chan string|Used by the keylogging function to send back the keys captured||
|stopChan|chan bool|Used to send a true value to the keylogging function to return the function||

## Functions

### setGlobalVars

Used to set global variables from the command line arguments

**Parameters**

None

**Return**

None

### executeCommand

Run a command in the command prompt

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|command|string|Command to run|

**Return**

|Type|Description|
|----|-----------|
|string|Output of command|
|error|Error from command if any|

### splitCsvString

Split a line of string from a CSV formatted input and return as a slice

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|csvstr|string|CSV formatted string|

**Return**

|Type|Description|
|----|-----------|
|[]string|Slice of string|

### getPrivilgeLevel

Get the user and privilege level the agent is running as

**Parameters**

None

**Return**

|Type|Description|
|----|-----------|
|string|Integrity level|
|string|Username|

### hostInfo

Get host information such as
- hostname
- privateIP
- publicIP
- integrity
- user

**Parameters**

None

**Return**

|Type|Description|
|----|-----------|
|map[string]any|Map of host information|

### init_conn

Connect and register with the Teamserver via HTTPS API

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|host_info|map[string]any|Map of host information|

**Return**

|Type|Description|
|----|-----------|
|string|Agent identifier issued by Teamserver|

### heartbeat

An infinite loop to send the Teamserver heartbeats every 5-10 seconds. Ran in a goroutine

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|agent_identifier|string|Agent identifier issued by Teamserver|

**Return**

None

### runExploits

Switch case and logic to select how to run the exploit and executes it

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|message|map[string]any|Message sent from Teamserver|

**Return**

|Type|Description|
|----|-----------|
|error|Error from running exploit if any|

### runPostExploit

Switch case and logic to run a post exploit function or enumeration

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|message|map[string]any|Message sent from Teamserver|
|priv|string|Integrity level of agent|

**Return**

|Type|Description|
|----|-----------|
|map[string]any|Map of data to send back to the Teamserver|
|string|Teamserver URL to send result to|
|error|Error from running functions if any|

### menu

Listen for a Websocket message and carry out its command

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|ws_conn|*websocket.Conn|Pointer to Websocket connection object|
|agent_identifier|string|Agent identifier issued by Teamserver|
|priv|string|Integrity level of agent|

**Return**

None

### DoManyPrint

Prints a string many times, each ended with a carriage return (\r). Used in an attempt to evade detection. 

|Parameter|Type|Description|
|-----|----|-----------|
|text|string|The string to print|

**Return**

|Type|Description|
|----|-----------|
|int|The number 8|