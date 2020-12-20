## Easy Living - A system integration exam project
Easy Living is a Internet of Things project based on a microservice architekture.

The finished result should be able to take alot of different sensor and do a task based on the readings from that sensor.
For an example, it could be a pir sensor that registeres movement and send a signal to a relay, that turns on the light in that area.

This will be a prototype with a minimal working order. But as i am gonna use this project on our old farm, this project is over time gonna be developed.

#### Constraints
This will as stated a minimal prototype, so the first version will only support a few sensors and a relay to make a proff of concept.

### Monolithic - The old app
This project is based on an old monolithic app with two parts.

Part one:
A server, that handlede everything. It had every thing build up in Lists and had every IoT device or unit loaded as a class, so it was not stateless and could not be scaled, it was also beginning to become too big and was starting to become very hard and time consuming to make any changes to it. If this server broke down, the service would stop.

Part two:
IoT devices running the same firmware, which was identified by their mac address. They had no logic themself, and only reacted to messages from the server mentioned in part 1.

### Microservices - The new app
Making as the new app will be made using the microservice arcitekture, it will consists of many, small app, each tending to a small portion of the combined software. The main benifit of this is that it gonna be easier to scale the individual microservice if it is becomming a bottle neck. Another advantage is that a single service can be easly updated.


#### Logical Data Model
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/Logical%20Data%20Model/Logical%20Data%20Model.png "Easy Living logical data model")



#### Use cases
![alt text](https://github.com/Janudanie/EasyLiving/blob/main/UseCase/Use%20cases.png "Easy Living use case")

#### Text based Use Cases
---
    UC1
    Name: Add controller

    Description:  
    A user has to add a new controller to the system

    Primary Actor: User

    Preconditions: The controller is configured and started up

    Main Scenario:

    User selects add controller.
    System shows a add controller form.
    User fills out the form.
    System adds the controller.

    Postcondition: (Success guaranties) A new controller is added.
---
    UC2
    Name: List controllers

    Description:  
    A user wants a list of all controllers in the system.

    Primary Actor: User

    Preconditions: None

    Main Scenario:

    User select lists controllers.
    System returns all controllers.

    Postcondition: (Success guaranties) A complete list of all controllers are returned.
---
    UC3
    Name: Remove controller

    Description:  
    A user has to remove a controller from the system

    Primary Actor: User

    Preconditions: None

    Main Scenario:

    User select lists controllers.
    System returns all controllers.
    User selecects remove controller.
    System removes the controller.

    Postcondition: (Success guaranties) A controller is remove.
---
    UC4
    Name: Add unit.

    Description:  
    A user wants to add a new unit to the system.

    Primary Actor: User

    Preconditions: A new unit is physical connected to a Controller that is online.

    Main Scenario:

    User selects add unit.
    System returns add new unit form.
    User fills out form.
    System returns all controllers.
    User selects controller to add unit to.
    System adds the new unit to the system.

    Postcondition: (Success guaranties) A new unit is added.
---
    UC5
    Name: List units.

    Description:  
    A user wants to see all units connected.

    Primary Actor: User

    Preconditions: None

    Main Scenario:

    User selects list units.
    System returns all units.

    Postcondition: (Success guaranties) A list of all units is returned.
---
    UC6
    Name: Change unit.

    Description:  
    A user wants to change a unit.

    Primary Actor: User

    Preconditions: None

    Main Scenario:

    User selects list units.
    System returns all units.
    User selects change unit.
    System returns the new unit form already filled out with old values.
    User fills out the form.
    System returns all controllers.
    User selects controller to add unit to.
    System changes the unit in the system.

    Postcondition: (Success guaranties) A unit is changed.
---
    UC7
    Name: Remove a unit.

    Description:  
    A user wants to remove a unit.

    Primary Actor: User

    Preconditions: None

    Main Scenario:

    User selects list units.
    System returns all units.
    User selects remove unit.
    System removes the unit.

    Postcondition: (Success guaranties) A unit is removed.
---
#### Sequence diagram.


#### Overview of the architecture

#### process and thoughts

#### future work


