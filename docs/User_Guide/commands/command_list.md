# Command List

This page briefly lists all the commands that can be used in the Bamboo Client (CLI and GUI). For usage examples, see the other pages in the User Guide.

| Console Command                                | Description                                                                                                                                             |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| help                                           | Shows the help menu that list all commands and descriptions                                                                                              |
| exit/quit                                      | Exits Bamboo Client                                                                                                                                      |
| chat                                           | Opens team chat to chat/receive chat messages from other Bamboo Client users. In GUI this is the equivalent of going to the TEAMCHAT tab                 |
| clear                                          | Clears chat messages                                                                                                                                     |
| users                                          | Displays all users with their status. Accessible in GUI via Menu > Users > Display User                                                                  |
| register --username [username] --pw [password] | Registers a new user into the database. Accessible in GUI via Menu > Users > Add User                                                                    |
| remove [handler]                               | Removes handler from database. Accessible in GUI via Menu > Users > Display User and using the Delete User dropdown in the Display pane                  |
| display                                        | Displays all agent information. Accessible in GUI via Menu > Agents > Display Agents                                                                     |
| use [agent]                                    | Starts using agent                                                                                                                                       |
| kill [agent]                                   | Disconnects agent and remove from database. Accessible in GUI via Menu > Display Agents > Agents and using the Delete agent dropdown in the Display pane |
| exp                                            | Displays all exploits in database. Accessible in GUI via Menu > Exploits > Display Exploits                                                                 |
| add                                            | Adds an exploit into the database. Accessible in GUI via Menu > Exploits > Add Exploits                                                                  |
| delete [exploit]                               | Deletes an exploit from the database. Accessible in GUI via Menu > Exploits > Display Exploits and using the Delete exploit dropdown in the Display pane |
| modify [exploit]                               | Modifies an exploit from the database. Accessible in GUI via Menu > Exploits > Modify Exploits                                                               |

**Commands for when an Agent is in use**

| Console Command  | Description                                                                            |
| ---------------- | -------------------------------------------------------------------------------------- |
| stop             | Stops using the Agent (closes its tab in GUI). Not to be confused with the kill command |
| info             | Displays information of current agent                                                   |
| exploit          | Commands Agent to run exploit                                                           |
| cmd              | Runs commands in Agent                                                                  |
| enum             | Enumerates Agent machine. Also accessible in the GUI via the side buttons               |
| postexp [method] | Runs a post exploit. Also accessible in the GUI via the side buttons                    |
