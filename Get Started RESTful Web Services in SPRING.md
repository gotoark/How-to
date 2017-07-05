# Get Started RESTful Web Services in SPRING

## Table of Contents
  * [Getting Started](#getting-started)
  * [Pre-requisites](#pre-requisites)
  * [Steps](#steps)
      1. [Create New SPRING MVC Project](#create-new-spring-mvc-project)
      2. [Add Required Dependecies](#add-required-dependecies)
      3. [Servlet Configuration](#servlet-configuration)
      4. [Add Required Bean Classes](#add-required-bean-classes)
      5. [Create Model,DAO,Service,Controller Packages](#create-model,dao,service,controller-packages)
      6. [Create Model Class](#create-model-class)
      7. [Create DAO Class](#create-dao-class)
      8. [Create Service Class](#create-service-class)
      9. [Create Controller Class](#create-controller-class)
     10. [Create a JSP page](#create-a-jsp-page)
     11. [Run On Server](#)
     12. [Test REST Urls ](#)
  * [Errors & Solutions](#run-project)
  * [Conclusion](#conclusion)

## Getting Started               
  
  A Simple Guide for RESTful Web Services in SPRING and HIBERNATE

### Pre-Requisites

* [Spring Tools Suite (Version: 3.6.4.RELEASE or above)](https://spring.io/tools/sts)
* [Apache Tomcat(7.0.77 or above)](https://tomcat.apache.org/download-70.cgi)
* [MySQL Server (5.1 or above)](https://www.mysql.com/downloads/)
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
   
   Now add the Required **Bean Classes**
   
    <!-- For JDBC -->
	<beans:bean id="dataSource"
	 class="org.springframework.jdbc.datasource.DriverManagerDataSource">
	  <beans:property name="driverClassName" value="com.mysql.jdbc.Driver"/>
	<beans:property name="url" value="jdbc:mysql://localhost:3306/springexample"/>  <!-- Give Database Name after / -->
	<beans:property name="username" value="root"/>
	<beans:property name="password" value="root"/>	
	</beans:bean>
	
	<!-- For Hibernate 4 Session Factory Bean Definition -->
	<beans:bean id="hibernate4AnnotatedSessionFactory"
	class="org.springframework.orm.hibernate4.LocalSessionFactoryBean">
	<beans:property name="dataSource" ref="dataSource"/>
	<beans:property name="annotatedClasses">
			<beans:list>
				<beans:value>com.arkthepro.model.Employee</beans:value> <!--Add All Model Classes Here to have Hibernate Access  -->
			</beans:list>
		</beans:property>
		<beans:property name="hibernateProperties">
			<beans:props>
				<beans:prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect
				</beans:prop>
				<beans:prop key="hibernate.show_sql">true</beans:prop>
				 <beans:prop key="hibernate.hbm2ddl.auto">update</beans:prop>
			</beans:props>
		</beans:property>
	</beans:bean>
	
	<!--For Transcation -->
	<beans:bean id="transactionManager" 
	 class="org.springframework.orm.hibernate4.HibernateTransactionManager">
	<beans:property name="sessionFactory" ref="hibernate4AnnotatedSessionFactory"/>
	</beans:bean>
	<tx:annotation-driven transaction-manager="transactionManager" /> 	
    </beans:beans>
    <!-- add this in top xmlns:tx="http://www.springframework.org/schema/tx"  for avoid error on tx:annotation-driven-->
    
Finally Add the **Base Package**

     <!-- Added by Me  -->
      <context:component-scan base-package="com.arkthepro" />   <!--Make Sure Base package dosen't points to particular package  -->
	 

#### Create Model,DAO,Service,Controller Packages

   * Now Create a New Pakage Called Model (com.arkthepro.model) - Under RestFulWebService/src/main/java
   * similarly create a Pakages for DAO,Service and Controllers
   
   
#### Create Model Class

   * Create a New Class Called EmployeeModel under the Package RestFulWebService/src/main/java/com/arkthepro/model
   * Add the Following code in it

    package com.arkthepro.model;
    import javax.persistence.Column;
    import javax.persistence.Entity;
    javax.persistence.GeneratedValue;
    import javax.persistence.Id;
    import javax.persistence.Table;
    
    @Entity
    @Table(name="employee")
    public class Employee {
	private static final long serialVersionUID=1L;
	@Id //defines Primary KEY 
	@GeneratedValue  //Auto Increment
	@Column(name="ID")
	private Integer emp_ID;
	@Column(name="NAME")
	private String emp_NAME;
	@Column(name="AGE")
	private Integer emp_AGE;
	@Column(name="PASSWORD")
	private String emp_PASSWORD;
	
	
	public Integer getEmp_ID() {
		return emp_ID;
	}
	public void setEmp_ID(Integer emp_ID) {
		this.emp_ID = emp_ID;
	}
	public String getEmp_NAME() {
		return emp_NAME;
	}
	public void setEmp_NAME(String emp_NAME) {
		this.emp_NAME = emp_NAME;
	}
	public Integer getEmp_AGE() {
		return emp_AGE;
	}
	public void setEmp_AGE(Integer emp_AGE) {
		this.emp_AGE = emp_AGE;
	}
	public String getEmp_PASSWORD() {
		return emp_PASSWORD;
	}
	public void setEmp_PASSWORD(String emp_PASSWORD) {
		this.emp_PASSWORD = emp_PASSWORD;
	}	
    }

#### Create DAO Class

   * Create a New Class Called EmployeeDAO under the Package RestFulWebService/src/main/java/com/arkthepro/dao

 * Add the Following code in it


     package com.arkthepro.dao;
      import java.util.List;
      import org.hibernate.Session;
      import org.hibernate.SessionFactory;
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Repository;
      import com.arkthepro.model.Employee;
     @Repository
     public class EmployeeDAO {

	@Autowired
	private SessionFactory sessionFactory;
	
	private Session session;
	
	public Session getSession() {
		return this.sessionFactory.getCurrentSession();
	}

	public void closeSession(){
		this.session.close();
	}
	public void setSession(Session session) {
		this.session = session;
	}

	public void setSessionFactory(SessionFactory sf) {
		this.sessionFactory=sf;
		
	}
	
	//Save Function
	public void saveEmployee(Employee emp){
		System.out.println("---------------------------------Save Employee DAO ");
	      Session session =this.sessionFactory.getCurrentSession();
	      session.persist(emp);
	     // session.close();   
	}
	
	public void updateEmployee(Employee emp){
		System.out.println("---------------------------------Update Employee DAO");
		getSession().update(emp);
		//closeSession();
	}
	public void deleteEmployee(Employee emp){
		System.out.println("---------------------------------Delete Employee DAO");
		getSession().delete(emp);
		//closeSession();
	}
	public Employee getEmployee(Integer id){
		System.out.println("---------------------------------Get Employee DAO");
		Employee emp=(Employee)getSession().get(Employee.class, id);
		return emp;
		
	}	
	public List<Employee> getAllEmployee(){
		System.out.println("---------------------------------Get All Employees DAO");
		Session session = this.sessionFactory.getCurrentSession();
        List empList=session.createQuery("From Employee").list();  //here Employee is Not a Table Name its a Class Name Ref: HQL
		return empList;
		}
       }


#### Create Service Class

   * Create a New Class Called EmployeeService under the Package RestFulWebService/src/main/java/com/arkthepro/service
   * Add the Follwing code
      
       
       package com.arkthepro.service;

        import java.util.List;
		import org.springframework.beans.factory.annotation.Autowired;
		import org.springframework.stereotype.Service;
		import org.springframework.transaction.annotation.Transactional;
		import com.arkthepro.dao.EmployeeDAO;
		import com.arkthepro.model.Employee;

		@Service("employeeService") //will be refered in Controller
		public class EmployeeService {
	    @Autowired
	    EmployeeDAO empDAO;
	
	@Transactional(value="transactionManager")  /*here value transactionManager is default so it is optional specify only  wheh we use custom name other than transactionManager */
	public void saveEmployeeService(Employee emp){
		System.out.println("---------------------------------Save Employee SERVICE");
        empDAO.saveEmployee(emp);
	}
	
	@Transactional
	public void updateEmployeeService(Employee emp){
		System.out.println("---------------------------------Update Employee SERVICE");
        empDAO.updateEmployee(emp);
	}
	@Transactional
	public void deleteEmployeeeService(Employee emp){
		System.out.println("---------------------------------Delete Employee SERVICE");
        empDAO.deleteEmployee(emp);
	}
	@Transactional
	public Employee getEmployeeService(Integer id){
		System.out.println("---------------------------------Get Employee SERVICE");
		return empDAO.getEmployee(id);

	}
	@Transactional
	public List<Employee> getAllEmployeeService(){
		System.out.println("---------------------------------Get All Employees SERVICE");
		System.out.println("---------------------------------Total Employees :" + empDAO.getAllEmployee().size());
		return empDAO.getAllEmployee();
	}
    }


 #### Create Controller Class

   * Create a New Class Called EmployeeController under the Package RestFulWebService/src/main/java/com/arkthepro/controller
   * Add the Following Code
   
 		
        package com.arkthepro.controller;

		import java.text.DateFormat;
		import java.util.Date;
		import java.util.HashMap;
		import java.util.List;
		import java.util.Locale;
		import java.util.Map;
		import javax.annotation.Resource;
		import org.slf4j.Logger;
		import org.slf4j.LoggerFactory;
		import org.springframework.stereotype.Controller;
		import org.springframework.ui.Model;
		import org.springframework.web.bind.annotation.RequestMapping;
		import org.springframework.web.bind.annotation.RequestMethod;
		import org.springframework.web.bind.annotation.RequestParam;
		import org.springframework.web.bind.annotation.ResponseBody;
		import com.arkthepro.model.Employee;
		import com.arkthepro.service.EmployeeService;
		/**
		 * Handles requests for the application home page.
		 */
		@Controller
		public class EmployeeController {
	
		private static final Logger logger = LoggerFactory.getLogger(EmployeeController.class);
	
	/**
	 * Simply selects the home view to render by returning its name.
	 */
	
	
	//Declare Service OBje
	@Resource(name="employeeService")
	EmployeeService restService;
	
	@RequestMapping(value = "/", method = RequestMethod.GET)
	public String home(Locale locale, Model model) {
		logger.info("Welcome home! The client locale is {}.", locale);
		
		Date date = new Date();
		DateFormat dateFormat = DateFormat.getDateTimeInstance(DateFormat.LONG, DateFormat.LONG, locale);
		
		String formattedDate = dateFormat.format(date);
		
		model.addAttribute("serverTime", formattedDate );
		
		return "home";
	}
	
	//Insert Employee
	@RequestMapping(value="/addEmployee",method=RequestMethod.GET)
	public @ResponseBody Map<String,List<Employee>> addEmployee(@RequestParam("emp_NAME") String name,@RequestParam("emp_AGE") String age,@RequestParam("emp_PASSWORD") String password) 
	{
		
		Map<String,List<Employee>> empJsont=new HashMap<String,List<Employee>>();
		try{
			Employee emp=new Employee();
			emp.setEmp_NAME(name);
			emp.setEmp_AGE(Integer.parseInt(age));  //Convert String to Int
			emp.setEmp_PASSWORD(password);
			
			//Insert New  employee to DB
			restService.saveEmployeeService(emp);
			//Get Updated List of Employees
			empJsont.put("Success", restService.getAllEmployeeService());
			
		}catch(Exception e){
			empJsont.put("Error", null);
			System.out.println("---------------------------------Error On Insert"+e);			
		}
		return empJsont;
		
	}
	
	//UPDATE  Employee Based on ID
	@RequestMapping(value="/updateEmployee")
	public @ResponseBody Map<String,List<Employee>> updateEmployee(@RequestParam("emp_ID") String id,@RequestParam("emp_NAME") String name,@RequestParam("emp_AGE") String age,@RequestParam("emp_PASSWORD") String password) 
	{
		
		Map<String,List<Employee>> empJsont=new HashMap<String,List<Employee>>();
		try{
			Employee emp=new Employee();
			emp.setEmp_ID(Integer.parseInt(id));
			emp.setEmp_NAME(name);
			emp.setEmp_AGE(Integer.parseInt(age));  //Convert String to Int
			emp.setEmp_PASSWORD(password);		
			//Insert New  employee to DB
			restService.updateEmployeeService(emp);
			//Get Updated List of Employees
			empJsont.put("Success", restService.getAllEmployeeService());
			
		}catch(Exception e){
			empJsont.put("Error", null);
			System.out.println("---------------------------------Error On UPDATE"+e);			
		}
		return empJsont;
		
	}
	//Delete Employee Based on ID
	@RequestMapping(value="/deleteEmployee")
	public @ResponseBody Map<String,List<Employee>> deleteEmployee(@RequestParam("emp_ID") String id) 
	{
		
		Map<String,List<Employee>> empJsont=new HashMap<String,List<Employee>>();
		try{
			Employee emp=new Employee();
			emp.setEmp_ID(Integer.parseInt(id));  //Convert String to Int			
			//Insert New  employee to DB
			restService.deleteEmployeeeService(emp);
			//Get Updated List of Employees
			empJsont.put("Success", restService.getAllEmployeeService());
			
		}catch(Exception e){
			empJsont.put("Error", null);
			System.out.println("---------------------------------Error On DELETE"+e);			
		}
		return empJsont;
		
	}
	//GET ALL Employee LIST
	@RequestMapping(value="/getAllEmployeeList")
	public @ResponseBody List<Employee> getAllEmployeeList(){
		List<Employee> empList = null;
		try{
			empList=restService.getAllEmployeeService();
			
		}catch(Exception e){
			System.out.println("---------------------------------Error On GET EMPLOYEE LIST"+e);			
		}
		return empList;
	}
	
	//GET ALL Employee with json
	@RequestMapping(value="/getAllEmployee")
	public @ResponseBody Map<String,List<Employee>> getAllEmployee() 
	{
		
		Map<String,List<Employee>> empJsont=new HashMap<String,List<Employee>>();
		try{
			empJsont.put("Success", restService.getAllEmployeeService());
			
		}catch(Exception e){
			empJsont.put("Error", null);
			System.out.println("---------------------------------Error On GET EMPLOYEE LIST JSON"+e);			
		}
		return empJsont;
		
	}
	//GET  Employee with json
	@RequestMapping(value="/getEmployeeObject")
	public @ResponseBody Employee getEmployeeObject(@RequestParam("emp_ID") String id) 
	{
		
		Employee emp = null;
		try{
			emp=restService.getEmployeeService(Integer.parseInt(id));
			
		}catch(Exception e){
			System.out.println("---------------------------------Error On GET EMPLOYEE OBJECT"+e);			
		}
		return emp;
		
	}
	
	//GET  Employee with json
	@RequestMapping(value="/getEmployee")
	public @ResponseBody Map<String,Employee> getEmployee(@RequestParam("emp_ID") String id) 
	{
		
		Map<String,Employee> empJsont=new HashMap<String,Employee>();
		try{
			empJsont.put("Success", restService.getEmployeeService(Integer.parseInt(id)));
			
		}catch(Exception e){
			empJsont.put("Error", null);
			System.out.println("---------------------------------Error On GET EMPLOYEE JSON"+e);			
		}
		return empJsont;
		
	}
	}


#### Create a JSP page

* Finally Create a Simple HTML to Showcase Our API Urls (Not Mandatory) 

Paste this code inside home.jsp 

     <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
	<%@ page session="false" %>
	<html>
	<head>
	<title>Home</title>
	</head>
	<center>
	<body>
	<h1>
	SPRING REST WEBSERVICE  </h1>

	<P>  The time on the server is ${serverTime}. </P>
	<h2>
	TEST URLS
	</h2>
	<P>  <a href="http://localhost:8080/restfulwebservice/addEmployee/?emp_AGE=21&emp_PASSWORD=mypassword123&emp_NAME=Rajesh">Add</a>                    - http://localhost:8080/restfulwebservice/addEmployee/?emp_AGE=21&emp_PASSWORD=mypassword123&emp_NAME=Rajesh </P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/addEmployee/?emp_AGE=21&emp_PASSWORD=mypassword123&emp_NAME=Rajesh">Update</a>                - http://localhost:8080/restfulwebservice/addEmployee/?emp_AGE=21&emp_PASSWORD=mypassword123&emp_NAME=Rajesh </P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/deleteEmployee/?emp_ID=5">DELETE</a>                - http://localhost:8080/restfulwebservice/deleteEmployee/?emp_ID=5 </P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/getAllEmployee">GET ALL EMPLOYEE JSON</a> - http://localhost:8080/restfulwebservice/getAllEmployee</P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/getAllEmployeeList">GET ALL EMPLOYEE </a>     - http://localhost:8080/restfulwebservice/getAllEmployeeList</P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/getEmployee?emp_ID=2">GET EMPLOYEE JSON</a>     - http://localhost:8080/restfulwebservice/getEmployee?emp_ID=2</P>
	<P>  <a  href="http://localhost:8080/restfulwebservice/getEmployeeObject?emp_ID=2">GET EMPLOYEE Object</a>   - http://localhost:8080/restfulwebservice/getEmployeeObject?emp_ID=2</P>
	</center>
	</body>
	</html>
   
   

## Conclusion
   
   :astonished: Yea hooo we did it  :raised_hands:  :smiley: 

* [Official Documentation](https://cordova.apache.org/docs/en/latest/guide/platforms/android/#opening-a-project-in-android-studio) - by Cordova