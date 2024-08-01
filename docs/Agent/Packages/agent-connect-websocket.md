# agent/connect/websocket

The package that exports functions used to connect and communicate with the Teamserver over WebSocket

## WebSocket functions

### Send_data

Send data through a established Websocket connection

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|conn|*websocket.Conn|Pointer to Websocket connection object|
|message|map[string]any|Message to send|

**Return**

|Type|Description|
|----|-----------|
|error|Error from Websocket if any|

### Receive_data

Listen to messages from Teamserver over Websocket

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|conn|*websocket.Conn|Pointer to Websocket connection object|

**Return**

|Type|Description|
|----|-----------|
|message|map[string]any|Message from Teamserver|
|error|Error from Websocket if any|

### Init_conn

Initialize Websocket connection with the Teamserver

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|c2_url|string|Address of the server in format ip:port|
|agent_id|string|Agent identifier issued by Teamserver|

**Return**

|Type|Description|
|----|-----------|
|conn|*websocket.Conn|Pointer to Websocket connection object|
|error|Error from Websocket if any|