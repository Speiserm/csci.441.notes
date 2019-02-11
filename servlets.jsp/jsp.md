# JavaServer Pages

## Why JSP?
With Servlets, you can easily:
- Read forms
- Read HTTP request headers
- Set HTTP status codes and response headers.
- Use cookies and session tracking
- Share data among Servlets
- Remember data between requests

But, it's not very easy to:
- Use println statements to generate entire HTML pages
- Maintain neat HTML

### JSP Framework

How it works:
- Use regular HTML for most of the pages
- Mark Servlet code with special tags (Like PHP)
- The entire servlet code gets translated into a servlet (once) and that servlet is what actually gets invoked (for each request)

These requests are put between <%= %> tags, like so: `<%= request.getParameter("title") %>`. This request would presumably return the title of the page. Using them within an HTML page looks like this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Order Confirmation</title>
  </head>
  <body>
    <h1>Order Confirmation</h1>
    Thanks for ordering
    <em><%= request.getParameter("title") %></em>!
  </body>
</html>
```

JSP can't do anything a servlet can't do, but because you can easily mix HTML and your usual java. This means that you can easily maintain good HTML code, or even have designers or other members of the team work on the HTML and presentation while you work on the Java. JSP standard practice encourages you to separate the Java code that creates the content from the HTML code that presents it.

### Another example

```HTML
<html>
  <head>
    <title>jsp expressions</title>
    <link rel="stylesheet" href="jsp-styles.css" type="text/css">
  </head>
  <body>
    <h1>jsp expressions</h1>
    <ul>
      <li>current time: <%= new java.util.date() %></li>
      <li>server: <%= application.getserverinfo() %></li>
      <li>session id: <%= session.getid() %></li>
      <li>the <code>testparam</code> form parameter: <%= request.getparameter("testparam") %></li>
      <li>How can we test the testParam?</li>
    </ul>
  </body>
</html>
```
This code should create this page, minus the styling:
![Test page 1](https://i.imgur.com/0XfsACd.png)

So, how do we test the testParam? We simply do a POST as a query string in the address:
`http://localhost:8080/c06a_expressions?testParam=value` should pass testParam a value, which should show up on our page.

## The JSP lifecycle

![The JSP lifecycle](https://i.imgur.com/oR7cVgr.png)

## Invoking Java code with JSP scripting elements
You do not want scripting elements calling servlet code directly, or scripting elements calling them indirectly, through something like utility classes. Instead, you should rely on the use of beans, servlet/JSP combos, MVC with JSP expression language, and custom tags. The most complex, but best way of handling information and data, is to use an MVC with beans, custom tags, anda  framework like Struts or JSF.

Say that you needed 25 lines of Java code to execute some operation. You could throw all 25 lines of that code directly into the JSP page, or you could put those 25 lines into a separate Java class and only put 1 line into the JSP page to invoke it. You should do the latter, because your goal should be to separate your Java and HTML as much as possible. This helps with several different things:

- You write the class in a separate Java environment, not an HTML one, so it's easier to code.
- It's easier to debug because you see errors immediately at compile time. You can also use print statements to debug since you have access to just the Java.
- You can test much easier, since the Java is separate it can act on it's own and test itself before it does any interaction with the html.
- You can also reuse that exact code very easily from other pages by just calling it.

## Basic syntax
Here's what some example code looks like before and after being processed and given to the server:

html text | html comments | jsp comments
--- | --- | ---
`<h1>blah</h1>` | `<!-- comment -->` | `<%-- comment --%>`
This gets passed through, but it's actually sent as servlet code and looks like `out.print("<h1>blah</h1>");` | This similarly gets processed and passed through, it ends up looking like this: `out.print("<!-- comment -->");` because it's HTML and not JSP. | This is not sent to the client because it's specifically a JSP comment. So, it should get ignored. If you need to send `<%` to your page, use the escape: `<\%`.

## Types of scripting elements
Expressions | Scriptlets | Declarations | Directive
--- | --- | --- | ---
`<%= expression %>` | `<% code %>` | `<%! code %>` | `<%@ code %>`
This gets evaluated and inserted into the servlet's output and sent to the client each time the page is requested. It returns in something like `out.print(expression)`. | This statement executes each time the page is requested. | This gets inserted verbatim into the body of the servlet class, outside of any existing methods. This becomes part of the class definition when the page is translated into a servlet. | Sets conditions that apply to the entire JSP.

## JSP Expressions
JSP expressions are what you'll be using most frequently. You can also use XML-compatible syntax, which is formatted like this: `<jsp:expression>Java Expression</jsp:expression>` but you must use it for the entire page if you use it once.

Here's what translating JSP into it's servlet code looks like:

Original JSP | Reslting servlet code
--- | ---
`<%= Math.random() %>` | `out.println(Math.random());`

## Predefined variables

request | response | out | session | application
--- | --- | --- | --- | ---
The HttpServletRequest (The first argument to service  doGet) | The HttpServletResponse (The second argument to service doGet) | The writer, use to send output to the client | The HTTP Session associated with the request | The ServletContext (for sharing data) as obtained via getServletContext().

## A comparison between Servlets and jsp
Here's the code to read three paramaneters and output them into an HTML page with just a servlet:

```
public class ThreeParams extends HttpServlet {
  public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    out.println(docType +"<html>\n"+
    "<head><title>"+title + "</title></head>\n"+
    "<body">\n" +"<h1>" + title + "</h1>\n" +"<ul>\n" + "<li>param1: " + request.getparameter("param1") + "</li>\n" +" <li>param2: " + request.getparameter("param2") + "</li>\n" +" <li>param3: " + request.getparameter("param3") + "</li>\n" +"</ul>\n" +"</body></html>");}}
```

And here's code that will produce a similar page but with JSP:

```html
<html><head><title>reading three request parameters</title></head><body><h1>Reading Three Request Parameters with<br> &lt;%= java expression %&gt;</h1><ul><li><b>param1</b>: <%= request.getparameter("param1") %> </li><li><b>param2</b>: <%= request.getparameter("param2") %> </li><li><b>param3</b>: <%= request.getparameter("param3") %> </li></ul><!-- Expressions are evaluated and inserted into the servlet's output --></body></html>
```
