# DBMS & OOP — Interview Preparation Guide

## Table of Contents

1. [1. What is DBMS? Mention advantages.](#1-what-is-dbms-mention-advantages)
2. [2. What is a Database?](#2-what-is-a-database)
3. [3. What is RDBMS? Mention its properties.](#3-what-is-rdbms-mention-its-properties)
4. [4. Types of database languages](#4-types-of-database-languages)
5. [5. ACID properties](#5-acid-properties)
6. [6. Keys in DBMS](#6-keys-in-dbms)
7. [7. Data abstraction in DBMS](#7-data-abstraction-in-dbms)
8. [8. Indexing in DBMS](#8-indexing-in-dbms)
9. [9. What is normalization? Types of normalization.](#9-what-is-normalization-types-of-normalization)
10. [10. What is functional dependency?](#10-what-is-functional-dependency)
11. [11. What is E-R Model?](#11-what-is-er-model)
12. [12. Serializability in DBMS](#12-serializability-in-dbms)
13. [13. Entity](#13-entity)
14. [14. What is schema?](#14-what-is-schema)
15. [15. What is a view?](#15-what-is-a-view)
16. [16. What is a trigger?](#16-what-is-a-trigger)
17. [17. What is sharding?](#17-what-is-sharding)
18. [18. Lock-based protocol](#18-lockbased-protocol)
19. [19. What is a transaction?](#19-what-is-a-transaction)
20. [20. What is concurrency control?](#20-what-is-concurrency-control)
21. [21. What is deadlock?](#21-what-is-deadlock)
22. [22. What is data redundancy?](#22-what-is-data-redundancy)
23. [23. What is data integrity?](#23-what-is-data-integrity)
24. [24. What is denormalization?](#24-what-is-denormalization)
25. [25. Difference between DELETE, TRUNCATE, and DROP](#25-difference-between-delete-truncate-and-drop)
26. [26. What is DBMS vs file system?](#26-what-is-dbms-vs-file-system)
27. [27. What is a relationship in DBMS?](#27-what-is-a-relationship-in-dbms)
28. [28. What are constraints in DBMS?](#28-what-are-constraints-in-dbms)
29. [29. What is cardinality?](#29-what-is-cardinality)
30. [30. What is degree of relationship?](#30-what-is-degree-of-relationship)
31. [31. What is data independence?](#31-what-is-data-independence)
32. [32. What is log in DBMS?](#32-what-is-log-in-dbms)
33. [33. What is recovery in DBMS?](#33-what-is-recovery-in-dbms)
34. [34. What is checkpoint in DBMS?](#34-what-is-checkpoint-in-dbms)
35. [35. What is dirty read?](#35-what-is-dirty-read)
36. [36. What is phantom read?](#36-what-is-phantom-read)
37. [37. What is non-repeatable read?](#37-what-is-nonrepeatable-read)
38. [38. What is database partitioning?](#38-what-is-database-partitioning)
39. [39. What is clustered vs non-clustered index?](#39-what-is-clustered-vs-nonclustered-index)
40. [40. What is the difference between SQL and NoSQL?](#40-what-is-the-difference-between-sql-and-nosql)
41. [1. What is Object-Oriented Programming (OOP)?](#1-what-is-objectoriented-programming-oop)
42. [2. Explain the four principles of OOP](#2-explain-the-four-principles-of-oop)
43. [3. What are classes and objects in C++?](#3-what-are-classes-and-objects-in-c)
44. [4. Why is encapsulation important in OOP?](#4-why-is-encapsulation-important-in-oop)
45. [5. Explain the concept of polymorphism](#5-explain-the-concept-of-polymorphism)
46. [6. What are constructors and destructors in C++ classes?](#6-what-are-constructors-and-destructors-in-c-classes)
47. [7. What is a superclass?](#7-what-is-a-superclass)
48. [8. What is a subclass?](#8-what-is-a-subclass)
49. [9. Describe the purpose of access specifiers in a class](#9-describe-the-purpose-of-access-specifiers-in-a-class)
50. [10. What is a static member variable or function in a class?](#10-what-is-a-static-member-variable-or-function-in-a-class)
51. [11. What is the purpose of the `this` pointer in C++?](#11-what-is-the-purpose-of-the-this-pointer-in-c)
52. [12. What is a virtual function, and why is it used?](#12-what-is-a-virtual-function-and-why-is-it-used)
53. [13. Distinguish between overriding, overloading, and operator overloading](#13-distinguish-between-overriding-overloading-and-operator-overloading)
54. [14. What is a friend class in C++?](#14-what-is-a-friend-class-in-c)
55. [15. What is the diamond problem in multiple inheritance, and how is it resolved?](#15-what-is-the-diamond-problem-in-multiple-inheritance-and-how-is-it-resolved)
56. [16. What is the role of `const` keyword in C++ member functions?](#16-what-is-the-role-of-const-keyword-in-c-member-functions)
57. [17. Types of Inheritance in OOP](#17-types-of-inheritance-in-oop)
58. [18. How to achieve data abstraction?](#18-how-to-achieve-data-abstraction)

---

# DBMS

## 1. What is DBMS? Mention advantages.
**DBMS (Database Management System)** is software that manages and organizes data in a structured manner, allowing users to store, retrieve, update, and manipulate data efficiently.

### Advantages of DBMS
- Improved data sharing
- Improved data security
- Better data integration
- Minimized data inconsistency
- Reduced data redundancy
- Backup and recovery support
- Better data integrity
- Efficient data access

---

## 2. What is a Database?
A **database** is an organized collection of structured information, typically stored electronically in a computer system.

---

## 3. What is RDBMS? Mention its properties.
**RDBMS (Relational Database Management System)** is a system that stores data in a structured manner using tables with rows and columns.

### Properties of RDBMS
- Data is organized in tables with rows (records) and columns (attributes)
- Relationships between tables are established using keys
- Provides data integrity through constraints like primary keys, foreign keys, and unique keys
- Follows **ACID properties**
- Uses **SQL (Structured Query Language)** for querying and manipulating data
- Utilizes indexing techniques for faster data retrieval
- Provides data security
- Reduces redundancy through normalization

---

## 4. Types of database languages

### 1. DDL (Data Definition Language)
Used to define database structure and schema.
- **CREATE**: Used to create a new table or database object
- **ALTER**: Used to modify the structure of the database
- **DROP**: Deletes the entire table, including all rows and columns
- **TRUNCATE**: Deletes all records from a table without removing table structure
- **RENAME**: Used to rename an object

### 2. DML (Data Manipulation Language)
Used to manipulate and retrieve data within the database.
- **SELECT**: Retrieves data from a database
- **INSERT**: Inserts data into a table
- **UPDATE**: Updates existing data within a table
- **DELETE**: Removes specific records from a table based on conditions

### 3. DCL (Data Control Language)
Used to manage user access and permissions.
- **GRANT**: Gives user access privileges
- **REVOKE**: Takes back permissions from the user

### 4. TCL (Transaction Control Language)
Used to manage transactions.
- **COMMIT**: Saves the transaction permanently
- **ROLLBACK**: Restores the database to the previous state since the last commit
- **SAVEPOINT**: Creates a point within a transaction to roll back partially

---

## 5. ACID properties
ACID properties ensure reliable transaction processing in DBMS.

- **Atomicity**: Either all operations within the transaction are completed, or none of them take effect
- **Consistency**: A transaction brings the database from one valid state to another valid state
- **Isolation**: Transactions are executed independently, as if they were the only ones running
- **Durability**: Once a transaction is committed, its changes become permanent even in case of system failure

---

## 6. Keys in DBMS

### Types of Keys
- **Super Key**: A set of one or more attributes that uniquely identify each row in a table
- **Candidate Key**: The smallest set of attributes that uniquely identifies each row
- **Primary Key**: A candidate key chosen to uniquely identify rows and cannot contain `NULL`
- **Foreign Key**: A column in one table that references the primary key in another table
- **Composite Key**: A key formed by combining multiple columns
- **Unique Key**: Ensures unique values in a column; depending on DBMS it may allow `NULL`
- **Alternate Key**: Candidate keys that were not chosen as the primary key

---

## 7. Data abstraction in DBMS
**Data abstraction** in DBMS refers to hiding complex details of data storage and showing only essential features to users.

### Three levels of abstraction
- **Physical Level**: Describes how data is actually stored in memory
- **Logical Level**: Describes what data is stored and the relationships among the data
- **View Level**: Shows only the part of the database that a specific user needs to see

---

## 8. Indexing in DBMS
**Indexing** is a technique used to optimize database performance by minimizing the number of disk accesses needed when a query is processed.

### Benefits of indexing
- Faster data retrieval
- Improves query performance
- Reduces search time

### Types of indexing
- Primary Index
- Secondary Index
- Clustered Index
- Non-clustered Index

---

## 9. What is normalization? Types of normalization.
**Normalization** is the process of organizing data in a database by breaking larger tables into smaller related tables to reduce redundancy and improve consistency.

### Types of normalization
- **1NF (First Normal Form)**: Removes repeating groups and ensures atomic values
- **2NF (Second Normal Form)**: Removes partial dependency
- **3NF (Third Normal Form)**: Removes transitive dependency
- **BCNF (Boyce-Codd Normal Form)**: Stronger version of 3NF
- **4NF**: Removes multi-valued dependency
- **5NF**: Removes join dependency

---

## 10. What is functional dependency?
A **functional dependency** means that the value of one attribute uniquely determines the value of another attribute in a table.

Example:
If `EmployeeID -> EmployeeName`, then EmployeeID functionally determines EmployeeName.

### Related concepts
- **Partial dependency**: A non-key attribute depends only on part of a composite primary key
- **Transitive dependency**: A non-key attribute depends on another non-key attribute

---

## 11. What is E-R Model?
**ER Model** stands for **Entity-Relationship Model**. It is a graphical representation used to show relationships between entities and attributes. It describes the structure of a database.

### Components of ER Model
- Entity
- Attribute
- Relationship

---

## 12. Serializability in DBMS
**Serializability** ensures that when multiple transactions execute concurrently, the final result is the same as if the transactions had been executed one after another in serial order.

---

## 13. Entity
An **entity** is a real-world object like Professor, Student, or Course in a college database.

### Types of Entity
- **Strong Entity Type**: Has a key attribute for unique identification
- **Weak Entity Type**: Does not have a key attribute of its own and depends on another entity for identity

---

## 14. What is schema?
A **schema** is the blueprint of a database. It defines the tables, columns, constraints, and relationships.

---

## 15. What is a view?
A **view** is a virtual table created from one or more existing tables. It provides a customized presentation of data without storing it separately.

---

## 16. What is a trigger?
A **trigger** is a set of SQL statements that execute automatically in response to certain database events such as `INSERT`, `UPDATE`, or `DELETE`.

---

## 17. What is sharding?
**Sharding** is the practice of distributing data across multiple databases or servers to improve performance and scalability.

---

## 18. Lock-based protocol
Lock-based protocols are used to control concurrent access to data.

### Types of locks
1. **Shared Lock (Read Lock)**: Allows transactions to read data but not modify it
2. **Exclusive Lock (Write Lock)**: Allows transactions to both read and modify data

---

## 19. What is a transaction?
A **transaction** is a sequence of one or more operations performed as a single logical unit of work.

---

## 20. What is concurrency control?
**Concurrency control** ensures that multiple transactions can execute safely at the same time without causing data inconsistency.

---

## 21. What is deadlock?
A **deadlock** occurs when two or more transactions wait indefinitely for each other to release locks.

---

## 22. What is data redundancy?
**Data redundancy** means unnecessary duplication of data in a database.

---

## 23. What is data integrity?
**Data integrity** refers to the accuracy, validity, and consistency of data stored in the database.

---

## 24. What is denormalization?
**Denormalization** is the process of combining tables to improve read performance, even though it may increase redundancy.

---

## 25. Difference between DELETE, TRUNCATE, and DROP

### DELETE
- Removes specific rows
- Can use `WHERE`
- Can be rolled back
- Table structure remains

### TRUNCATE
- Removes all rows
- Cannot use `WHERE`
- Faster than DELETE
- Table structure remains

### DROP
- Removes the entire table
- Deletes both data and structure

---

## 26. What is DBMS vs file system?
- In a **file system**, data is stored in separate files without strong relationships or controls
- In **DBMS**, data is centrally managed with security, consistency, and query support

---

## 27. What is a relationship in DBMS?
A **relationship** represents an association between two or more entities.

### Types of relationships
- One-to-One
- One-to-Many
- Many-to-One
- Many-to-Many

---

## 28. What are constraints in DBMS?
Constraints are rules enforced on data columns to maintain accuracy and reliability.

### Types of constraints
- Primary Key
- Foreign Key
- Unique
- Not Null
- Check
- Default

---

## 29. What is cardinality?
**Cardinality** defines the number of entities in one entity set that can be associated with entities in another entity set.

---

## 30. What is degree of relationship?
The **degree of relationship** refers to the number of entities participating in a relationship.
- Unary
- Binary
- Ternary

---

## 31. What is data independence?
**Data independence** means the ability to change the schema at one level without affecting the schema at the next higher level.

### Types
- Physical data independence
- Logical data independence

---

## 32. What is log in DBMS?
A **log** is a record of all transaction activities used for recovery purposes.

---

## 33. What is recovery in DBMS?
**Recovery** is the process of restoring the database to a correct state after failure.

---

## 34. What is checkpoint in DBMS?
A **checkpoint** is a mechanism that saves the current database state so recovery can start from that point instead of from the beginning.

---

## 35. What is dirty read?
A **dirty read** happens when one transaction reads data written by another transaction that has not yet been committed.

---

## 36. What is phantom read?
A **phantom read** occurs when a transaction re-executes a query and finds new rows inserted by another committed transaction.

---

## 37. What is non-repeatable read?
A **non-repeatable read** happens when the same row is read twice and gives different values because another transaction modified it in between.

---

## 38. What is database partitioning?
**Partitioning** means dividing a large table or database into smaller parts for better performance and manageability.

---

## 39. What is clustered vs non-clustered index?
- **Clustered index** physically arranges data in the table
- **Non-clustered index** creates a separate structure pointing to the data

---

## 40. What is the difference between SQL and NoSQL?
- **SQL databases** are relational, structured, and table-based
- **NoSQL databases** are flexible, non-relational, and may store data as documents, key-value pairs, graphs, or columns

---

# OOPs

## 1. What is Object-Oriented Programming (OOP)?
**OOP** is a programming paradigm that organizes code using objects and classes. It models real-world problems more naturally.

### Why OOP is needed
OOP is needed because it provides:
- Better code organization
- Reusability
- Maintainability
- Modularity
- Easier real-world modeling

---

## 2. Explain the four principles of OOP

### Inheritance
When one class acquires the properties and behavior of another class.

### Polymorphism
The ability of objects to take different forms depending on context.

### Abstraction
Hiding internal details and showing only required functionality.

### Encapsulation
Wrapping data and functions together in a single unit.

---

## 3. What are classes and objects in C++?
A **class** is a blueprint or template that defines the structure and behavior of objects.
An **object** is an instance of a class.

---

## 4. Why is encapsulation important in OOP?
Encapsulation is important because it:
- Provides data security
- Prevents unauthorized access
- Improves maintainability
- Controls data modification

---

## 5. Explain the concept of polymorphism
Polymorphism means the same function or operator can behave differently depending on usage.

### Types of polymorphism
#### Compile-time polymorphism
Occurs at compile time.
- Function overloading
- Operator overloading

#### Run-time polymorphism
Occurs at runtime.
- Function overriding using virtual functions

---

## 6. What are constructors and destructors in C++ classes?
- **Constructor**: Initializes an object when it is created
- **Destructor**: Cleans up resources when an object is destroyed

---

## 7. What is a superclass?
A **superclass** or **base class** is a class that acts as a parent to another class.

Example: `Vehicle` is superclass of `Car`.

---

## 8. What is a subclass?
A **subclass** or **derived class** is a class that inherits from another class.

Example: `Car` is a subclass of `Vehicle`.

---

## 9. Describe the purpose of access specifiers in a class
Access specifiers determine the visibility of class members.

### Types
- `public`
- `private`
- `protected`

---

## 10. What is a static member variable or function in a class?
When a variable is declared as **static** inside a class, memory is allocated only once for the whole program, and all objects share it.

A **static member function** can be called without creating an object of the class.

---

## 11. What is the purpose of the `this` pointer in C++?
The `this` pointer refers to the current object inside a class.

### Uses
- Refers to current object
- Resolves naming conflicts
- Can return current object

---

## 12. What is a virtual function, and why is it used?
A **virtual function** is a member function in a base class that can be overridden in a derived class to achieve **runtime polymorphism**.

---

## 13. Distinguish between overriding, overloading, and operator overloading

### Function overriding
When a child class provides its own version of a method already defined in the parent class.

### Function overloading
When multiple functions have the same name but different parameters.

### Operator overloading
When operators like `+`, `-`, `*` are given custom behavior for user-defined types.

---

## 14. What is a friend class in C++?
A **friend class** can access the private and protected members of another class.

---

## 15. What is the diamond problem in multiple inheritance, and how is it resolved?
The **diamond problem** occurs when a class inherits from two classes that both inherit from the same base class, causing ambiguity.

### Solution
It is resolved using **virtual inheritance**.

---

## 16. What is the role of `const` keyword in C++ member functions?
The `const` keyword in a member function means that function will not modify the object’s data members.

---

## 17. Types of Inheritance in OOP
- **Single Inheritance**: One child inherits from one parent
- **Multiple Inheritance**: One child inherits from more than one parent
- **Multilevel Inheritance**: Inheritance chain like grandparent → parent → child
- **Hierarchical Inheritance**: Multiple child classes inherit from one parent
- **Hybrid Inheritance**: Combination of multiple inheritance types

---

## 18. How to achieve data abstraction?
Data abstraction can be achieved using:
- **Abstract class**
- **Pure virtual function**

### Abstract class
A class that contains at least one pure virtual function.

### Pure virtual function
A function declared with `= 0` and no implementation in the base class.

Example:
```cpp
virtual void show() = 0;



Derived classes must implement pure virtual functions.

19. Shallow copy vs deep copy

Shallow copy

Copies object properties' references, so changes can affect both original and copied object.

Deep copy

Creates a new object and recursively copies all members, so changes are independent.

20. What are getters and setters?

Getter: Function used to get the value of a private member

Setter: Function used to set or update the value of a private member

21. What is abstraction?

Abstraction means showing only the important details and hiding implementation details.

22. What is inheritance?

Inheritance is the process by which one class acquires properties and behavior of another class.

23. What is object slicing in C++?

Object slicing happens when a derived class object is assigned to a base class object, causing derived-class-specific data to be lost.

24. What is an abstract class?

An abstract class is a class that cannot be instantiated directly and contains at least one pure virtual function.

25. What is a pure virtual function?

A pure virtual function is a function with no implementation in the base class and must be overridden in derived classes.

26. What is constructor overloading?

Constructor overloading means defining multiple constructors in the same class with different parameter lists.

27. Can constructors be virtual?

No, constructors cannot be virtual because object creation needs the exact class type to be known.

28. Can destructors be virtual?

Yes, destructors can be virtual. In fact, base class destructors should often be virtual to ensure correct cleanup of derived objects.

29. What is dynamic binding?

Dynamic binding means function call resolution happens at runtime, usually with virtual functions.

30. What is early binding?

Early binding means function call resolution happens at compile time.

31. What is composition in OOP?

Composition means one class contains objects of another class.
It represents a has-a relationship.

32. Difference between aggregation and composition

Aggregation: Weak relationship; contained object can exist independently

Composition: Strong relationship; contained object depends on the container

33. What is message passing in OOP?

Message passing means objects communicate with each other using method calls.

34. Difference between abstraction and encapsulation

Abstraction hides implementation details

Encapsulation wraps data and methods together and restricts direct access

35. Difference between class and struct in C++

In a class, default access is private

In a struct, default access is public

36. What is a virtual destructor?

A virtual destructor ensures proper destruction of derived class objects when deleted through a base class pointer.

37. What is operator overloading?

Operator overloading allows custom behavior for operators when used with user-defined data types.

38. What is method overloading?

Method overloading means having multiple methods with the same name but different parameters in the same class.

39. What is method overriding?

Method overriding means redefining a parent class method in the child class with the same signature.

40. Why is OOP better than procedural programming?

OOP is better for large applications because it offers:

Code reusability

Better maintainability

Better organization

Real-world modeling

Easier debugging and scaling

Important Additional Interview Differences

DBMS vs RDBMS

DBMS may not support relationships

RDBMS supports relational tables and constraints

Primary Key vs Unique Key

Primary key cannot be null

Unique key ensures uniqueness but may allow null depending on DBMS

DELETE vs TRUNCATE vs DROP

DELETE removes selected rows

TRUNCATE removes all rows

DROP removes table completely

Abstraction vs Encapsulation

Abstraction hides complexity

Encapsulation protects data by binding it with methods

Overloading vs Overriding

Overloading: Same name, different parameters

Overriding: Same method signature in parent and child

Compile-time vs Runtime Polymorphism

Compile-time: Resolved by compiler

Runtime: Resolved during execution

Short Revision Section

DBMS quick points

DBMS manages data

RDBMS stores data in tables

SQL is used for querying

ACID ensures reliable transactions

Keys define uniqueness and relationships

Index improves performance

Normalization reduces redundancy

Transactions maintain consistency

OOP quick points

OOP is based on class and object

Four pillars: encapsulation, abstraction, inheritance, polymorphism

Constructor initializes object

Destructor cleans resources

Virtual functions give runtime polymorphism

Abstract class contains pure virtual function

Composition means has-a relationship

