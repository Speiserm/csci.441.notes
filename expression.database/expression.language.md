## Expression language

### Test points:
#### [1. How to invoke the EL](#invoking)

#### [2. Scoped Variables / Search Order](#scoped)

#### [3. Equivalent Forms](#equivalent)

---
### What is Expression Language?
The JSP 2.0 EL provides concise, easy-to-read access to:
- Bean properties
- Collection elements
- Standard HTTP elements such as request parameters, request headers, and cookies

The JSP 2.0 EL works best with MVC. You should only use it to output values created by separate Java code, and resist using it for business logic.

### Advantages of Expression Language

- __Concise access to stored objects.__
  - To output a __Scoped Variable__ (An object stored with setAttribute in the PageContext, HttpServletRequest, HttpSession, or ServletContext) named saleItem, you would use `${saleItem}`.


- __Shorthand notation for bean properties.__
  - To output the companyName property (i.e., result of the getCompanyName method) of a scoped variable named company, you would use `${company.companyName}`.

  - To access the firstName property of the president property of a scoped variable named company, you would use `${company.president.firstName}`.

- __Simple access to collection elements.__
  - To access an element of an array, List, or Map, you would use `${variable[indexOrKey]}`.


- __Succinct access to request parameters, cookies, and other request data.__
  - To access the standard types of request data, you can use one of several predefined implicit objects.


- __A small but useful set of simple operators.__
  - To manipulate objects within EL expressions, you can use any of several arithmetic, relational, logical, or empty-testing operators.


- __Conditional output.__
  - To choose among output options, you do not have to resort to Java scripting elements. Instead, you can use `${test ? option1:option2}`.


- __Automatic type conversion.__
  - The expression language removes the need for most typecasts and for much of the code that parses strings as numbers.


- __Empty values instead of error messages.__
  - In most cases, missing values or NullPointerExceptions result in empty strings, not thrown exceptions.

<a name="invoking"></a>
### Invoking the Expression Language

#### Basic form: `${expression}`
These EL elements can appear in ordinary text or in JSP tag attributes, provided that those attributes permit regular JSP expressions. For example:
```html
<ul>
<li>Name: ${expression1}</li>
<li>Address: ${expression2}</li>
</ul>
<jsp:include page="${expression3}"/>
  ```


#### The EL in tag attributes
You can use multiple expressions (possibly intermixed with static text) and the results are coerced into strings and concatenated. For example:
```html
<jsp:include page="${expr1}blah ${expr2}"/>
```

### Escaping special characters
To get ${ in the page output, use `\${` in the JSP page.

To get a single quote within an EL expression, use `\'`.

To get a double quote within an EL expression, use `\"`.

<a name="scoped"></a>
### Accessing Scoped Variables
`${varName}` is used to search the PageContext, the HttpServletRequest, the HttpSession, and the ServletContext, __in that order__, and output the object with that attribute name.
* PageContext does not apply with MVC.

<a name="equivalent"></a>
### Equivalent Forms:

#### JSP Scripting Elements: Scriptlets, expressions, and declarations


1. __Expressions__

Expressions are formatted like `<%=expression %>`. These are evaluated, converted to a string, and then placed directly into the output. For example, `Current time: <%=new java.util.Date() %>` would return the text `Current time: 11:44` or whatever time it currently is. You also have access to the following predefined variables:

- `request` - The HttpServletRequest.
- `response` - The HttpServletResponse.
- `session` - The HttpSession associated with the request.
- `out` - The PrintWriter, used to send output to the client.


2. __Scriptlets__

Scriptlets are formatted like `<% code %>`. They're used to do more complex things than a single simple expression. Scriptlets insert code into the service() method of the generated servlet. Scriptlets can access the same automatically defined variables as expressions (request, response, session, and out). For example,
```java
<%
  String name = request.getParameter("name");
  out.println("name:" + name);
%>
```

3. __Declarations__

Declarations are formatted like `<%! code %>`. They can be used to define methods or fields that then get inserted into the main body of the servlet class, outside of the service method processing the request. For example,
```java
<%!
  public int getValue(){
    return 69420;
  }
%>
```

---
### Examples
Coming soon...
