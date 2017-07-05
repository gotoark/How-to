# Get Started RESTful Web Services in SPRING

## Table of Contents
  * [Getting Started](#getting-started)
  * [Pre-requisites](#prerequisites)
  * [Steps](#Steps)
      1. [Create New SPRING MVC Project](#create-new-spring-mvc-project)
      2. [Add Required Dependecies](#add-required-dependecies)
      3. [Servlet Configuration](#Servlet-Configuration)
      4. [Add Required Bean Classes](#add-required-bean-classes)
      5. [Create Model,DAO,Service,Controller Packages](#)
      6. [Create Model Class](#)
      7. [Create DAO Class](#)
      8. [Create Service Class](#)
      9. [Create Controller Class](#)
     10. [Create a Html](#)
     11. [Run On Server](#)
     12. [Test REST Urls ](#)
  * [Errors & Solutions](#run-project)
  * [Conclusion](#conclusion)

## Getting Started               
  
  A Simple Guide to import existing Cordova Projects to Android Studio and Run 

### Pre-Requisites

* [Spring Tools Suite (Version: 3.6.4.RELEASE or above)](https://spring.io/tools/sts)
* [Java (1.7.0_79 or above)](https://www.java.com/en/download/)
* [Browser (any) ](https://www.google.com/chrome/browser/desktop/index.html)
* [Post Man (Optional)](https://www.getpostman.com/apps)

## Steps

   #### 1. Create New SPRING MVC Project

   * Open **Spring Tools Suite**(aka STS)
   * Choose **File** -> **New** -> **Spring Legacy Project**
   * Enter the **Project Name** and Click **Next**
   * Enter Package Name which Means **com.companyname.projectname**
   * Finish
 
        This wil Creates a new  **SPRING MVC*** Project with Default **Configurations,Controller ,Dependecies and Servlet** 
   
   #### 2. Add Required Dependecies
   
   Inside Your Project Click on the **pom.xml** and Add **Properties,Dependecies** with in the 
   **Dependencies** Tag
   
   Add this with in **Properties**
   
         <!-- Defines Version numbers as Common Variable that  -->
		<java-version>1.7</java-version>
		<org.springframework-version>4.2.3.RELEASE</org.springframework-version>
		<org.aspectj-version>1.6.10</org.aspectj-version>
		<org.slf4j-version>1.6.6</org.slf4j-version>
		<hibernate.version>4.3.5.Final</hibernate.version>

 
   Add the Following in **Dependencies**
         
           <!-- JDBC -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.6</version>
		</dependency>     
        
		<dependency>
    		<groupId>org.springframework</groupId>
    		<artifactId>spring-jdbc</artifactId>
    		<version>${org.springframework-version}</version>
        </dependency>

       <!-- Json --> <!-- If we miss, then this occurs No converter found for return value of type: class java.util.HashMap -->
		<dependency>
			<groupId>com.fasterxml.jackson.core</groupId>
			<artifactId>jackson-databind</artifactId>
			<version>2.3.3</version>
		</dependency>
		 <!-- Hibernate -->
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-core</artifactId>
			<version>${hibernate.version}</version>
		</dependency>
		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-entitymanager</artifactId>
			<version>${hibernate.version}</version>
		</dependency>

		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-c3p0</artifactId>
			<version>${hibernate.version}</version>
		</dependency>
		<!-- Spring ORM -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-orm</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
		<!-- Spring transaction -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-tx</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
				
				<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.6</version>
		</dependency>

 Save the File **(Ctrl+S)**. It will Download and All the Required **JARS** in Background and Build the Project Automatically.
 
#### 3. Servlet Configuration
   
 Open **servlet-context.xml** Which resides in  **yourProject/src/main/webapp/WEB-INF/spring/appServlet**
 
 Lets have a view on the Following tags those were **added automatically by STS.**
   
    <!-- Enables the Spring MVC @Controller programming model -->
	<annotation-driven />
    
    <!-- Handles HTTP GET requests for /resources/** by efficiently serving up static resources in the ${webappRoot}/resources directory -->
	<resources mapping="/resources/**" location="/resources/" />
    <!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
    
	<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<beans:property name="prefix" value="/WEB-INF/views/" />
		<beans:property name="suffix" value=".jsp" />
	</beans:bean>
 
   
   #### 4.Add Required Bean Classes
