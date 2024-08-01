# Miscellaneous Functions

The functions below shows all the miscellaneous functions that can be found in Bamboo Client.

## arguments

### Description

Mainly for the CLI, this function allows user to connect to Bamboo Teamserver using a different IP Address and/or ports from the default. With this function, users can add arguments when running.

```
python handler_cli.py -ip 192.168.39.7 -p 1122
python handler_cli.py --host 32.222.104.31 --port 9999
```

### Function Argument

**This function does not require any arguments**

<br>

## check_agent_status

### Description

This function acts as a 'middleman' that when called, it will call the [`auth.check_agent_status`](Command_Classes/command_auth.md#check_agent_status) command to check for the specified Bamboo Agent status. It is used in commands that requires the Bamboo Agent to be 'alive', which includes [`exp`](commands.md#exp), [`cmd`](commands.md#cmd), and [`postexp [method]`](commands.md#postexp).

### Function Argument

| Field            | Type   | Description                     |
| ---------------- | ------ | ------------------------------- |
| username         | String | Username of Bamboo Client       |
| agent_identifier | String | Bamboo Agent to query status    |
| server_ip        | String | IP Address of Bamboo Teamserver |
| jwt_token        | String | JWT                             |

### Argument Example

```
check_agent_status("bambooUser", "5zrire9a", "127.0.0.1", jwt_token)
```

<br>

## login & gui_login

<!-- LINK COMMAND -->

### Description

Both functions is used to login Bamboo Client users, but `login` is for CLI while `gui_login` is for GUI. The difference being `login` allows user input while `gui_login` does not require user input as it is in a window. Both functions calls the [`auth.authentication`](Command_Classes/command_auth.md#authentication) command.

### Function Argument

#### `login`

| Field     | Type   | Description                     |
| --------- | ------ | ------------------------------- |
| server_ip | String | IP Address of Bamboo Teamserver |

#### `gui_login`

| Field     | Type   | Description                     |
| --------- | ------ | ------------------------------- |
| username  | String | Username that user input        |
| password  | String | Password that user input        |
| server_ip | String | IP Address of Bamboo Teamserver |

### Argument Example

#### `login`

```
login("127.0.0.1")
```

#### `gui_login`

```
gui_login("bambooUser", "adnap", "127.0.0.1")
```

<br>

## TeamChatReaderWriter

### Description

TeamChatReaderWriter is a class that enables the command [`chat`](commands.md#chat) in the CLI. This class is not needed for Bamboo Client GUI.

#### Brief Breakdown

Bamboo Client user will run the `run_chat` function within to start the teamchat function. The teamchat function will run another function `reading_teamchat` in another process and will have an infinite `while` loop until the user `exit`. `reading_teamchat` is a function within the class that will read the new chat messages in the file and if there are new messages using the `read_new_message` function, it will be printed out for the user in real time. Users will also be able to send messages in the teamchat function using the function `teamchat` within the class, that will send the user's message to Bamboo Teamserver that will be broadcasted to all Bamboo Clients connected.

### Function Argument

| Field     | Type   | Description              |
| --------- | ------ | ------------------------ |
| username  | String | Username that user input |
| jwt_token | String | JWT                      |

### Argument Example

```
run_chat("bambooUser", jwt_token)
```

<br>

## timestamp

### Description

Widely used in Bamboo Client that helps generate timestamp of command input.

### Function Argument

**This function does not require any arguments**

<br>

## websock_conn and server_msg

These functions are the core components for WebSocket communicates between Bamboo Client and Bamboo Teamserver.

### Description - websock_conn

websock_conn is called when a Bamboo Client is starting up. After the Bamboo Client log ins successfully, this function will help the Bamboo Client to connect to the Bamboo Teamserver WebSocket connection to receive real time updates.

### Function Argument - websock_conn

| Field    | Type   | Description              |
| -------- | ------ | ------------------------ |
| username | String | Username that user input |

### Argument Example - websock_conn

```
websock_conn("bambooUser")
```

### Description - server_msg

As another core component of the WebSocket, this function enables Bamboo Client to receive and print out the messages to Bamboo Client users in real time. There are a total of 5 message type that the Bamboo Teamserver can send.

| Message Type | Description                                                   | Example                                                                                               |
| ------------ | ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| serverMsg    | General server message                                        | When a new Bamboo Agent is registered, all Bamboo Clients will be notified in real time               |
| chatMsg      | For teamchat function                                         | Teamchat messages from other Bamboo Client will be received and be appended into the message file     |
| keylogMsg    | For command [`postexp keylog`](commands.md#postexp) results   | Bamboo Client will generate a file for the keylogging results and put it in the keylog folder         |
| enumerateMsg | For [command `enum`](commands.md#enum) results                | Bamboo Client will generate a file for the enumeration results and put it in the enum folder          |
| retrieveMsg  | For [command `postexp retrieve`](commands.md#postexp) results | Bamboo Client will generate a folder for the registry hive files and put it under the retrieve folder |

### Function Argument

| Field   | Type       | Description                               |
| ------- | ---------- | ----------------------------------------- |
| ws      | Object     | WebSocket connection                      |
| message | Dictionary | Contains the message type and the message |

### Argument Example

```
server_msg(ws,
    {
        "chatMsg": "bambooUser: Hello"
    })
```

<br>

## open_files

### Description

This file contains 3 functions, `open_keylog`, `open_enum`, and `open_retrieve`. These functions allow the dropdown menu of the GUI to open the respective folder when clicked.

### Function Argument

**This function does not require any arguments**

## start\_\*

### Description

`start_*` are a list of files that contains a class or a function. Each file is a crucial component of the GUI as it contains the pop up windows for certain commands and the logic for each.

| File           | Class\Function | Command                  | Description                                                                                      |
| -------------- | -------------- | ------------------------ | ------------------------------------------------------------------------------------------------ |
| run_add        | start_add      | [`add`](GUI/widgets.md#add)/dropdown menu      | Allows Bamboo Client user to configure and add a new exploit into the database and server        |
| run_exploit    | start_exploit  | [`exploit`](GUI/widgets.md#exploit)                | Allows Bamboo Client user to configure exploits and sent it over to Bamboo Teamserver to proceed |
| run_homescreen | run_homescreen | Null                     | Runs the homescreen for GUI on start up                                                          |
| run_login      | run_login      | Null                     | Runs the connection and login window for GUI for connection and authorisation                    |
| run_modify     | start_modify   | [`modify`](GUI/widgets.md#modify)/dropdown menu   | Allows Bamboo Client user to modify an exploit in Bamboo Teamserver                              |
| run_register   | register_user  | [`register`](GUI/widgets.md#register)/dropdown menu | Allows Bamboo Client user to register a new set of credentials                                   |
