# Global Variables

This page covers global variables used in the Bamboo Client GUI. A global variable is typically used to store and share information across different parts of the application. This helps maintain consistent states or configurations that need to be accessible from multiple components.

## Global Variables - Bamboo Client GUI

|Variable|Type|Description|Usage|
|--------|----|-----------|-----|
|jwt_token|String|Stores the [JSON Web Token (JWT)](https://jwt.io/) in a global variable|Enables Bamboo Client GUI to access the JWT when needed|
|ws_process|String|Stores the WebSocket process|Enables Bamboo Client GUI to terminate the WebSocket process easily|