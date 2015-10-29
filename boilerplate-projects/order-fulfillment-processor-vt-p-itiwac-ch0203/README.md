# Order Fulfillment Processor Boilerplate Project

## Table of Contents
**[Resource location](#resource-location)**  
**[Overview](#overview)**
**[System requirements](#system-requirements)**
**[Important code blocks](#important-code-blocks)**  
**[Project notes](#project-notes)**  
**[Server deployment](#server-deployment)**  
**[Tests](#tests)**  

## Resource location
- Resource - [PluralSight] Introduction to Integration With Apache Camel (Feb 19, 2015) - 02. Getting Started With Apache Camel - 02_03-Case Study Download
- Source repository - [https://github.com/mikevoxcap/pluralsight-camel-intro/](https://github.com/mikevoxcap/pluralsight-camel-intro/)

## Overview
This is the installation guide for setting up the order fulfillment processor application that acts as the case study for Pluralsight's Introduction to Integration with Apache Camel. The case study is a custom implementation of a mediator. You will be able to follow along with the course using this case study project as the base for demonstrations.

## System requirements

The case study was developed using the following:

- Windows 8, 64-bit/ Ubuntu 14.04
- IntelliJ Idea
- JDK 1.7.0_45
- Maven 3.0.3
- Spring 4
- PostgreSQL 9.3
- Wildfly 8.1.0.Final

## Server deployment

### Server deployment demo videos

- [PostgreSQL Database import](https://youtu.be/S6_cIeDQ0_w)
- [Wildfly server deployment](https://www.youtube.com/watch?v=K-SMhqBenIc)

Below are the instructions on a per-component basis. The installation assumes Windows, so you will need to follow the instructions that pertain to your OS if you are not using Windows.

### PostgreSQL Database import

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

### Start Wildfly
1. Open a command line and navigate to the root of the Wildfly directory.
2. The following shows the command line to start the server:

        For Linux:   WILDFLY_HOME/bin/startup.sh
        For Windows: WILDFLY_HOME\bin\startup.bat

### Build and Deploy the application
1. Make sure you have started the Wildfly Server as described above.
2. Open a command line and navigate to the root directory of this example.
3. Type this command to build and deploy the archive:

        mvn wildfly:deploy  

4. This will deploy `target/ofp.war` to the running instance of the server.

### Undeploy the Archive
1. Make sure you have started the Wildfly Server as described above.
2. Open a command line and navigate to the root directory of this example.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy

## Tests

### Test scenarios demo video

[https://youtu.be/jGTFzCXVB5I](https://youtu.be/jGTFzCXVB5I)

### Test scenario 1 - View home page

1. Navigate to the following url.       
<http://localhost:8080/ofp/orderHome/>
2. You should see a page with following text.

		Order Fulfillment Management
		Supporting various pages devoted to order fulfillment management.

### Test scenario 2 - Reset orders

1. Navigate to the following url.       
<http://localhost:8080/ofp/orderHome/>
2. Click following link in menu. Orders -> Reset Orders
3. You should see a page with following text.

		Reset Orders
		Clicking the button below will reset the order statuses of all orders to new.
4. Click the button "Click Me!".
5. Page should be reloaded and it should display a list of orders in a table with the Status of "New".

### Test scenario 3 - Process orders

1. Navigate to the following url.       
<http://localhost:8080/ofp/orderHome/>
2. Click following link in menu. Orders -> Process Orders
3. You should see a page with following text.

		Process Orders Orders
		Click the button below to run order fulfillment processing.
4. Click the button "Click Me!".
5. Page should be reloaded and it should display a list of orders in a table. First 5 orders should display with the Status of "Processing".


### Test scenario 4 - View orders

1. Follow "Test scenario 3 - Process orders"
1. Navigate to the following url.       
<http://localhost:8080/ofp/orderHome/>
2. Click following link in menu. Orders -> View Orders
5. Page should display a list of orders in a table. First 5 orders should display with the Status of "Processing".