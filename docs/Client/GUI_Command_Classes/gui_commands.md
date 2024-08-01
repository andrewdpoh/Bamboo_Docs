# GUI Commands

This is not a user guide, this is the documentation for GUI Commands. GUI Commands are a set of classes that works between the commands and the Bamboo Client GUI. As Bamboo Client GUI was built on top of Bamboo Client CLI, the GUI will invoke the functions in /handler/gui/commands first. The functions located in there will then invoke the functions in /handler/commands to request for specific APIs from the Bamboo Teamserver and will then return messages accordingly. The additional step is required to ensure that the statements are printed in the GUI itself instead of the terminal running in the background. However, there are some cases where the CLI does not require a certain action, or an entire new command needs to be created as the command is only suited for the CLI. When this happens, GUI Commands will directly call the server endpoint instead.

GUI Commands are split into 5 different classes that were grouped together according to their use cases and domains. To find out more about each command, click on the command or visit the [Commands page](../commands.md).

|Class|Description|
|-----|-----------|
|[agent_commands](#agent_commands)|Commands that involves Agents|
|[exploit_commands](#exploit_commands)|Commands that involves Exploits|
|[general_commands](#general_commands)|General commands|
|[postexp_commands](#postexp_commands)|Commands that involves Post Exploits|
|[user_commands](#user_commands)|Commands that involves Users|


## agent_commands

|Functions|GUI Command|Command Called|Arguments|
|---------|-----------|-------|---------|
|display_agent|[`display`](../commands.md#display)|handler_func.display|Null|
|use_agent|[`use [agent]`](../commands.md#use)|handler_func.use_agent|agent_identifier|
|remove_agent|[`kill [agent]`](../commands.md#kill)|handler_func.remove_agent|agent_identifier|
|stop_agent|[`stop`](../commands.md#stop)|handler_func.stop_agent|agent_in_use|
|info_status|[`info`](../commands.md#info)|handler_func.info_status|agent_in_use|
|checkStatus|[`exploit`](../commands.md#exploit), [`cmd`](../commands.md#cmd), [`postexp`](../commands.md#postexp)|func.check_agent_status|agent_in_use|
|cmd|[`cmd`](../commands.md#cmd)|commands.command_prompt|agent_identifier, cmd|

## exploit_commands

|Functions|GUI Command|Command Called|Arguments|
|---------|-----------|--------------|---------|
|display_exploit|[`exp`](../commands.md#exp)|exploits.view_exploits|Null|
|delete_exploit|[`delete [exploit]`](../commands.md#delete)|exploits.del_exploit|exploit_name|
|gather_exploits|[`modify`, `exploit`](../commands.md#modify)|Endpoint: /exploit/view_all|jwt_token|
|stop_process|[`exploit`](../commands.md#exploit)|Endpoint: /exploit/quit|agent_identifier|
|send_exploit_config|[`exploit`](../commands.md#exploit)|Endpoint: /exploit/send_config|need_donut, agent_identifier, exploit_to_use, evasion_method, app_version, uac_bypass, donut_config, donot_for|
|add_exploit|[`add`](../commands.md#add)|Endpoint: /exploit/add|exploit_path, exploit_name, app_version, LPE_start, LPE_end, uac_bypass, d2d, inj, dropfile|
|modify_exploit|[`modify`](../commands.md#modify)|Endpoint: /exploit/modify_gui|modified_exploit_name, new_name, new_app_version, new_LPE_start, new_LPE_end, new_uac_bypass, new_d2d, new_inj, new_dropfile|

## general_commands

|Functions|GUI Command|Command Called|Arguments|
|---------|-----------|--------------|---------|
|show_help|[`help`](../commands.md#help)|Null|Null|
|exiting|[`exit`/`quit`](../commands.md#exitquit)|Null|Null|
|clear|[`clear`](../commands.md#clear)|Null|Null|

## postexp_commands

|Functions|GUI Command|Command Called|Arguments|
|---------|-----------|--------------|---------|
|enum|[`enum`](../commands.md#enum)|commands.enum|agent_identifier, priv_lvl|
|postexp_gui|[`postexp [method]`](../commands.md#postexp)|commands.postexp|agent_identifier, method, priv_lvl|

## user_commands

|Functions|GUI Command|Command Called|Arguments|
|---------|-----------|--------------|---------|
|show_users|[`users`](../commands.md#users)|handler_func.view_users|Null|
|register_user|[`register`](../commands.md#register)|handler_func.register_user|new_user, new_pw|
|delete_user|[`remove [handler]`](../commands.md#remove)|handler_func.delete_user|del_username|