## Model View Controller: Framework for Web Apps

### 3 parts of the model View Controller

- ___The View___ is the part of the app that handles the display or output of the data. The View is often designed after the model data so that it makes sense when it displays that data.

- ___The Controller___ is the part of the application that handles user interaction. The controller can handle user input and read data it receives from the view, then send those inputs to the model.

- ___The Model___ is the part of the app that handles the logic and processes application data. It usually also works with a database to handle retrieving and storing data.

## MVC models

### Model 1:
![MVC Model 1](https://i.imgur.com/6P50lSI.png)

In this model, JSP's handle all of the processing and presentation of the app. This means that your application is a lot less modular, and a smaller amount of JSP's have to handle more work. It also means that you have a little less control than if you split up the work into a controller and a view.

### Model 2: The MVC model

![MVC Model 2](https://i.imgur.com/F1CCsJY.png)

With MVC, you can see that the parts of the application are better divided into functional parts. The View serves the index.html landing page where users will first land, and then the thanks.jsp page where they end. These are both of the views that users will interact with. HTTP requests call the Controller, EmailListServlet.class. Classes like this let you separate out functions into individual modular actions. Then, the model interacts with the controller to pass data back and forth with the data store, or your database.

### Types of files in an MVC model

- An HTML file uses tags that define the content of the actual webpage

- A CSS page contains the formatting for those pages

- Servlets contain Java code for the application to run. When these servlets control how the application runs, they're known as controllers.

- A web.xml file is the deployment descriptor which describes how the application should be configured when it's deployed. This includes things like which page is the landing page, or any JSP's to run when it launches.

- A JavaBean is a Java class that:
  - Provides a zero-argument constructor
  - Provides get and set methods for all of it's instance variables
  - Implements the Serializable or Externalizable interface.

- A JavaServer Page (JSP) consists of special Java tags such as Expression Language (EL) tags that are embedded within HTML code. An EL tag begins with a dollar sign ($).
