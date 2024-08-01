# Command List

This page briefly lists all the commands that can be used from the Bamboo Client (CLI and GUI). For usage examples, see the other pages in the User Guide.

| Console Command                                | Description                                                                                                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| help                                           | Show the help menu that list all commands and descriptions                                                                                              |
| exit/quit                                      | Exit Bamboo Client                                                                                                                                      |
| chat                                           | Open team chat to chat/receive chat messages from other Bamboo Client users. In GUI this is the equivalent of going to the TEAMCHAT tab                 |
| clear                                          | Clear chat messages                                                                                                                                     |
| users                                          | Display all users with their status. Accessible in GUI via Menu > Users > Display User                                                                  |
| register --username [username] --pw [password] | Register a new user into the database. Accessible in GUI via Menu > Users > Add User                                                                    |
| remove [handler]                               | Remove handler from database. Accessible in GUI via Menu > Users > Display User and using the Delete User dropdown in the Display pane                  |
| display                                        | Display all agent information. Accessible in GUI via Menu > Agents > Display Agents                                                                     |
| use [agent]                                    | Start using agent                                                                                                                                       |
| kill [agent]                                   | Disconnect agent and remove from database. Accessible in GUI via Menu > Display Agents > Agents and using the Delete agent dropdown in the Display pane |
| exp                                            | View all exploits in database. Accessible in GUI via Menu > Exploits > Display Exploits                                                                 |
| add                                            | Add an exploit into the database. Accessible in GUI via Menu > Exploits > Add Exploits                                                                  |
| delete [exploit]                               | Delete an exploit from the database. Accessible in GUI via Menu > Exploits > Display Exploits and using the Delete exploit dropdown in the Display pane |
| modify [exploit]                               | Modify exploit from the database. Accessible in GUI via Menu > Exploits > Modify Exploits                                                               |

**Commands for when an Agent is in use**

| Console Command  | Description                                                                            |
| ---------------- | -------------------------------------------------------------------------------------- |
| stop             | Stop using the Agent (closes its tab in GUI). Not to be confused with the kill command |
| info             | Display information of current agent                                                   |
| exploit          | Command Agent to run exploit                                                           |
| cmd              | Run commands in Agent                                                                  |
| enum             | Enumerate Agent machine. Also accessible in the GUI via the side buttons               |
| postexp [method] | Run a post exploit. Also accessible in the GUI via the side buttons                    |
