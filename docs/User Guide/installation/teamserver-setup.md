# Teamserver Setup

## Part 1: Downloading the Files

1. Open a terminal or command prompt on your computer.
2. Clone the repository (skip this step if you already have the code).
    ```
    git clone https://github.com/time0ut07/C2-Agent.git
    ```

3. Change directory into the folder.
    ```
        cd C2-Agent
    ```
4. Install requirements.
    ```
        pip install -r requirements.txt
    ```

## Part 2: Setting up MongoDB

**Windows**

1. Download the [MongoDB Community Server](https://www.mongodb.com/try/download/community).
2. Open MongoDB Compass and connect to the local database
3. Create a database named "C2-Server"
4. In the database, create a collection named "**user**"
5. In the user collection, select add data > import JSON or CSV file
6. Select **C2-Server.user.json** from the folder
7. Repeat steps 4 to 6 to create the collection "**exploits**" and import the data file **C2-Server.exploits.json**.

**Unix**

1. Install the [MongoDB Community Server](https://www.mongodb.com/docs/manual/administration/install-community/) according to the operating system.
2. Start the mongodb service
    ```
    sudo systemctl start mongod
    ```
3. Using the shell command `[mongosh]`(https://www.mongodb.com/docs/mongodb-shell/) to interact with mongodb
4. Create the database C2-Server if it does not exist 
    ```
    use C2-Server
    ```
5. Create a collection called "**user**"
    ```
    db.createCollection("user")
    ```
6. Import the JSON file **C2-Server.user.json** to the **user** collection with the following command:
    ```
    mongoimport --uri="mongodb://localhost:27017" --db=C2-Server --collection=user --file=C2-Server.user.json --jsonArray
    ```
7. Repeat steps 4 to 6 to create the collection "**exploits**" and import the data file **C2-Server.exploits.json**.

## Part 3: Running the Teamserver 

Run the teamserver (to listen on all interfaces) with: 
```
python teamserver.py -ip 0.0.0.0
```

The Teamserver uses default command line arguments to change the port and address it listens to

|Parameter|Description |
|---|------|
|`-ip <addr>`|The address of the Teamserver. Default is 127.0.0.1|
|`-p <int>`|The port which the Teamserver is running on. Default is 4444|
