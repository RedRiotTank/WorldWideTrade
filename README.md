# World Wide Trade (hito 1)

World Wide Trade is a set of software built for minecraft servers which idea is allowing players to buy and sell items regardless the game server they're in (when both of the server have this system installed).

This repository is a set of two repositories: 

- [wwtapi](https://github.com/RedRiotTank/wwtapi): This is the rest api of the application, it manages players requests and access the common server database. You can consult it if you are interested in how it is done or if you want to make any contribution/improvement, but it is not necessary to interact with it in any way for the system to work since it is already deployed in the cloud.
- [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master): This is the minecraft server plugin you have to introduce in your server (or any other fork that does the requests). This plugin will provide users a graphic interphace to buy and sell their items and allow admins to manage what players can or can't do.

## Project frameworks (hito 3)

The microservices management frameworks have been as follows:

[Spring Boot](https://spring.io/projects/spring-boot) in [wwtapi](https://github.com/RedRiotTank/wwtapi): Spring Boot is used in the Kotlin backend for its robust ecosystem, easy integration with other Spring projects, and extensive support for REST APIs. It simplifies the setup and configuration process, enabling rapid development and scalability for complex applications.

[Ktor](https://ktor.io/docs/welcome.html) in [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master): Ktor is ideal for making requests in a Minecraft plugin because it is lightweight, asynchronous, and well-suited for Kotlin. Its flexibility and minimalistic design allow seamless integration into environments with specific requirements, like plugins, while maintaining high performance.

## Branch metodology (hito 1)

Both of the repositories will always have, at least, two branches:
- Master: Will be the latest stable version of the project, ready/in production deployment.
- Develop: Development branch, where changes from new implementations and bug fixes will converge.

In addition, new branches will be opened and closed depending on the necessary issues.

## API structure (hito 3)

For the design of the REST API, we will follow the design patterns recommended by Spring Boot. This involves a modular and layered design that aims to separate controller logic, business logic, database access logic, and the mapping and modeling of entities. To achieve this, we will have:

- **[Controller](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/wwt/api/controller):** Handles incoming requests and calls the corresponding service to retrieve the required data. It will also manage possible [exceptions](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/exception) that may arise during the operation flow.

- **[Service](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/wwt/api/service):** Implements the corresponding business logic, performing the necessary data processing.

- **[Repository](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/wwt/api/repository):** Abstracts database access through an interface.

- **[Model](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/wwt/api/entity):** Models the structure of the database tables.

- **[DTOs](https://github.com/RedRiotTank/wwtapi/tree/master/src/main/kotlin/wwt/api/dto):** Represent the potential input and output objects for data exchange in the API.

## Testing (hito 2 y 3)

- Api: Will be doing unit and integration testing for code coverage and continuous integration.
- Plugin: Will be doing in game testing as integration tests since we can not do unit testing for this development.

### Task manager election (hito 2)
For task management with tests I will be using the Intellij IDEA's integrated task manager since it has native support with the testing framework the project will be using.

In addition, Intellij IDEA's task manager has a very usefull option called "coverage" which allows you to see and manage the percentage of code you have covered and see in the code as you program exactly which areas are covered and which are not.

<p align="center">
    <img width="304" alt="{179980D1-48AB-4B44-A7DF-094DE0E47C67}" src="https://github.com/user-attachments/assets/8d56f091-f3f7-4211-831b-380a8b42e737">
</p>

You can see in the photo the coverage percentage of every development. In the next photo, you can see in green covered code and in red code that haven't been covered yet or it fails (it doesn't because this development is not finished yet but it will be covered when it's finished).

<p align="center">
 <img width="473" alt="{D8936CEE-BDAF-4016-848C-ACD256323E08}" src="https://github.com/user-attachments/assets/5aed71b3-1662-422e-a4f8-9df10d6dab4d">
</p>


### Assertion library and Testing framework (hito 2)
This project won't have testing in compilation time for [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master) (since this will be running in a minecraft server, so we can just test it on game as integration test), so this will apply only for [wwtapi](https://github.com/RedRiotTank/wwtapi). The api is being built in kotlin with Spring Boot framework, which implements its own assertion library ([springframework.test](https://docs.spring.io/spring-framework/reference/testing/unit.html)), combinated with [JUnit 5](https://junit.org/junit5/docs/current/user-guide/) (JUnit + Jupiter) as testing framwork, will conform perfectly to any API REST made with Spring Boot. This testing architecture is the most common and used for Spring Boot development thanks to the great support and consistency that it has obtained over the years in the community of this framework.

Since this application is being build in Kotlin for both (api and minecraft plugin), which is based in Java, we have two popular options for compilation integration, Gradle and Maven. It is true that Gradle is newer and has better multi-project support; however, I have preferred to maintain the robustness that a well-established system like Maven provides, in which I also have more experience of use.
This way, Maven will run the tests on the project builds and will notify us if any test is failing.

### Continuous integration (hito 2)

WorldWide Trade will be maintained after its completion as an open source repository, so I have decided that the best way to perform continuous integration is through GitHub Actions, as this tool will allow users to quickly see if the business logic is working correctly.

It also has easy integration with the branching system, which will allow merging to the main branch (production branch) only if the tests are running correctly. For example in the next photo you can see how a pull request could be merged from develop to master branch because it has passed the test phase (one for pr commits and another one for merging).
<p align="center">
 <img width="535" alt="{BF4CA22F-D54C-492B-8FC3-E38E9DE9F13A}" src="https://github.com/user-attachments/assets/77439553-949e-446a-8bc0-d031e8b0e62d">
</p>

![{A044ADAA-A1D3-45C0-9BDB-4631F6DE12A7}](https://github.com/user-attachments/assets/c3861a6d-b55f-49ca-b62c-d730f3b02b8c)

You can check CI integration configuration [here](https://github.com/RedRiotTank/wwtapi/blob/master/.github/workflows/ci.yml). You can check CI status for the last master branch update [here](https://github.com/RedRiotTank/wwtapi/tree/f891709364532a5ceadde2a472253a573e7f6a96).

To review the test execution process more thoroughly, we could go into the github actions logs. 
<p align="center">
 <img width="821" alt="{052F6329-7434-4E52-8BB9-F50EA57E6D5C}" src="https://github.com/user-attachments/assets/4389852a-7aba-47d1-b2c4-7d2dec577a1b">
</p>


### Business logic testing (hito 2)
At this point, [wwtapi](https://github.com/RedRiotTank/wwtapi) already has business logic implemented and correctly tested for the action of selling objects, you can, for example, review the tests for its [controller](https://github.com/RedRiotTank/wwtapi/blob/f891709364532a5ceadde2a472253a573e7f6a96/src/test/kotlin/wwt/api/controller/ItemControllerTest.kt) or its [service](https://github.com/RedRiotTank/wwtapi/blob/f891709364532a5ceadde2a472253a573e7f6a96/src/test/kotlin/wwt/api/controller/ItemControllerTest.kt).

As you can see, the service responses are mocked in the controller and the database responses are mocked in the service. This helps maintain the unit testing principle of checking the functionality of only a specific code fragment and thus being able to abstract from other functionalities or the data source.

## Cloud Computing scalability (hito 1)
 
This project will be divided into different instances using cloud computing:
- API instance.
- Logs Instance.
- Database instance.
- n Minecraft servers instances.

We could have n minecraft servers (in the cloud or locally). These servers will have the [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master) plugin installed, the plugin will manage interactions with [wwtapi](https://github.com/RedRiotTank/wwtapi) which will be running in the cloud and linked to a database instance. Logger instance will be registering transactions or possible errors.   

## Log System (hito 3)

It doesn't make much sense to implement logs in the plugin part of this project ([wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master)) because each server will handle its logging logic in different ways, so the logs will only be placed in the API ([wwtapi](https://github.com/RedRiotTank/wwtapi)).

For this, I will log request receptions in the controllers and the objects returned by the services, as well as when exceptions are thrown.

I am using the [slf4j](https://www.slf4j.org) logging library, which allows configuring different log levels such as DEBUG, INFO, WARNING, ERROR, and CRITICAL. This makes it easy to adjust the detail of the messages logged depending on the needs of the environment, from detailed information for debugging to critical error messages.

Currently, the logs are printed to the screen to aid with debugging during development and are also written to a local file. Later on, when I have a log server in place, they will be configured to be sent via Logstash, allowing for more efficient centralized log management. You can check configuration in [logback](https://github.com/RedRiotTank/wwtapi/blob/master/src/main/resources/logback-spring.xml).

Each log will, by default, include relevant information such as the date, the location in the code where it occurs, the log type (error, info, etc.), and the corresponding message.

## Container Architecture (hito 4)
![FULL](https://github.com/user-attachments/assets/f5682304-b9bc-428d-9ddd-8dc9da74edff)


The bulk of the container architecture is built around the backend architecture, since the client side (minecraft servers) will not necessarily be under our control (we could create a minecraft server container, but I consider it inappropriate to force the client to do so).

The architecture has the different Dockerfiles differentiated, which provides scalability to the application, and the entire construction is unified in a single [compose.yml](https://github.com/RedRiotTank/wwtapi/blob/master/compose.yml) (Check it since it is completely committed to be self-explanatory). The logging system is made using an EFK stack.

The containers are the following:

- app: Since spring runs on a tomcat virtualization, I have chosen a stable image of this container, to which I pass the war execution file. [Dockerfile](https://github.com/RedRiotTank/wwtapi/blob/master/Dockerfile).

- db: For the database I have chosen a stable image of MariaDB (since it is an open source relational database), to which some environment variables and the entry of an [initialization file](https://github.com/RedRiotTank/wwtapi/blob/master/db/init.sql) are configured. [Dockerfile](https://github.com/RedRiotTank/wwtapi/blob/master/db/Dockerfile)

- Filebeat: It allows me to efficiently collect and process the logs produced by spring. The image used corresponds to a stable and compatible version of the official elastic stack. It also has a shared volume which allows you to access the spring logs. You can consult its Dockerfile and its configuration. [Dockerfile](https://github.com/RedRiotTank/wwtapi/blob/master/logs/filebeat/Dockerfile).

- ElasticSearch: It is a highly scalable search engine, which I use as a log database. For this I have used a stable and compatible version of the elastic satck.

- Kibana: It is a data visualization tool, which allows you to visualize and analyze data stored in elasticsearch in a graphical and intuitive way. I use it to view the logs.

### Github packages (hito 4)
In order to achieve greater integrity and improve version control of the application, custom container images have been created in [GitHub Packages](https://github.com/redriottank/wwtapi/pkgs/container/wwtapi) for the app, you can see how it's used on the followings dockerfiles:

- [app](https://github.com/RedRiotTank/wwtapi/blob/master/Dockerfile)
- [db](https://github.com/RedRiotTank/wwtapi/blob/master/db/Dockerfile)
- [filebeat](https://github.com/RedRiotTank/wwtapi/blob/master/logs/filebeat/Dockerfile)
- kibana (later)
- elasticsearch (later)

In addition, a [Github workflow](https://github.com/RedRiotTank/wwtapi/blob/master/.github/workflows/docker-publish.yml) has been added that will update these images when their corresponding dockerfiles are updated and will also be executed through Continuous Integration to check the correct operation of the containers applying then some basic operations that will confirm the container is up correctly.


## About this repository

Remember this repository is a modules container, you can learn more form git modules [here](https://git-scm.com/book/en/v2/Git-Tools-Submodules). This means the references on this repository won't point directly to the master submodules branch but the last master submodule branch that was updated for this repository. So I will be updating this repository pointers everytime I obtain a stable version of any of the submodules.  

Milestones and issues won't be done in this repository neither, each repository will have their own for a better separation of functionality.
