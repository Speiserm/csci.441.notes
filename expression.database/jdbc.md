## Java DataBase Connectivity

### Test points:
#### [1. The 7 step process for using JDBC](#steps)

#### [2. Statements - What they are and how to write them](#statements)

### JDBC Introduction
JDBC provides a standard library for accessing relational databases. Its API standardizes a few things:
- A way to establish a connection to the database
- An approach to initiating queries
- A method to create stored (parameterized) queries
- The data structure of the query result (table)
  - Useful for things like determining the number of columns, looking up metadata, etc.

The API however does not standardize SQL syntax. JDBC does nothing to standardize SQL syntax. __JDBC classes are in the java.sql package.__

JDBC consists of two parts, the JDBC API, a purely Java-based API, and the JDBC Driver Manger, which communicates with vendor-specific drivers that perform the actual communication with the database. __This means that the transation to the vendor format is performed on the client.__ This means that there are no changes needed tot he server, and that the driver, or translator, is needed on the client.

![JDBC structure diagram](https://i.imgur.com/M2yDunN.png)

<a name="steps"></a>
### The 7 step process for using JDBC
__1. Load the driver__

`Class.forName("com.mysql.jdbc.Driver");`

__2. Define the connection URL__

```java
//localhost
String host = "jdbc:mysql://127.0.0.1/cars_db";
```

__3. Establish the connection__

```java
String username = "jay_debesee";
String password = "secret";
Connection connection =
  DriverManager.getConnection(host, username, password);
```

__4. Create a statement__
```java
Statement statement =
  connection.createStatement();
```

__5. Execute a query__
```java
String query =
  "SELECT col1, col2, col3 FROM sometable";
ResultSet resultSet =
  statement.executeQuery(query);  
```
Note: To modify the database (aka, not just querying it for info), use `executeUpdate` instead of `executeQuery`. You should supply a string that uses `UPDATE`, `INSERT`, or `DELETE`.

You can also use `setQueryTimeout` to specify a maximum delay to wait for results.

__6. Process the result__
```java
while(resultSet.next()) {
  System.out.println(
    resultSet.getString(1) + " " +
    resultSet.getString(2) + " " +
    resultSet.getString(3));
}
```
Note: The first column's index starts at 1, not 0, because someone really hates us. ResultSet also provides several useful `get` methods that can take a column index or _column name_ and return that data. You can also access result metadata, such as column names.

__7. Close the connection__
`connection.close()`;
Note: Opening a connection to the database is resource intensive, so don't close the connection if additional database operations are expected.

<a name="statements"></a>
### Using Statements
SQL statements are sent to the SQL database via the `Statement` object.

There are three types of statement objects:

- `Statement` - For executing a ___simple SQL statment___
- `PreparedStatement` - For executing a ___precompiled SQL statement___ passing in parameters
- `CallableStatement` - For executing a database ___stored procedure___

### Using Statement methods
`executeQuery` executes the SQL query and returns the data in a table called `ResultSet`. This resulting table may be empty, but will never be null. Example:
```java
ResultSet results =
  statement.executeQuery("SELECT a, b FROM table");
```

`executeUpdate` is used to execute for an `UPDATE`, `INSERT`, or `DELETE` statement. This method will return the number of rows effected by the command. It also supports `CREATE TABLE`, `DROP TABLE`, and `ALTER TABLE`. Example:
```java
int rows =
  statement.executeUpdate("DELETE FROM EMPLOYEES" + " WHERE STATUS=0");
```

`execute` is a generic method for executing stored procedures and prepared statements. It's rarely used, mainly for multiple return result sets. It will either return a `ResultSet` (use `statement.getResultSet`), or a value of true, which means that two or more result sets were produced.

`getMaxRows`/`setMaxRows` are used to determine the maximum number of rows a `ResultSet` may contain. Unless explicitly set, the number of rows is unlimited, and this will return a value of 0.

`getQueryTimeout`/`setQueryTimeout` is used to specify the amount of time a driver will wait for a `Statement` to complete before throwing a `SQLException`.

### Prepared statements, or precomiled queries
The idea is that if you are going to execute similar SQL statements multiple times, using _prepared_ or _parameterized_ statements can be much more efficient. You can create a statement in a standard form that is then sent to the database for compilation before actually being used. Each time you use it, you simply replace some of the marked parameters using the `set` methods. __PreparedStatement inherits from Statement, so the corresponding execute methods have no parameters__ (`execute()`, `executeQuery()`, `executeUpdate()`).

An example:

```java
Connection connection =
  DriverManager.getConnection(url, user, password);
PreparedStatement statement =
  connection.prepareStatement(
    "UPDATE employees "+
    "SET salary = ? "+
    "WHERE id = ?");
int[] newSalaries = getSalaries();
int[] employeeIDs = getIDs();
for(int i=0; i<employeeIDs.length; i++) {
  statement.setInt(1, newSalaries[i]);
}
```
