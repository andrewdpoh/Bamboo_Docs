# Overview

This section of the document includes information pertaining to the Bamboo Teamserver.  

Below is the file structure of the Bamboo Teamserver.

```
teamserver
├── api
│   ├── agent.py
│   ├── authentication.py
│   ├── exploit.py
│   ├── handler_func.py
│   └── postexp.py
├── certs
│   ├── cert.pem
│   └── key.pem
├── database
│   ├── models
│   │   ├── agent.py
│   │   ├── auth.py
│   │   ├── exploit.py
│   │   └── users.py
│   └── db.py
├── exploits
│   ├── barracudadrive.exe
│   ├── clfs.exe
│   ├── drfone.exe
│   ├── edrblocker.exe
│   ├── filmora.exe
│   └── wacom.exe
├── func
│   ├── agent_identifier_gen.py
│   ├── arg.py
│   ├── datetime.py
│   ├── initialise_db.py
│   └── update_agentDB.py
├── shellcode
│   ├── payload.bin
│   └── payload.txt
├── uac_bypass
│   └── uac_bypass.exe
├── ws
│   └── websocket.py
├── global_vars.py
└── teamserver.py
```