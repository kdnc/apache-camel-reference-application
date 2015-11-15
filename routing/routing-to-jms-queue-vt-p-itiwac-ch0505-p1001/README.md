# Configuring a Camel route

## Table of Contents
**[Resource location](#resource-location)**  
**[Overview](#overview)**
**[System requirements](#system-requirements)**
**[Important code blocks](#important-code-blocks)**  
**[Project notes](#project-notes)**  
**[Server deployment](#server-deployment)**  
**[Tests](#tests)**  

## Resource location
- Resource - [PluralSight] Introduction to Integration With Apache Camel (Feb 19, 2015) - 05. Routing to a JMS Queue - 05_05-Case Study ActiveMQ Component

## Overview

- Routing to ActiveMQ JMS Queue

## System requirements

The case study was developed using the following:

- Windows 8, 64-bit
- IntelliJ Idea
- JDK 1.7.0_45
- Maven 3.0.3
- Spring 4
- PostgreSQL 9.3
- ActiveMQ 5.12
- Wildfly 8.1.0 Final

## Important code blocks

- pom.xml
- src\test\resources\order-fulfillment-test.properties
- src\main\resources\order-fulfillment.properties
- src\main\java\com\pluralsight\orderfulfillment\config\IntegrationConfig.java

[Watch Video - Important code blocks]()
	
## Project notes

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/message-processing-vt-p-itiwac-ch0410/etc/2-apache-camel-intro-integration-m2-slides-page-002.jpg)
![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/message-processing-vt-p-itiwac-ch0410/etc/2-apache-camel-intro-integration-m2-slides-page-003.jpg)
![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/message-processing-vt-p-itiwac-ch0410/etc/2-apache-camel-intro-integration-m2-slides-page-004.jpg)
![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/message-processing-vt-p-itiwac-ch0410/etc/2-apache-camel-intro-integration-m2-slides-page-005.jpg)
![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/message-processing-vt-p-itiwac-ch0410/etc/2-apache-camel-intro-integration-m2-slides-page-006.jpg)

## Server deployment

### Server deployment demo videos

- [Watch Video - Wildfly server deployment]()

Below are the instructions on a per-component basis. The installation assumes Windows, so you will need to follow the instructions that pertain to your OS if you are not using Windows.

### PostgreSQL Database import

- [Watch Video - PostgreSQL Database import](https://youtu.be/S6_cIeDQ0_w)

The scripts to create the database for the case study project can be found in the project directory:

   order-fulfillment-processor\src\main\sql\postgresql\ddl

Scripts include:

- create-orders-db.sql = Creates the login, database and schema for the project.
- create-orders.sql = Drops and re-creates the database table schema
- drop-orders-db.sql = Drops the orders database

The script to load initial data can be found in the project directory:

- order-fulfillment-processor\src\main\sql\postgresql\dml\load-orders.sql
	
To initially create the database:

1. Log in to `PGAdmin III` or `phppgadmin` and connect using the `postgres` user
2. Create the login for orders using the create statement found in `create-orders-db.sql`
3. Create the database for orders using the create statement found in `create-orders-db.sql
4. Disconnect from the server, then right click the database, select properties and enter the user name as `orders` and password as `orders`.
5. Connect to the server using the `orders` user name. 
6. Open the query tool and run the `create-orders.sql` file, then run the `load-orders.sql` file.

To re-load the database:

1. Log in to `PGAdmin III` or `phppgadmin` and connect using the `orders` user
2. Open the query tool and run the `create-orders.sql` file, then run the `load-orders.sql file`

### Configuring HawtIO on Tomcat to monitor Camel Contexts demo video

[Watch Video - https://youtu.be/Gv9jnPFvlK8](https://youtu.be/Gv9jnPFvlK8)

### Start Wildfly
1. Open a command line and navigate to the root of the Tomcat directory.
2. The following shows the command line to start the server:

        For Linux:   WILDFLY_HOME/bin/startup.sh
        For Windows: WILDFLY_HOME\bin\startup.bat

### Build and Deploy the application
1. Make sure you have started the Tomcat Server as described above.
2. Open a command line and navigate to the root directory of this example.
3. Type this command to build and deploy the archive:

        mvn wildfly:deploy  

4. This will deploy `target/ofp.war` to the running instance of the server.

### Undeploy the Archive
1. Make sure you have started the Tomcat Server as described above.
2. Open a command line and navigate to the root directory of this example.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy

## Tests

### Test scenarios demo video

[Watch video - Test scenarios demo]()