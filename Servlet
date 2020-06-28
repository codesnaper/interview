## Servlet
-   Servlet is an interface that must be implemented for creating any Servlet.
-   Servlet is a class that extends the capabilities of the servers and responds to the incoming requests. It can respond to any requests.
-   Servlet is a web component that is deployed on the server to create a dynamic web page.

Servlet Method:
1. init()
2. service()
3. destroy()
4. getServletConfig()
5. getsServletInfo()

**withoud load-on-startup**
When First Request hit 
	1. servlet loading
	2. servlet instantiation
	3. init()
	4. service()

When Second Request Hit:
	1. service()

**With load-on-startup**
1. servlet loading
2. servlet instantiation
3. init()

At FIrst Request:
4. service()

At second Request():
5. service()

**Q1. What is a Servlet?**

**Ans**: A  **Servlet** is a Java program that runs on a Web server. It is similar to an applet but is processed on the server rather than a client’s machine. **Servlets** are often run when the user clicks a link, submits a form, or performs another type of action on a website

**Q6. What is the difference between a Generic Servlet and HTTP Servlet?**

**Ans:** A  **common feature**  between Generic Servlet and HTTP Servlet is  both these Classes are  [**Abstract Classes.**](https://www.edureka.co/blog/abstract-classes-in-java/)  But, they do have differences between them which discussed as follows

|**Generic Servlet**|**HTTP Servlet**|
|--|--|
|Protocol Independent|Protocol Specific|
|Belongs to javax.servlet package|Belongs to javax.servlet.http package|
|supports only service() method|supports doGet(), doPost(), doHead() methods|

**What is the use of RequestDispatcher Interface?**

**Ans:** The **RequestDispatcher** interface defines the object that receives the request from the client and dispatches it to the resources such as a servlet, JSP, HTML file. The RequestDispatcher interface has the following two methods:
```public void forward(ServletRequest request, ServletResponse response)```
**Forwards**  request from one servlet to another resource like servlet, JSP, HTML etc.
````public`  `void`  `include(ServletRequest request, ServletResponse response)````
Includes the  **content**  of the resource such as a servlet, JSP, and HTML in the response.
**Q24. What is the difference between ServletConfig and ServletContext?**

**Ans:**  Some of the major differences between  **ServletConfig**  and  **ServletContext**  are:

|**ServletConfig**|**ServletContext**|
|--|--|
|ServletConfig is a unique object per servlet.|ServletContext is a unique object for a complete application.|
|ServletConfig is used to provide the init parameters to the servlet.|ServletContext is used to provide the application-level init parameters that all other servlets can use.|
|Attributes in the ServletConfig object cannot be set.|We can set the attributes in ServletContext that other servlets can use.|

**What is the use of HttpServletRequestWrapper and HttpServletResponseWrapper?**

**Ans:**  Both  **HttpServletRequestWrapper**  and  **HttpServletResponseWrapper**  classes are used to help developers with a custom implementation of a servlet  **request**  and  **response**  types. Programmers can extend these classes and override only the specific methods that they need to implement for customized  **request**  and  **response**  objects.
**What is the difference between Context Parameter and Context Attribute?**

**Ans:** The main difference is,  **Context Parameter**  is a value stored in the deployment descriptor, which is the  **web.xml**  and is loaded during the deployment process. On the other hand,  **Context Attribute**  is the value which is set dynamically and can be used throughout the application.

**Q43. What do you mean by HttpServlet and how it is different from the GenericServlet?**

**Ans:**  **HttpServlet**  is basically extended from GenericServlet and it also inherits the properties of  **Genericservlet.**  HttpServlet defines an  **HTTP protocol**  servlet while GenericServlet defines a  **generic, protocol-independent**  servlet.

**Q46.  How can you create a session in servlet?**

**Ans:** We can get  **HttpSession**  object by calling the  **public method getSession()**  of  **HttpServletRequest.** The following code segment will help us.

1

`HttpSession session = request.getSession();`

**Q47. Explain JSESSIONID and when is it created?**

**Ans**:  **JSESSIONID**  is basically a cookie that is used to manage the session in a Java Web Application. It is created by the  **Web Container**  when a new session is created.

**Q48. What is the difference between sendRedirect() and Forward() in a Servlet?**

**Ans:**  The difference between  **sendRedirect()**  and Forward() can be explained as follows:

**sendRedirect():**

-   **sendRedirect()**  method is declared in HttpServletResponse Interface.
-   The  **syntax**  for the function is as follows:

1

`void` `sendRedirect(String URL)`

-   This method redirects the client request for further processing, the new location is available on a different server or different context. The web container handles this and transfers the request using the browser, this request is visible in the browser in the form of a new request. It is also called a client-side redirect.

**Forward():**

-   **Forward()**  method is declared in the  **RequestDispatcher**  Interface.
-   The syntax for the function is as follows:

1

`forward(ServletRequest request, ServletResponse response)`

-   This passes the request to another resource for processing within the same server, another resource could be any servlet, JSP page. Web container handles the  **Forward()**  method. When we call  **Forward()**  method, a request is sent to another resource without informing the client, about the resource that will handle the request. It will be mentioned on the  **requestDispatcher**  object which we can be got in two ways. Either using  **ServletContext**  or  **Request.**



**Q49. Explain the working of service() method of a servlet.**

**Ans:**  The  **service()**  method is actually the main method that is expected to perform the actual task. The servlet container calls the  **service()**  method to handle requests coming from the  **client/browsers**  and to provide the response back to the client.

Each time the server receives a request for a  **servlet,**  the server creates a new thread and calls for the service. The  **service()**  method checks the  **HTTP**  request type and calls the respective methods as required.

The sample code for the same is as follows:
```
public` `void` `service(ServletRequest request, ServletResponse response)``throws` `ServletException, IOException{}
```


The  **container**  calls the  **service()**  method and service method invokes _doGet(), doPost(), doPut(), doDelete(),_  methods as needed. So you have nothing to do with  **service()**  method but you override either doGet() or doPost() depending on the request you receive from the client-end.

**Explain steps to establish JDBC Connections.**

**Ans:**  The steps to be followed to establish a JDBC Connectio are as follows:

-   **Import JDBC Packages:** Add **import** statements to your  to import required classes in your Java code.
    
-   **Register JDBC Driver:**
-   You should use the _registerDriver()_  method if you are using a non-JDK compliant JVM, such as the one provided by Microsoft. Here each form requires a database **URL**.
    
-   **Database URL Formulation:** URL Formulation is necessary to create a properly formatted address that points to the database to which you want to connect. Once you loaded the driver, you can establish a connection using the  **DriverManager.getConnection()** method. DriverManager.getConnection() methods are−
    
    -   getConnection(String url)
    -   getConnection(String url, Properties prop)
    -   getConnection(String url, String user, String password)

-   **Create a connection object**

You can create a connection using the database URL, username, and password and also using properties object.

-   **Close the connection**

Finally, to end the database session, you need to close all the database connections. However, if you forget, Java’s garbage collector will close the connection when it cleans up stale objects.
