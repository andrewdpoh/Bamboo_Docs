# Global Variables

This page covers global variables used in the Bamboo Teamserver. A global variable is typically used to store and share information across different parts of the application. This helps maintain consistent states or configurations that need to be accessible from multiple components.

## Global Variables - Bamboo Teamserver

|Variable|Type|Description|Usage|
|--------|----|-----------|-----|
|ws_handler|Dictionary|Whenever a Bamboo Client logs in and connects via a WebSocket, the Bamboo Teamserver will record the username as the key and the WebSocket as the value|Enables the Bamboo Teamserver to broadcast messages to all connected Bamboo Clients|
|ws_agent|Dictionary|Whenever a Bamboo Agent connects via WebSocket, the Bamboo Teamserver will record its agent identifier as the key and the WebSocket as the value|Enables the Bamboo Teamserver to broadcast commands|
|agent_response|Dictionary|For the [`cmd`](../Client/commands.md#cmd) command, Bamboo Agent's response is recorded in this dictionary|Enables Bamboo Client to receive the response|
|keylog_status|Dictionary|For the [`postexp keylog`](../Client/commands.md#postexp) command, the Bamboo Teamserver will record down the status of each Bamboo Agent keylog process (start/stop)|Determines if a Bamboo Client is starting or stopping a keylog process|