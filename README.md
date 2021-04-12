# The Tartan SmartHome Platform

This Dropwizard application is a RESTful service to control the Tartan SmartHome platform. 
It also contains the IoTController code in it.

(NOTE: if using Windows, all instances of `./gradlew` should be replaced with `gradlew.bat`).

## Requirements
- The Java JDK 1.8 needs to be installed on your system before compiling the application.
- If not running the Dockerized startup, MySQL 5.7 should be installed on the system (for the Historian DB).
- If not running the Dockerzied startup, Python 3.6+ should be installed on the system (for the House Simulator).


## Building the Code

### Building the Platform

To build the Platform code:

1. Go inside the "/Platform" folder.
1. Execute `./gradlew build` to build your code.
1. To create a standalone JAR of the Platform, execute `./gradlew shadowJar`
   1. This will create a "tartan-1.0-SNAPSHOT.jar" file inside the "/Platform/build/libs" subfolder with the Platform and all its dependencies.

### Setting Up the Historian DB

If the Dockerized statup is not being used, the database has to be manually set up. MySQL is installed differently depending
on the system. If using Ubuntu, MySQL 5.7 can usually be installed executing the following:

1. `sudo apt update`
1. `sudo apt install mysql-server`
1. `sudo mysql_secure_installation`
 
The "/Database/init.sql" script can then be executed to create the DB and user. 

## Starting the System as Components

The following instructions are used when starting each component separately.

### Starting the House Simulators
To start a House Simulator:

1. Go inside the "/HouseSimulator" folder.
1. Execute `python3 simple_server.py localhost <port>`, replacing <port> with one of the ports configured in the Platform's config.yml file.

Multiple House Simulators can be executed at the same time, as long as each one is listening on a different port. The default
config.yml file in the "/Platform" project expects two House Simulators to be running, one on port 5050 and one on port 5051. 
In order to make the Platform with the default configuration start successfully, you should start two instances of the House Simulator, one on each port.

### Starting the Platform

In order for the Platform to run properly, MySQL and the House Simulators configured in the config.yml file have to be already running on the system.

1. Go inside the "/Platform" folder.
1. To start the Platform from Gradle, simply run `./gradlew run`
1. Alternatively, to start the platform from the standalone JAR, follow these steps:
    1. Go inside the "/Platform/build/libs" folder.
    1. Execute `java -jar tartan-1.0-SNAPSHOT.jar server ../../config.yml`

## Starting the System inside Docker Containers

Instead of starting each component manually as described in the previous section, all components can be started together inside Docker containers with docker-compose. 

NOTE: In order for this to work, you first need to set up Docker and Docker-compose on your system.

NOTE: When running the Dockerized version of the Platform, the configuration file used is "/Platform/config.docker.yml", so any changes
should be made there.

1. Execute `sudo docker-compose up --build`

## Check Successful Start

To check that the Platform is running properly, open a browser and enter either `http://localhost:8080/smarthome/state/mse` or `http://localhost:8080/smarthome/state/cmu` and log in.
Log in information for each house is stored in the config.yml file.
