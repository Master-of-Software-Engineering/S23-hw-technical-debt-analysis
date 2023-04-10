# The Tartan SmartHome Platform

This Dropwizard application is a RESTful service to control the Tartan SmartHome platform. 
It also contains the IoTController code in it.

(NOTE: if using Windows, all instances of `./gradlew` should be replaced with `gradlew.bat`).

## Requirements
- The Java JDK 1.8 needs to be installed on your system before compiling the application.
- If not running the Dockerized startup, MySQL 5.7 should be installed on the system (for the Historian DB).
- If not running the Dockerzied startup, Python 3.6+ should be installed on the system (for the House Simulator).

### Building the Platform

To build the Platform code:

1. Go inside the "/Platform" folder.
1. Execute `./gradlew build` to build your code.
1. To create a standalone JAR of the Platform, execute `./gradlew shadowJar`
   1. This will create a "tartan-1.0-SNAPSHOT.jar" file inside the "/Platform/build/libs" subfolder with the Platform and all its dependencies.

