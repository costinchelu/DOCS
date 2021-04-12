## Advantages of a PreparedStatement

- Precompilation and DB-side caching of the SQL statement leads to overall faster execution and the ability to reuse the same SQL statement in batches.
- Automatic prevention of SQL injection attacks by builtin escaping of quotes and other special characters. Note that this requires that you use any of the PreparedStatement setXxx() methods to set the values.

```java
preparedStatement = connection.prepareStatement("INSERT INTO Person (name, email, birthdate, photo) VALUES (?, ?, ?, ?)");
preparedStatement.setString(1, person.getName());
preparedStatement.setString(2, person.getEmail());
preparedStatement.setTimestamp(3, new Timestamp(person.getBirthdate().getTime()));
preparedStatement.setBinaryStream(4, person.getPhoto());
preparedStatement.executeUpdate();
```

- Eases setting of non-standard Java objects in a SQL string, e.g. `Date`, `Time`, `Timestamp`, `BigDecimal`, InputStream (`Blob`) and Reader (`Clob`). On most of those types you can't "just" do a `toString()` as you would do in a simple Statement. You could even refactor it all to using `PreparedStatement#setObject()` inside a loop

```java
public static void setValues(PreparedStatement preparedStatement, Object... values) throws SQLException {
    for (int i = 0; i < values.length; i++) {
        preparedStatement.setObject(i + 1, values[i]);
    }
}

preparedStatement = connection.prepareStatement("INSERT INTO Person (name, email, birthdate, photo) VALUES (?, ?, ?, ?)");
setValues(
    preparedStatement, 
    person.getName(), 
    person.getEmail(), 
    new Timestamp(person.getBirthdate().getTime()), 
    person.getPhoto());
preparedStatement.executeUpdate();

```

- Provide stronger separation between the query code and the parameter values (compared to concatenated SQL strings), boosting readability and helping code maintainers quickly understand inputs and outputs of the query.
- In java, can call getMetadata() and getParameterMetadata() to reflect on the result set fields and the parameter fields, respectively
- Accepts SQL ARRAYs, as parameter type via setArray method
- Accepts CLOBs, BLOBs, OutputStreams and Readers as parameter "feeds" via  setClob/setNClob, setBlob, setBinaryStream, setCharacterStream/setAsciiStream/setNCharacterStream methods, respectively
- allows DB-specific values to be set for SQL DATALINK, SQL ROWID, SQL XML, and NULL via setURL, setRowId, setSQLXML ans setNull methods
- Inherits all methods from Statement. It inherits the addBatch method, and additionally allows a set of parameter values to be added to match the set of batched SQL commands via addBatch method.
- A special type of PreparedStatement (the subclass CallableStatement) allows stored procedures to be executed - supporting high performance, encapsulation, procedural programming and SQL, DB administration/maintenance/tweaking of logic, and use of proprietary DB logic & features

## Difference between JDBC and Hibernate

| S.NO | JDBC                                     | Hibernate                                |
|------|------------------------------------------|------------------------------------------|
| 1.   | In JDBC, one needs to write code to map the object model’s data representation to the schema of the relational model. | Hibernate maps the object model’s data to the schema of the database itself with the help of annotations. |
| 2.   | JDBC enables developers to create queries and update data to a relational database using the Structured Query Language (SQL). | Hibernate uses HQL (Hibernate Query Language) which is similar to SQL but understands object-oriented concepts like inheritance, association etc. |
| 3.   | JDBC code needs to be written in a try catch block as it throws checked exception(SQLexception). | Hibernate manages the exceptions itself by marking them as unchecked. |
| 4.   | JDBC is database dependent i.e. one needs to write different codes for different database. | Hibernate is database independent and same code can work for many databases with minor changes. |
| 5.   | Creating associations between relations is quite hard in JDBC. | Associations like one-to-one, one-to-many, many-to-one, and many-to-many can be acquired easily with the help of annotations. |

**JDBC** stands for Java Database Connectivity. It is a java application programming interface to provide a connection between the Java programming language and a wide range of databases (i.e), it establishes a link between the two so that a programmer could send data from Java code and store it in the database for future use.

**Hibernate** is an open-source, non-invasive, light-weight java ORM(Object-relational mapping) framework to develop objects which are independent of the database software and make independent persistence logic in all JAVA, JEE. It simplifies the interaction of java applications with databases. Hibernate is an implementation of JPA(Java Persistence API).

-----------------

Benefits and risks of using Hibernate (hibernate)

What is a SessionFactory? Is it a thread-safe object?  (hibernate)

SessionFactory vs Session  (hibernate)

EntityManager vs EntityManagerFactory  (JPA)

What is the difference between merge and update (hibernate)

What is difference between merge and refresh (jpa)

What is Hibernate Query Language/ Java Persistence Query Language (HQL/JPQL)? (hibernate/jpa)

Lazy loading (hibernate/jpa)

Describe concept of JPA (ex: EntityManager, EntityManagerFactory, PersistenceContext, PersistenceUnit) - (jpa)

Describe annotation: @Temporal/@Transient/@Table/@Version?  - (jpa)

What do you mean by Named – SQL query and how to invoke it? (hibernate/jpa)

What is the difference between sorted and ordered collection in hibernate? (hibernate/jpa?)

Difference between get() and load() (hibernate)

find() vs getReference()  - (jpa)


