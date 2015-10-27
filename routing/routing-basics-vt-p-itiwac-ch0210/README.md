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
- Resource - [PluralSight] Introduction to Integration With Apache Camel (Feb 19, 2015) - 02. Getting Started With Apache Camel - 02_10-Configuring a Camel Route
- Source repository - [https://github.com/mikevoxcap/pluralsight-camel-intro/](https://github.com/mikevoxcap/pluralsight-camel-intro/)

## Overview
How to configure a camel route

## System requirements

The case study was developed using the following:

- Windows 8, 64-bit/ Ubuntu 14.04
- IntelliJ Idea
- JDK 1.7.0_45
- Maven 3.0.3
- Spring 4
- PostgreSQL 9.3
- Wildfly 8.1.0.Final

## Important code blocks

- pom.xml
	- Added Camel libraries

			<dependency>
				<groupId>org.apache.camel</groupId>
				<artifactId>camel-spring</artifactId>
				<version>2.13.2</version>
			</dependency>
			<dependency>
				<groupId>org.apache.camel</groupId>
				<artifactId>camel-spring-javaconfig</artifactId>
				<version>2.13.2</version>
			</dependency>
			
			<dependency>
				<groupId>org.apache.camel</groupId>
				<artifactId>camel-test-spring</artifactId>
				<version>2.13.2</version>
				<scope>test</scope>
			</dependency>

- src\main\java\com\pluralsight\orderfulfillment\config\IntegrationConfig.java
	- Configure Camel context
	- Add Camel routes

			@Configuration
			public class IntegrationConfig extends CamelConfiguration {
			   @Inject
			   private Environment environment;
			   @Override
			   public List<RouteBuilder> routes() {
			      List<RouteBuilder> routeList = new ArrayList<RouteBuilder>();
			      routeList.add(new RouteBuilder() {
			         @Override
			         public void configure() throws Exception {
			            from(
			                  "file://"
			                        + environment
			                              .getProperty("order.fulfillment.center.1.outbound.folder")
			                        + "?noop=true")
			                  .to("file://"
			                        + environment
			                              .getProperty("order.fulfillment.center.1.outbound.folder")
			                        + "/test");
			         }
			      });
			      return routeList;
			   }
			}
	
## Project notes

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-002.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-003.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-004.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-005.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-006.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-007.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-008.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-009.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-010.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-011.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-012.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-013.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-014.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-015.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-016.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-017.jpg)

## Server deployment

### Server deployment demo videos

- [PostgreSQL Database import](https://youtu.be/g3bOEUc01_o)
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

[https://youtu.be/Z1gpG5TOKzM](https://youtu.be/Z1gpG5TOKzM)

### Test scenario 1 - Created .csv file in outbound folder should be again copied to test folder inside outbound folder 

1. Open `C:\nuwan\dev\order-fulfillment-process\fulfillmentcenter1\out` in file explorer.
2. Empty the contents if available in above folder.
3. Navigate to the following url.       
<http://localhost:8080/ofp/orderHome/>
4. Click following link in menu. Orders -> Process Orders
5. Csv file should be created inside the folder, `C:\nuwan\dev\order-fulfillment-process\fulfillmentcenter1\out`
6. With the Apache camel routing, the same Csv file should be copied in to a folder named test, `C:\nuwan\dev\order-fulfillment-process\fulfillmentcenter1\out\test`