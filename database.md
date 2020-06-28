### **What are the different levels of abstraction in the DBMS?**

There are three levels of data abstraction in DBMS. They are:

-   **Physical Level:**  It is the lowest level of abstraction and describes how the data is stored.
-   **Logical Level:**  This is the next level of abstraction after the Physical level. This layer determines what data is stored in the database, and what is the relationship between the data points.
-   **View Level:**  The View Level is the highest level of abstraction and it describes only a part of the entire database.

### **What is normalization and what are the different types of normalization?**

The process of organizing data to avoid any duplication of data and redundancy is known as Normalization.  There are many successive levels of normalization which are known as  **normal forms**. Each consecutive normal form depends on the previous one. The following are the first three normal forms. Apart from these, you have higher normal forms such as BCNF.

-   **First Normal Form (1NF)** – No repeating groups within rows
-   **Second Normal Form (2NF)** – Every non-key (supporting) column value is dependent on the whole primary key.
-   **Third Normal Form (3NF)** – Dependent solely on the primary key and no other non-key (supporting) column value.

## Key in DBMS
-   **Candidate Key –** This is a set of attributes which can uniquely identify a table. Each table can have more than a candidate key. Apart from this, out of all the candidate keys, one key can be chosen as the Primary key. In the above example, since CustomerID and PanNumber can uniquely identify every tuple, they would be considered as a Candidate Key.
-   **Super Key –** This is a set of attributes which can uniquely identify a tuple. So, a candidate key, primary key, and a unique key is a superkey, but vice-versa isn’t true.
-   **Primary Key –**  This is a set of attributes which are used to uniquely identify every tuple. In the above example, since CustomerID and PanNumber are candidate keys, any one of them can be chosen as a Primary Key. Here CustomerID is chosen as the primary key.
-   **Unique Key –** The unique key is similar to the primary key, but allows NULL values in the column. Here the PanNumber can be considered as a unique key.
-   **Alternate Key –** Alternate Keys are the candidate keys, which are not chosen as a Primary key. From the above example, the alternate key is PanNumber
-   **Foreign Key –** An attribute that can only take the values present as the values of some other attribute, is the foreign key to the attribute to which it refers. in the above example, the CustomerID from the Customers Table is referred to the CustomerID from the Customer_Payment Table.
-   **Composite Key –** A composite key is a combination of two or more columns that identify each tuple uniquely. Here, the CustomerID and Date_of_Payment can be grouped together to uniquely identify every tuple in the table.

### **Mention the differences between Trigger and Stored Procedures**

|**Triggers**|**Stored Procedures**|
|--|--|
|A special kind of stored procedure that is not called directly by a user. In fact, a trigger is created and is programmed to fire when a specific event occurs.|A group of SQL statements which can be reused again and again. These statements are created and stored in the database.|
|A trigger cannot be called or execute directly by a user. Only when the corresponding events are fired, triggers are created.|Can execute stored procedures by using the exec command, whenever we want.|
|You cannot schedule a trigger.|You can schedule a job to execute the stored procedure on a pre-defined time.|
|Cannot directly call another trigger within a trigger.|Call a stored procedure from another stored procedure.|
|Parameters cannot be passed as input|Parameters can be passed as input|
|Cannot  return  values.|Can  return  zero or n values.|
|Transactions are not allowed within a trigger.|You can use  transactions  within a stored procedure.|


### **Q27. What do you understand by cursor? Mention the different types of cursor**

A cursor is a database object which helps in manipulating data, row by row and represents a result set.

The types of cursor are as follows:

-   **Implicit cursor:**  This type of cursor is declared automatically as soon as the execution of  [SQL](https://www.edureka.co/blog/sql-commands)  takes place. Here, the user is not indicated about the declaration of the cursor.
-   **Explicit cursor:**  This type of cursor is defined by the PL/ SQL, as it handles a query in more than a single row.
### **What are the differences between DROP, TRUNCATE and DELETE commands?**
|**DROP**|**TRUNCATE**|**DELETE**|
|--|--|--|
|Used to delete a database, table or a view|Used to delete all rows from a table|Used to delete a row in the table| 
|Data cannot be rollbacked|Data cannot be rollbacked|Data can be rollbacked|
| DDL command|A DDL command|A DML command.|
|Slower than TRUNCATE|Faster than DROP and DELETE|Slower than TRUNCATE|

### **Write a query to create a duplicate table with and without data present?**
```
CREATE TABLE DuplicateCustomer AS SELECT * FROM Customers WHERE 1=2;
```

### **Mention a query to calculate the even and odd records from a table**
```
SELECT CustomerID FROM (SELECT rowno, CustomerID from Customers) where mod(rowno,2)=0;
```
### **Write a query to remove duplicate rows from a table?**
```
DELETE FROM Customers WHERE ROWID(SELECT MAX (rowid) FROM Customers C WHERE CustomerNumber = C.CustomerNumber);
```
