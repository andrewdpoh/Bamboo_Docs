
This section of the document includes information pertaining to the Bamboo Client. Note that the Client is referenced as "the handler" in the source code.

Below is the file structure of the Bamboo Client.


```
handler
├── commands
│   ├── auth.py
│   ├── cmd.py
│   ├── exploit.py
│   └── handler_func.py
├── func
│   ├── argument.py
│   ├── check_agent_status.py
│   ├── login.py
│   ├── teamchat.py
│   ├── timestamp
│   └── ws.py
├── gui
│   ├── commands
│   │   ├── agent.py
│   │   ├── exploit.py
│   │   ├── general.py
│   │   ├── postexp.py
│   │   └── user.py
│   ├── func
│   │   ├── add_tab.py
│   │   ├── open_files.py
│   │   ├── resize.py
│   │   ├── run_add.py
│   │   ├── run_exploit.py
│   │   ├── run_homescreen.py
│   │   ├── run_login.py
│   │   ├── run_modify.py
│   │   └── run_register.py
│   ├── img
│   │   ├── app_icon.ico
│   │   ├── app_icon.png
│   │   ├── bamboo_home.png
│   │   ├── bamboo_home2.png
│   │   ├── bamboo_icon.png
│   │   ├── bamboo_icon2.png
│   │   └── bamboo_logo.png
│   ├── widgets
│   │   ├── center_window.py
│   │   ├── console.py
│   │   ├── displayFrame.py
│   │   ├── menu.py
│   │   ├── tabs.py
│   │   ├── teamchat.py
│   │   └── ws_textBox.py
│   └── info.txt
├── postexp
│   ├── enumerate
│   ├── keylog
│   └── retrieve
├── global_vars.py
├── handler_cli.py
├── handler_gui.py
├── homescreen.py
├── login.py
└── teamchat.txt
```