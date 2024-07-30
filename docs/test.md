# test

## Overview

The Bamboo Teamserver's APIs are used by the Client and Agent to access various functionalities of the teamserver and communicate with one another.

### Base URL

```
https://[teamserver_ip]:[port]
```
For example, if your teamserver is hosted locally on port 4000, your base URL would be

```
https://127.0.0.1:4000
```
### Authorization

Authentication and authorization is required for requests to these APIs unless otherwise stated. This is handled using JWT Tokens.

```
{Provide an example request with JWT Token authentication.}
```

### HTTP status codes

The {product} APIs use the following standard HTTP response codes:

| Status code | Message           | Description   |
| ----------- | ----------------- | ------------- |
| `200 OK`    | Request succeeds. | {description} |
|             |                   |               |
|             |                   |               |

### Errors

{This section is optional.}

The {product} APIs use the following error types:

| Error                                   | Description      |
| --------------------------------------- | ---------------- |
| [{ExampleErrorType}](#exampleerrortype) | {Failure in ...} |
|                                         |                  |
|                                         |                  |

#### ExampleErrorType

| Field          | Type     | Description                                                          |
| -------------- | -------- | -------------------------------------------------------------------- |
| {errorType}    | {enum}   | {Predefined error codes. Possible enum values are x, y, ..., and z.} |
| {errorMessage} | {string} | {Additional information about why the error occurs.}                 |


## {Endpoint name}

{Provide a one-line description of what the API does. Starts with a verb in the indicative mood. For example, "Retrieves a user by `userID`".}

### Endpoint

```
{METHOD} /{request-url}/{{path-parameter}}
```

### Description

{Explain what the endpoint does.}


### Authorization

The [{authorization method}](#authorization) is required for each API request.


### Request schema

#### Path parameters

{This section is optional.}

| Path parameter | Type   | Required? | Description                 |
| -------------- | ------ | --------- | --------------------------- |
| {id}           | string | Required  | {Unique identifier of user} |
|                |        |           |                             |

#### Query parameters

{This section is optional.}

| Query parameter | Type | Required? | Description                                                                       |
| --------------- | ---- | --------- | --------------------------------------------------------------------------------- |
| {pageSize}      | int  | Optional  | {The number of items to be returned in a single request. The default value is N.} |
|                 |      |           |                                                                                   |

#### Header parameters

{This section is optional.}

| Header parameter | Type   | Required? | Description                                      |
| ---------------- | ------ | --------- | ------------------------------------------------ |
| {Content-Type}   | string | Required  | {Media type of the resource. Must be an object.} |
|                  |        |           |                                                  |

#### Request body

{This section is optional.}

| Field  | Type   | Required? | Description                     |
| ------ | ------ | --------- | ------------------------------- |
| {id}   | string | Required  | {Unique identifier of the user} |
| {name} | string | Optional  | {Name of the user}              |

### Request example

```
{Provide an example of the API request, filled with sample values.}
```

### Response schema

| Status code | Schema                                  | Description                                                                  |
| ----------- | --------------------------------------- | ---------------------------------------------------------------------------- |
<!-- | `2xx`       | [{ExampleDataType}](#data-model)        | {Describe the result where the request succeeds.}                            | -->
<!-- | `4xx`       | [{ExampleErrorType}](#exampleerrortype) | {Describe the result where the request fails with the specified error code.} | -->

### Response example

```
{Provide an example of the API response, filled with sample values.}
```

---