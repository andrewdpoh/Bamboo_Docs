# Agent Setup

## Part 1: Building the Agent

1. If not yet installed, [install Go](https://go.dev/doc/install). 
2. Go to the agent directory and run the following command to download dependencies: 
```
go get . 
```
3. Edit default-ip.txt file to the IP address of the Teamserver 
4. In the Agent folder, build the Agent (with flags to reduce the size of the exe) with the command to get agent.exe 
```
go build  -ldflags "-s -w" 
```

## Part 2: Running the Agent

1. Transfer the agent to the Desktop folder of the user in the target host.
2. Ensure the Teamserver is running. 
3. Run the agent by either running it in a terminal or double clicking its icon

The agent has options for command line parameters, but they are typically not required.

|Parameter|Description |
|---|------|
|`-ip <addr>`|The address of the Teamserver. Default value is the string in default-ip.txt when the agent is compiled |
|`-port <int>`|The port which the Teamserver is running on. Default is 4444|
|`-skip-priv`|If this parameter is included, the Agent will not check its privilege level and user. Only used for testing purposes.|