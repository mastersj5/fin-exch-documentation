# Knowledge base for Financial Exchange 

# Table of Contents
1. [Setup Guides](#setup-guides)
2. [Microservices](#microservices)
    1. [Client Exchange](#client-exchange-client-exchange-mcs)
    2. [Matching Engine](#matching-engine-matching-engine-mcs)
    3. [Data Warehouse](#data-warehouse-data-warehouse-mcs)
    4. [Event Stream Sequencer](#event-stream-sequencer-event-stream-sequencer-mcs)
    5. [Start of Day Loader](#start-of-day-loader-start-of-day-loader-mcs)
    6. [Event Logger](#event-logger-event-logger-mcs)
    7. [Common Microservice Functionalities](#common-microservice-functionality)
3. [Resources](#resources)
    1. [Frontend](#resources)
        1. [React](#react) 
        2. [Figma](#figma)
        3. [Sass](#sass)
        4. [Chart.js](#chartjs)
        5. [Postman](#postman)
        6. [Miscellaneous](#frontend-misc)
    2. [Backend](#backend)
        1. [Docker](#docker)
        2. [Java](#java)
        3. [MongoDB](#mongodb)
        2. [Spring](#spring)
        3. [Serialization](#serialization)
        4. [Miscellaneous](#backend-misc)
    3. [Documentation](#documentation)
        1. [Mermaid](#mermaid)
        2. [PlantUML](#plantuml)
        3. [Draw.IO](#drawio)
    4. [FAQ](#faq)

## Setup Guides

1. [Kafka Java setup](guides/kafka_java_setup.md)
2. [React Getting Started](guides/react_getting_started.md)
3. [React](guides/react.md)
4. [Kafka Quickstart Guide](guides/kafka_setup_locally.md)
5. [Post-Sprint 2 Catchup Guide](guides/spr2catchupguide.md)

## Microservices
Overview of functionality/purpose of each Microservice for the Iceberg Financial Exchange.

##### <u>Security Note:</u> Commands are private and Events are public across all microservices.

### Client Exchange (```client-exchange-mcs```)
#### Purpose: Manages interactions between clients and the exchange.
#### Key Functionalities: Handles registration, order placement and modification, retrieves aggregate data, authenticates clients.

### Matching Engine (```matching-engine-mcs```)
#### Purpose: Facilitates trades by matching buyers and sellers, ensuring market liquidity.
#### Key Functionalities: Maintains order books, processes order events, executes trades based on priority.

### Data Warehouse (```data-warehouse-mcs```)
#### Purpose: Synchronizes system aggregate data by retrieving updates via Kafka event channel
#### Key Functionalities: Listens for Kafka events, updates aggregate data on MongoDB

### Event Stream Sequencer (```event-stream-sequencer-mcs```)
#### Purpose: Coordinates the exchange's command and event flow, ensuring system-wide consistency.
#### Key Functionalities: Listens for commands, generates and broadcasts events, validates orders.

### Start of Day Loader (```start-of-day-loader-mcs```)
#### Purpose: Initializes the system with necessary static data for daily trading operations.
#### Key Functionalities: Retrieves data from MongoDB, creates command headers, sends commands sequentially to Kafka channel.

### Event Logger (```event-logger-mcs```)
#### Purpose: Records system events in a human-readable log file.
#### Key Functionalities: Subscribes to the Kafka Event Channel, formats event data, appends to log file.

### <u>Common Microservice Functionality</u>

#### **Serialization:** Converting data objects into formats (like JSON or XML) suitable for transmission over the network or for storage. This is crucial for communication between microservices and persistence. For our purposes we chose byte serialization
#### **Local databases:** For longer-term persistence (e.g., embedded database like SQLite, or a full-fledged database if the microservice's scope demands it).
### <u>Subscribing to Kafka Event Channels:</u>
#### **Kafka Event Channel:** In Kafka, an event channel is often referred to as a "topic." It's a named stream of related events. Microservices can subscribe to specific topics to receive real-time updates for asynchronous communication.

## Resources 

### Frontend:
#### <u>React</u> --
- **Purpose:** A powerful JavaScript library for building dynamic user interfaces. It focuses on creating reusable components for efficient and modular web development.
- **When to Use:** Building complex, interactive web applications where performance and maintainability are crucial.

Links:  
🞄 [React: Quick Start](https://react.dev/learn)  
🞄 [React in 100 Seconds (Video)](https://www.youtube.com/watch?v=Tn6-PIqc4UM&list=PL0vfts4VzfNgUUEtEjxDVfh4iocVR3qIb)

#### <u>Figma</u> --
- **Purpose:** Collaborative, web-based design tool used primarily for user interface (UI) and user experience (UX) design.
- **When to Use:** Designing user interfaces, websites, mobile apps, presentations, and other visual assets requiring team collaboration.

Links:  
🞄 [Figma: Getting Started](https://help.figma.com/hc/en-us/categories/360002051613-Get-started)  
🞄 [Intro to Figma - Beginners guide to Figma Basics (Video)](https://www.youtube.com/watch?v=jk1T0CdLxwU)  
🞄 [Prototype Orders Data (2/28/24)](https://www.figma.com/proto/w045PRvmR0I0w0aebGUzqL/Full-Prototype-WIP?type=design&node-id=29-58&t=kQhH8HUV0DiNZ24H-1&scaling=contain&page-id=29%3A57)  
🞄 [Dropdown Menu (Video)](https://www.youtube.com/watch?v=uI3k9Ol-Mp4)  
🞄 [Functional Dropdown Menu Prototype (Video)](https://www.youtube.com/watch?v=UD6RCsO-Gtk)  

#### <u>Sass</u> --
- **Purpose:** A CSS preprocessor, extending CSS with features that improve maintainability and code organization.
- **When to Use:** When you want to write cleaner, more organized, and maintainable CSS, especially for larger projects.

Links:  
🞄 [Sass Basics](https://sass-lang.com/guide/)  
🞄 [Sass in 100 Seconds (Video)](https://www.youtube.com/watch?v=akDIJa0AP5c)

#### <u>Chart.js</u> --
- **Purpose:** An open-source JavaScript library used to create beautiful and customizable charts and graphs in web applications.
- **When to Use:** 
Projects requiring you to visually represent data in a clear and user-friendly manner.

Links:   
🞄 [Chart.js (Overview)](https://www.chartjs.org/)  
🞄 [Chart.js: Getting Started](https://www.chartjs.org/docs/latest/getting-started/)

#### <u>Postman</u>
- **Purpose:** A popular API development and testing platform. Streamlines the process of interacting with REST APIs, SOAP APIs, and GraphQL APIs.
- **When to Use:** For developing, testing, documenting, and consuming APIs in your applications.

Link(s):  
🞄 [Postman](https://www.postman.com/product/what-is-postman/)

#### <u>Frontend Misc.</u> --
1. [Coolers.co Color Palettes](https://coolors.co/dde392-afbe8f-7d8570-646f58-504b3a)
2. [Website Design Color Theory](https://www.flux-academy.com/blog/how-to-strategically-use-color-in-website-design)
3. [Dark Theme Material Design](https://m2.material.io/design/color/dark-theme.html)
4. [Principle of Scale in Design (Video)](https://www.microsoft.com/en-us/microsoft-365-life-hacks/presentations/scale-in-graphic-design#:~:text=Scale%20refers%20to%20the%20relative,important%20element%20to%20focus%20on)



### Backend:
#### <u>Docker</u> --
- **Purpose:** A platform to package applications and their dependencies into lightweight, portable containers. This streamlines development, deployment, and scaling across various environments.
- **When to Use:** 
    - Simplifying application deployment.  
    - Isolating applications from one another to prevent conflicts.  
    - Scaling applications easily by replicating containers.  
    - Creating and using microservices architectures.

**Reference Document**: [<u>Dockerization Document</u>](./dockerization.md)

Links:  
🞄 [Docker Getting Started](https://docs.docker.com/compose/gettingstarted/)  
🞄 [Scaling w/Docker: Beginner's Guide](https://www.appsdeveloperblog.com/scaling-with-docker-compose-a-beginners-guide/)  
🞄 [Docker-Kafka Connection](https://hub.docker.com/r/ubuntu/kafka)   
🞄 [Dockerizing a Spring Application](https://www.baeldung.com/dockerizing-spring-boot-application)

#### <u>Java</u> --
- **Purpose:** A versatile, general-purpose programming language known for its platform independence ("Write once, run anywhere"). Java is object-oriented, robust, and widely used for building a variety of applications.
- **When to Use:** 
    - Building enterprise-scale web applications.
    - Creating server-side applications.
    - Working with big data technologies.
    - Implementing microservices.

Links:  
🞄 [Java (Oracle)]( https://www.oracle.com/java/)  
🞄 [Learn Java (tutorialspoint)](https://www.tutorialspoint.com/java/index.htm)   

#### <u>MongoDB</u> --
- **Purpose:** A NoSQL document database that stores data in flexible JSON-like structures. MongoDB is known for its scalability, high performance, and ease of use in modern applications.
- **When to Use:**  
    - Managing large volumes of semi-structured or unstructured data.
    - Building applications that require rapid development and flexible schemas.
    - Storing data with dynamic or evolving structures.
    - Scaling applications horizontally. 

Links:  
🞄 [MongoDB Website](https://www.mongodb.com/)  
🞄 [MongoDB Getting Started](https://docs.mongodb.com/manual/tutorial/getting-started/)  
🞄 [MongoDB University](https://university.mongodb.com/)  

#### <u>Spring</u> --
- **Purpose:** A popular Java framework providing comprehensive support for building enterprise-grade web applications. It simplifies common tasks and promotes best practices.
- **When to Use:** When building scalable, robust, and maintainable Java web applications, including REST APIs.

Links:  
🞄 [Spring Website](https://spring.io)   
🞄 [Spring Guides](https://spring.io/guides)  
🞄 [Spring for Apache Kafka](https://spring.io/projects/spring-kafka)  
🞄 [Spring Boot](https://spring.io/projects/spring-boot)  
🞄 [Spring Boot: Get Started](https://spring.io/projects/spring-boot#learn)

#### <u>Serialization</u> --
- **Purpose:** The process of converting a data object (in memory) into a format suitable for storage (like a file) or transmission (over a network). The reverse process (deserialization) reconstructs the object back into memory.
- **When to Use:** 
    - Saving application data to be used in later sessions
    - Sending data between different parts of a distributed system
    - Caching objects to avoid re-creating them

**Reference Document**: [<u>Serialization Document</u>](./serialization.md)

Links:  
🞄 [Java - Serialization](https://www.tutorialspoint.com/java/java_serialization.htm)  
🞄 [Serial Version UID](https://www.baeldung.com/java-serial-version-uid#:~:text=Simply%20put%2C%20we%20use%20the,classes%20to%20have%20unique%20values)  
🞄 [Serialization and Deserialization in Java with Example](https://www.geeksforgeeks.org/serialization-in-java/)

#### <u>Backend Misc.</u> --
1. [Refactoring Design Patterns](https://refactoring.guru/design-patterns/command)

### Documentation:

#### <u>Mermaid</u> --
- **Purpose:** A text-based diagramming tool. It allows you to create charts and diagrams (flowcharts, sequence diagrams, Gantt charts, etc.) by writing simple text descriptions.
- **When to Use:** When you need to create clear and concise diagrams within documentation, code repositories, or collaborative notes.

Links:  
🞄 [Mermaid](https://mermaid.js.org)  
🞄 [Mermaid: Tutorial](https://mermaid.js.org/ecosystem/tutorials.html)

#### <u>PlantUML</u> --
- **Purpose:** Similar to Mermaid, PlantUML lets you create diagrams using a dedicated text-based language. It focuses on UML diagrams (class diagrams, sequence diagrams, etc.), as well as several other diagram types.
- **When to Use:** Primarily for software engineers or architects who need to model system components, interactions, and class structures.

Links:  
🞄 [PlantUML](https://plantuml.com)  
🞄 [PlantUML: Getting Started](https://plantuml.com/starting)  
🞄 [PlantUML VSCode Documentation](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)  
🞄 [PlantUML in VSCode (Video)](https://www.youtube.com/watch?v=xkwJ9GwgZJU)

#### <u>Draw.io</u> --
- **Purpose:** A versatile, web-based diagramming tool with a drag-and-drop interface. It offers a wide range of shapes and templates for various diagrams, not limited to technical ones.
- **When to Use:** Great for general-purpose diagrams, process flows, mind maps, mockups, and any project requiring a visual representation.

Links:  
🞄 [Draw.io App](draw.io)  
🞄 [Draw.io Tutorials](https://drawio-app.com/tutorials/)


## FAQ 

1. [Spring vs. Springboot](https://www.baeldung.com/spring-vs-spring-boot)
2. [Difference Between Kafka and Websockets or Socket.io](https://www.reddit.com/r/apachekafka/comments/u4d6mu/what_is_difference_between_kafka_and_websockets/)
3. [Command for Multiple Repository Git Pull](https://dev.to/rmpato/git-pull-multiple-repositories-at-once-4l68)

### Event Sourcing with CQRS (Command Query Response)

In short, commands are requests to affect the state of an object. Commands may be rejected.
Events are the results of those requests. This pattern creates an immutable stream of state
changes that when taken in aggregate gives you the current state of an object.

It’s perfect in the following circumstances:

- You need a detailed, ordered, immutable history of all “events” within a system.
- You need to be able to deterministically reproduce the state of a system at any given point in
time
- Many to Many - You have multiple writers to the same object
- Many to Many - You have a large number of readers that may produce different views of the
data

You need redundancy without sacrificing speed

- When you need to scale horizontally
- When you need to distribute distribute work across processes

This makes it a perfect fit for an exchange.
Here are some resources that will help.


[Event Sourcing and CQRS Explained | When should you use them? (Youtube)](https://www.youtube.com/watch?v=p0wimdpCNGk)

[CQRS pattern/arctiecture](https://learn.microsoft.com/en-us/azure/architecture/patterns/cqrs)

[Event sourcing pattern/arctiecture](https://learn.microsoft.com/en-us/azure/architecture/patterns/event-sourcing)

[Event sourcing, CQRS, stream processing and Apache Kafka: What’s the connection?](https://www.confluent.io/blog/event-sourcing-cqrs-stream-processing-apache-kafka-whats-connection/)

[CQRS and Event Sourcing in Java](https://www.baeldung.com/cqrs-event-sourcing-java)

[CQRS & Event Sourcing: Sounds cool, but is it worth it?](https://medium.com/@dorinbaba/cqrs-event-sourcing-sounds-cool-but-is-it-worth-it-e97bd5bfb7c1)
