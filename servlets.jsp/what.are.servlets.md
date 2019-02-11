## What are servlets?

___Servlets___ are used to create dynamic web applications. They can serve many purposes, including these:
- Used to create dynamic web applications
- Used as an API to provide interfaces and classes
- Used as an interface that must be implemented for creating any servlet
- Used as a class that extends the ability of servers and responds to any incoming requests

They're small java classes that take in HTTP requests, and return HTTP responses. That's why they're called ___Servlets___, they process and serve back data. They run as a middleman between the requests coming from users, and the database or application that is running on the server itself. 

A ___Servlet Container___, or ___Engine___, is run on the web server and gives you a runtime environment that manages your servlets. It can create instances of servlet classes and also manages the requests to give them to the proper servlets. It does this by creating object instances of servlet classes and giving requests to the proper object.

### Servlets VS Java applications

Servlets don't have a `main()` as java apps do. The `main()` is instead inside the server, which then calls servlets like it calls methods, such as `doGet()` or `doPost()`. This also means that the end user interacts with servlets indirectly, through request and response object API's. The Servlet Container instead passes the request to the servers, which then process that request within the server, and give the response back out. This output is usually in HTML.

These Servlet Containers have 5 specific jobs:
- Create servlet instance
- Call `init()`
- Call `service()` whenever a request is made
  - `service()` calls a method written by a programmer, and it handles the request
  - For example, `doGet()` handles GET requests, as `doPost()` handles Post
- Call `destroy()` before killing the servlet
- Destroy the instance

Whenever a request comes to a servlet, the servlet container does one of two things:
1. If there is an active object running for the servlet, the container will create a new thread to handle the request.

2. If there is no active object for the servlet, the container instantiates a new object of that class, and that objects handles the request.

This object will continue to run as a servlet instance until the container decides to destroy it. If `destroy()` is not set by the servlet, the container will usually destroy it after 10 or 15 minutes, but this value can be changed by the sysadmin. The container can also be set up to never destroy a servlet object.

Some common containers are:
- Tomcat
- Glassfish (Oracle)
- Jetty (Eclipse)
- JBoss (Open-source)

### The old way (CGI)
CGI (Common Gateway Interface) was the old way to process requests and generate dynamic applications. It has several disadvantages, because the server had to call an external program and pass the HTTP request information into it. It also had to generate individual processes for each request. It's model looks like this:

![MVC Model 1](https://www.javatpoint.com/images/cgi.JPG)

#### The disadvantages of CGI
- If there are a large amount of clients, there is a much heavier load, so the server can slow down
- The web server has to start a process for each request and really can't do much else
- The language is tied to whatever platform it's running on.


### The new way (Servlet)
The Servlet enables a web server to instead process multiple requests in a single web container using ___threads___, which means that it can process requests faster and with a lower load on the server.

![MVC Model 1](https://www.javatpoint.com/images/servlet.JPG)

#### Advantages of Servlet
- Servlets use threads instead of creating a new process for every request, so it's a lot more lightweight, faster, and less of a load on the server.
- It is not platform dependent, because it uses Java, you can pass it from platform to platform thanks to the JVM.
- JVM manges your servlets for you, which means it manages memory, garbage collection, and much more that you don't have to worry about.

## A simple servlet example

This code should be sufficient to output the plain text of "Hello World":

```java
import java.io.*;  // input and output streams
import javax.servlet.*; // primary containers
import javax.servlet.http.*; // methods to service requests
public class HelloWorld extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response)
  throws ServletException, IOException {     
    PrintWriter out = response.getWriter();
    out.println("Hello World");
  }
}
```

### A servlet to generate Http

There are a few steps to generate HTML out of a servlet:

1. Tell the browser that you're going to be sending it HTML: `response.setContentType("text/html");`

1. Modify the `println` statments to build a legal webpage. These print statements then need to be changed so that their outputs are within legal HTML tags.

1. Check the output with a formal syntax validator:
 - [W3 Schools](http://validator.w3.org/)
 - [HTML Help](http://www.htmlhelp.com/tools/validator/)

The following code should be a working servlet that can generate a Hello World HTML page:

```java
public class HelloServlet extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
      response.setContentType("text/html");
      PrintWriter out = response.getWriter();
      out.println("<!DOCTYPE html>\n<HTML>\n" +
      "<HEAD><TITLE>Hello </TITLE></HEAD>\n"+
      "<BODY BGCOLOR=\"#FDF5E6\">\n" +
      "<H1>Hello</H1>\n" +
      "</BODY></HTML>");
    }
  }
```
