# Miscellaneous Functions

The functions below shows all the miscellaneous functions that can be found in Bamboo Teamserver.

## generate_unique_id

### Description

Used to generate Bamboo Agent an agent identifier. Using the library `random`, Bamboo Teamserver will generate a random 8 characters string that can consist of lowercase alphabets and numbers.

### Function Argument

**This function does not require any arguments**

<br>

## arguments

### Description

Allows user to run Bamboo Teamserver using a different IP Address and/or ports. With this function, users can add arguments when running.

```
python teamserver.py -ip 192.168.39.7 -p 1122
python teamserver.py --host 32.222.104.31 --port 9999
```

### Function Argument

**This function does not require any arguments**

<br>

## timestamp

### Description

Widely used in Bamboo Teamserver when generating printed logs with timestamp.

### Function Argument

**This function does not require any arguments**

<br>

## initialise_db

### Description

Used when Bamboo Teamserver is starting up to initialise Bamboo Teamserver. Users can edit this function before start up to change the host of MongoDB.

### Function Argument

**This function does not require any arguments**

<br>

## update_agentDB

### Description

Runs in the background of Bamboo Teamserver every 1000 seconds. This function helps to clean up the 'dead' registered Bamboo Agents. Every time it runs, it will update the status of each Bamboo Agent accordingly and if the registered Bamboo Agent is 'dead' for 100 seconds already, it will be removed from the database.

### Function Argument

**This function does not require any arguments**