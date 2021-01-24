## Easy Living - A system integration exam project
##### Made by Alex Langhoff aka Janudanie

### What is this project?
Easy Living is a Internet of Things project based on a microservice architecture.

It lets the user set up different IoT devices that can control anything.
In this first release it will have the ability to take signals from a PIR sensor and start a relay based on this.

[A small video presentation of the project](https://www.youtube.com/watch?v=bzZf3gNJx3g)

#### Constraints
This will as stated a minimal prototype, so the first version will only support a few sensors and a relay to make a proff of concept.

### Monolithic - The old app
This project is based on an old monolithic app with two parts.

Part one:
A server, that handlede everything. It had every thing build up in Lists and had every IoT device or unit loaded as a class, so it was not stateless and could not be scaled, it was also beginning to become too big and was starting to become very hard and time consuming to make any changes to it. If this server broke down, the service would stop.

[The old App](https://github.com/Janudanie/EasyLivingOldMonolithic)

Part two:
IoT devices running the same firmware, which was identified by their mac address. They had no logic themself, and only reacted to messages from the server mentioned in part 1.

[The old NodeMCU](https://github.com/Janudanie/EasyLivingOldNodeMCU)

### Microservices - The new app
Making as the new app will be made using the microservice arcitekture, it will consists of many, small app, each tending to a small portion of the combined software. The main benifit of this is that it gonna be easier to scale the individual microservice if it is becomming a bottle neck. Another advantage is that a single service can be easly updated.

The app consists of the following:

* Rest Frontend - Handles Client request
        
        This microservice adds a rest api that give the option to interact with the system

* CLI Frontend - Handles Client request

        This give a command line interface to interact with the system
* Backup service - Handles Frontend request, save the committed changes to the database
        
        This takes the request from the frontends and process them, either saving or retriving from the database.
        Send configuration changes to the Configurator to handle.
* Configurator - Handles the configuring of the IoT devices

        Get the configurations and pushes them out into the IoT network
* Logging service - Handles all logs

        Handles all the logs
* DTO
        A contract containing the object used in the system, so all components of the system has the same objects.

#### Business Process Model and Notation
There are a few business processes in the program. The model is the same for every sensor or relay, so only one business process is made for all the different units.
This project in itself will be able to let a user create their own business process models and can automate those processes.

##### BPMN for creating a new unit
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/BPMN/Create%20a%20new%20unit.png "Create a new unit")


##### BPMN for changing a new unit
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/BPMN/Update%20a%20unit.png "Update a unit")

##### PBMN for deleting a unit
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/BPMN/Delete%20a%20Unit.png "Update a unit")



#### Overview of the architecture
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/Architecture/Architecture.png "Easy Living architecture")


##### MongoDB
For chosing the database to be used, there where a few that came up. 

Hbase:
    Hbase was discarded because of you dont choose Hbase unless you have huge amounts of data. As there is not a huge data collection involved in this project, going with Hbase would not have been a viable choise.

Postgresql:
    Using PostgreSql for this project would have worked nicely if the data to be stored would have been converted, but other databases would be able to store the data without a major converting.

Neo4J:
    Neo4J is more of a graph database, would not have maded much sense. But would definitely make sense, if a future project would add a map of the area the system is installed in.

MongoDb:
    MongoDb was found to the best suited database. The reason for this choise was that MongoDb takes Json and store, and all the messages between systems are Json, it would easly store and retrieve these messages.

##### Messages broker
For chosing the message broker one criteria was used, which was easiest to integrate with MQTT that is used for the IoT network.

There where two viable choices found, spend roughly 30 minutes on each, trying to figure out how easy MQTT would be.

Kafka:
    First started looking at Kafka, there seemed to be no internal mechanism to use MQTT. Searching on google turned up a few 3rd party software that would make a proxy between Kafka and MQTT. 30 minutes passed and the result, use a third party proxy, or make one myself(Might try and do that in another procject).

RabbitMQ:
    The first search lead to RabbitMQ's page, with a detailed guide on how to setup MQTT inside RabbitMQ as a plugin. Within the 30 minutes, RabbitMQ was up and running, and could veryfi it with Paho(a MQTT client).
    Seeing how easy this was, RabbitMQ was choosen for this project

##### SpringBoot
Our instructor has show us Springboot, to learn more about this, i have tried using springboot. A very powerfull framework to really speed up the process of making applications (Once you learn how to use it)

#### Deployment
As this system is gonna be used in my home, i had to have a development environment, that can later be the production environment. This rules out my computer as a local environment.


The project is deployed on a QNAP TS 251+ that has the ability to deploy containers. 

#### Links to the Codebases

##### Microservices
[Backup](https://github.com/Janudanie/EasyLivingBackup)

[Logger](https://github.com/Janudanie/EasyLivingLogger)

[Configurator](https://github.com/Janudanie/EasyLivingLogger)

##### Frontends
[CLI-Frontend](https://github.com/Janudanie/EasyLivingCLIFrontend)

[REST-Frontend](https://github.com/Janudanie/EasyLivingCLIFrontend)

##### Contract
[Easy Living DTO](https://github.com/Janudanie/EasyLivingDTO)

#### future work
Add more Unit - some form of a doorbell would be proberbly be in the next major update
Add a mobile as a virtuel controller that could give a sound when the doorbell is pressed.

Move the system from a prototype to a real system.
