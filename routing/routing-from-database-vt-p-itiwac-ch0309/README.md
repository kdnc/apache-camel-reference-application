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
- Resource - [PluralSight] Introduction to Integration With Apache Camel (Feb 19, 2015) - 03. Routing From a Database - 03_09-Routing Rule Implementation

## Overview
How to configure a camel route from database to log file.

SQL Component instance used for routing orders from the orders database and updating the orders database. Camel RouteBuilder for routing orders from the orders database. Routes any orders with status set to new, then updates the order status to be in process. The route sends the message exchange to a log component.

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
	- Added Camel sql libraries

			<dependency>
				<groupId>org.apache.camel</groupId>
				<artifactId>camel-sql</artifactId>
				<version>2.13.2</version>	
			</dependency>
	
	- Added derby library for embedded database used in testing			

			<dependency>
				<groupId>org.apache.derby</groupId>
				<artifactId>derby</artifactId>
				<version>10.10.2.0</version>
				<scope>test</scope>
			</dependency>

- src\main\java\com\pluralsight\orderfulfillment\config\IntegrationConfig.java
	- Camel components
			@Bean
		   public org.apache.camel.component.sql.SqlComponent sql() {
		      org.apache.camel.component.sql.SqlComponent sqlComponent = new org.apache.camel.component.sql.SqlComponent();
		      sqlComponent.setDataSource(dataSource);
		      return sqlComponent;
		   }

	- Routing rule implementation

		   @Bean
		   public org.apache.camel.builder.RouteBuilder newWebsiteOrderRoute() {
		      return new org.apache.camel.builder.RouteBuilder() {
		
		         @Override
		         public void configure() throws Exception {
		            // Send from the SQL component to the Log component.
		            from(
		                  "sql:"
		                        + "select id from orders.\"order\" where status = '"
		                        + OrderStatus.NEW.getCode()
		                        + "'"
		                        + "?"
		                        + "consumer.onConsume=update orders.\"order\" set status = '"
		                        + OrderStatus.PROCESSING.getCode()
		                        + "' where id = :#id").to(
		                  "log:com.pluralsight.orderfulfillment.order?level=INFO");
		         }
		      };
		   }
			
	
## Project notes

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-002.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-003.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-004.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-005.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/2-apache-camel-intro-integration-m2-slides-page-006.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-002.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-003.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-004.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-005.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-006.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-007.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-008.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-009.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-010.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-011.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-012.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-013.jpg)

![](https://raw.githubusercontent.com/kdnc/apache-camel-reference-application/master/routing/routing-basics-vt-p-itiwac-ch0210/etc/3-apache-camel-intro-integration-m3-slides-page-014.jpg)

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

[https://youtu.be/fZ4LYIfDZnI](https://youtu.be/fZ4LYIfDZnI)