# agent/connect/c2_api

The package that exports functions used to interact with the Teamserver via HTTP APIs

## C2 Connection Functions

### C2_http

Make a request to the Teamserver's HTTP APIs

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|url|string|Address of the server in format ip:port|
|endpoint|string|The resource to connect to on the Teamserver|
|method|string|The HTTP RESTful method to use (GET, POST)|
|message|any|Map of body to send to Teamserver|

**Return**

|Type|Description|
|----|-----------|
|map[string]any|Server response|
|error|Error from request if any|

### GetFile

Download file from Teamserver (at /agent/download/&lt;filename&gt;)

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|url|string|Address of the server in format ip:port|
|filename|string|Name of file to download|

**Return**

|Type|Description|
|----|-----------|
|[]byte|File in bytes slice|
|error|Error from request if any|


## Data Parsing Functions

These functions are not exported but rather used by C2_http to handle the request and response body. 

### dataToHttpBody

Convert from map variable into io.Reader that can be used with the http package

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|data|any|Map of body to convert to send|


**Return**

|Type|Description|
|----|-----------|
|io.Reader|Reader interface to be used by http|
|error|Error from request if any|

### httpBodyToData

Download file from Teamserver (at /agent/download/&lt;filename&gt;)

**Parameters**

|Parameter|Type|Description|
|-----|----|-----------|
|http_body|io.ReadCloser|Reader returned by http response|


**Return**

|Type|Description|
|----|-----------|
|map[string]any|Map response data|
|error|Error from request if any|
