# Word Wide Trade

World Wide Trade is a set of software built for minecraft servers which idea is allowing players to buy and sell items regardless the game server they're in (when both of the server have this system installed).

This repository is a set of two repositories: 

- [wwtapi](https://github.com/RedRiotTank/wwtapi): This is the rest api of the application, it manages players requests and access the common server database. You can consult it if you are interested in how it is done or if you want to make any contribution/improvement, but it is not necessary to interact with it in any way for the system to work since it is already deployed in the cloud.
- [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master): This is the minecraft server plugin you have to introduce in your server (or any other fork that does the requests). This plugin will provide users a graphic interphace to buy and sell their items and allow admins to manage what players can or can't do.

## Branch metodology

Both of the repositories will always have, at least, two branches:
- Master: Will be the latest stable version of the project, ready/in production deployment.
- Develop: Development branch, where changes from new implementations and bug fixes will converge.

In addition, new branches will be opened and closed depending on the necessary issues.

## Testing

- Api: Will be doing unit and integration testing for code coverage and continuous integration.
- Plugin: Will be doing in game testing as integration tests since we can not do unit testing for this develop.

## Cloud Computing scalability
 
This project will be divided into different instances using cloud computing:
- API instance.
- Logs Instance.
- Database instance.
- n Minecraft servers instances.

We could have n minecraft servers (in the cloud or locally). These servers will have the [wwtshop](https://github.com/RedRiotTank/wwtshop/tree/master) plugin installed, the plugin will manage interactions with [wwtapi](https://github.com/RedRiotTank/wwtapi) which will be running in the cloud and linked to a database instance. Logger instance will be registering transactions or possible errors.   

## About this repository

Remember this repository is a modules container, you can learn more form git modules [here](https://git-scm.com/book/en/v2/Git-Tools-Submodules). This means the references on this repository won't point directly to the master submodules branch but the last master submodule branch that was updated for this repository. So I will be updating this repository pointers everytime I obtain a stable version of any of the submodules.  

Milestones and issues won't be done in this repository neither, each repository will have their own for a better separation of functionality.
