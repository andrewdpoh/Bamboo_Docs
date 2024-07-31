# Overview 

This section of the document will list the functions used in the agent and global variables declared, broken down by the packages used. 

Below is the file structure of the Bamboo Agent 

```
agent
├── connect
│   ├── c2_api
│   │   ├── c2_api.go 
│   ├── websocket
|   |   ├── websocket.go
├── exploit
│   ├── embed
│   │   ├── ntqueueapcthreadex.exe
│   ├── disk-drop.go
│   ├── inject.go
├── post_exploit
│   ├── enumerate.go
│   ├── keylogger.go
│   ├── sssretrieve.go
├── agent.go
├── default-ip.txt
├── go.mod
├── go.sum
└── helper.go
```
