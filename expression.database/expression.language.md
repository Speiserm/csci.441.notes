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
Equivalent Forms:

`${name}`

`<%=pageContext.findAttribute("name") %>`
```
<jsp:useBean id="name"
    type="somePackage.SomeClass"
    scope="...">
<%=name %>
```
---
### Examples
Coming soon...
