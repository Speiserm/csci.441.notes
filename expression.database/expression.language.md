## Expression language

### Test points:
#### [1. How to invoke the EL](#invoking)

#### [2. Scoped Variables / Search Order](#scoped)

#### [3. Equivalent Forms](#equivalent)

---

### Advantages of Expression Language

- Concise access to stored objects.
  - To output a __Scoped Variable__ (An object stored with setAttribute in the PageContext, HttpServletRequest, HttpSession, or ServletContext) named saleItem, you would use `${saleItem}`.


- Shorthand notation for bean properties.
  - To output the companyName property (i.e., result of the getCompanyName method) of a scoped variable named company, you would use `${company.companyName}`.

  - To access the firstName property of the president property of a scoped variable named company, you would use `${company.president.firstName}`.

- Simple access to collection elements.
  - To access an element of an array, List, or Map, you would use `${variable[indexOrKey]}`.


- Succinct access to request parameters, cookies, and other request data.
  - To access the standard types of request data, you can use one of several predefined implicit objects.


- A small but useful set of simple operators.
  - To manipulate objects within EL expressions, you can use any of several arithmetic, relational, logical, or empty-testing operators.


- Conditional output.
  - To choose among output options, you do not have to resort to Java scripting elements. Instead, you can use `${test ? option1:option2}`.


- Automatic type conversion.
  - The expression language removes the need for most typecasts and for much of the code that parses strings as numbers.


- Empty values instead of error messages.
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

## Escaping special characters
To get ${ in the page output, use `\${` in the JSP page.

To get a single quote within an EL expression, use `\'`.

To get a double quote within an EL expression, use `\"`.

<a name="scoped"></a>
## Accessing Scoped Variables
`${varName}` is used to search the PageContext, the HttpServletRequest, the HttpSession, and the ServletContext, __in that order__, and output the object with that attribute name.
* PageContext does not apply with MVC.

<a name="equivalent"></a>
Equivalent Forms:
- `${name}`
- `<%=pageContext.findAttribute("name") %>`
- ```html
<jsp:useBean id="name"
    type="somePackage.SomeClass"
    scope="...">
<%=name %>
```
---
## Examples
Coming soon...
