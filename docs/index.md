# About

This project is a view for logs in relational databases. The logs are collected by the **audit-mq-collector** project, and
generated by any number of applications in a distributed non async way.

See [Project Home] for more details

# Development and Production

To develop the application you will need preparation for the environment, this preparation is like what is used
in production, but in production you will be doing that different (perhaps env variables).

We need 3 things:

1. Configure the database in application-dev.properties
2. Create and configure the login file in [keycloak] server
3. Install Bower Dependencies

This application has spring security but it do not authenticate the users. It delegates to the single sign on server
[keycloak]

I assume you understand what that means, and way is awesome. If not, don't worry, go to the [keycloak]
site and learn it.

<p class="alert alert-info">

<b>Important note!</b> Spring is programmed to let only users with a <b>AUDIT_VIEW_ACCESS</b> authority to access
this application. That means you need to create that role on keycloak and assign to a user, you can assign a role to
another role by using
</i><a href="http://keycloak.github.io/docs/userguide/keycloak-server/html/roles.html">role composition</a></i>
in keycloak server. That adds the flexibility needed

</p>

## Configure the database

Create a **srv/main/resources/application-dev.properties** file. There is a *application-dev.properties.dist* as example
 in the same folder.
 A *.dist* file is a pattern for distribution, do not edit that unless you wanna change the example, this is a common
 mistake, you need to copy the file because it is diferent for every single developer machine, because of this,
 this file is configured to be ignored by git.

 See [configuration.md](./configuration.md) for details

## Configure the login file

In the keycloak server, you need to create a client application.

Download the file, and put in **srv/main/resource/keycloak-dev.json**. Note that the location of this file is configured
in the *application-dev.properties* file, and there is a example in the same folder

In production you probably want change that dynamically with env variables.

## Install bower dependencies

The web files are located in **srv/main/webapp** you need NodeJS installed and the bower package manage installed by
*npm* as a global command. The procedure is to go to the folder in the command line and run `bower install`

 There is, however a gradle command to do that, and the gradle try to install dependencies in the build. That way
 `gradle build` is everything you need for a production _jar_

Installing the dependencies:

     npm install -g bower
     cd src/main/webapp
     bower install

Or with gradle

    npm install -g bower
    ./gradlew bowerInstall

You can run the application, the default environment is the **dev** environment. I recomend to change that in production
using the flag **--spring.profiles.active=prod**

See [configuration](./configuration.md) for options on how to config the application

[keycloak]:http://keycloak.jboss.org
[Project Home]:https://github.com/crcpuc/audit-docs