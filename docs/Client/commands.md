# Commands

This is not a user guide, this is the documentation for Bamboo Client Commands. Bamboo Client offers a wide variety of commands in both CLI and GUI interface. This enables users to interact with Bamboo Teamserver, Bamboo Agent, and even other Bamboo Client users. The table below contains all the commands that Bamboo offers. The commands below are mainly for the CLI and may defer in the GUI. Use the `help` command see the difference in the GUI.

| Command                       | Description                                |
|-------------------------------|--------------------------------------------|
| [`help`](#help)               | Displays command list                      |
| [`exit`/`quit`](#exitquit)    | Exit handler                               |
| [`chat`](#chat)               | Send/Receive message in team chat          |
| [`clear`](#clear)             | Clear chat logs                            |
| [`users`](#users)             | Display all handler information            |
| [`register`](#register)       | Add in a new handler                       |
| [`remove [handler]`](#remove) | Remove handler from DB                     |
| [`display`](#display)         | Display all agent information              |
| [`use [agent]`](#use)         | Start using an agent                       |
| [`kill [agent]`](#kill)       | Remove agent from DB                       |
| [`exp`](#exp)                 | View all exploits in DB                    |
| [`add`](#add)                 | Add exploit to DB (CLI cannot upload file) |
| [`delete [exploit]`](#delete) | Remove exploit from DB                     |
| [`modify [exploit]`](#modify) | Modify exploit in DB                       |

**When Handler is Using an Agent with [`use`](#use)**

| Command                        | Description                                |
|--------------------------------|--------------------------------------------|
| [`stop`](#stop)                | Stop using agent                           |
| [`info`](#info)                | Displays information of current agent      |
| [`exploit`](#exploit)          | Run specific exploit in agent              |
| [`cmd`](#cmd)                  | Run commands in agent                      |
| [`enum`](#enum)                | Enumerate victim machine                   |
| [`postexp [method]`](#postexp) | Run post exploit                           |


---

### help

Show the help menu that lists all commands and descriptions.

| CLI Command | GUI Command | Command |
|-------------|-------------|---------|
| `help`      | `help`      | Null    |

---

### exit/quit

Exit Bamboo Client.

| CLI Command  | GUI Command  | Command    |
|--------------|--------------|------------|
| `exit/quit`  | `exit/quit`  | auth.logout|

---

### chat

Open team chat to send/receive chat messages from other Bamboo Clients.

| CLI Command | GUI Command  | Command                     |
|-------------|--------------|-----------------------------|
| `chat`      | TEAMCHAT tab | TeamChatReaderWriter.run_chat|

---

### clear

Clear chat messages.

| CLI Command | GUI Command | Command                        |
|-------------|-------------|--------------------------------|
| `clear`     | `clear`     | TeamChatReaderWriter.clearchat |

---

### users

Display all users with their status.

| CLI Command | GUI Command        | Command                |
|-------------|--------------------|------------------------|
| `users`     | `users`/dropdown menu | handler_func.view_users |

---

### register

Register a new user into the database.

| CLI Command                              | GUI Command        | Command                    |
|------------------------------------------|--------------------|----------------------------|
| `register --username [username] --pw [password]` | `register`/dropdown menu | handler_func.register_user |

---

### remove

Remove a handler from the database.

| CLI Command       | GUI Command     | Command               |
|-------------------|-----------------|-----------------------|
| `remove [handler]`| `remove [handler]` | handler_func.delete_user |

---

### display

Display all agent information.

| CLI Command | GUI Command        | Command               |
|-------------|--------------------|-----------------------|
| `display`   | `display`/dropdown menu | handler_func.display  |

---

### use

Start using an agent.

| CLI Command  | GUI Command  | Command                |
|--------------|--------------|------------------------|
| `use [agent]`| `use [agent]`| handler_func.use_agent |

---

### kill

Kill an agent and remove it from the database.

| CLI Command   | GUI Command            | Command                |
|---------------|------------------------|------------------------|
| `kill [agent]`| `kill [agent]`/dropdown menu | handler_func.remove_agent |

---

### exp

View all exploits in the database.

| CLI Command | GUI Command       | Command                   |
|-------------|-------------------|---------------------------|
| `exp`       | `exp`/dropdown menu | exploits.view_exploits     |

---

### add

Add an exploit into the database.

| CLI Command | GUI Command     | Command                |
|-------------|-----------------|------------------------|
| `add`       | `add`/dropdown menu | exploit.add_exploit    |

---

### delete

Delete an exploit from the database.

| CLI Command       | GUI Command               | Command             |
|-------------------|---------------------------|---------------------|
| `delete [exploit]`| `delete [exploit]`/dropdown menu | exploit.del_exploit  |

---

### modify

Modify an exploit in the database.

| CLI Command       | GUI Command      | Command          |
|-------------------|------------------|------------------|
| `modify [exploit]`| `modify`/dropdown menu | exploit.modify   |

**When the Client is Using an Agent with [`use`](#use)**

---

### stop

Stop using the agent.

| CLI Command | GUI Command | Command            |
|-------------|-------------|--------------------|
| `stop`      | `stop`      | handler_func.stop_agent |

---

### info

Display information of the current agent.

| CLI Command | GUI Command | Command               |
|-------------|-------------|-----------------------|
| `info`      | `info`      | handler_func.info_status |

---

### exploit

Command the agent to run an exploit.

| CLI Command | GUI Command | Command                  |
|-------------|-------------|--------------------------|
| `exploit`   | `exploit`   | commands.exploit_process |

---

### cmd

Run commands in the agent.

| CLI Command | GUI Command | Command                 |
|-------------|-------------|-------------------------|
| `cmd`       | `cmd`       | commands.command_prompt |

---

### enum

Enumerate the agent machine.

| CLI Command | GUI Command     | Command        |
|-------------|-----------------|----------------|
| `enum`      | `enum`/buttons  | commands.enum  |

---

### postexp

Run a post exploit.

| CLI Command         | GUI Command             | Command           |
|---------------------|-------------------------|-------------------|
| `postexp [method]`  | `postexp [method]`/buttons | commands.postexp  |
