# Database Management System

## Introduction

**Database Management System** (DBMS) is a software which is used to manage databases. A DBMS allows users the following tasks: data definition, data updation, data retrieval and user administration.

### Data Definition Language

DDL deals with database schemas and descriptions, of how the data should reside in the database:

- **CREATE**: to create a database and its objects (tables, indexes, views, stored procedures, functions, and triggers)
- **ALTER**: alters the structure of the existing database
- **DROP**: delete objects from the database
- **TRUNCATE**: remove all records from a table, all spaces allocated for the records are removed
- **COMMENT**: add comments to the data dictionary
- **RENAME**: rename an object

### Data Manipulation Language

DML deals with data manipulation, it is used to store, modify, retrieve, delete and update data in a database:

- **SELECT**: retrieve data from a database
- **INSERT**: insert data into a table
- **UPDATE**: updates existing data within a table
- **DELETE**: Delete all records from a database table
- **MERGE**: UPSERT operation (insert or update)
- **CALL**: call a procedure
- **EXPLAIN PLAN**: interpretation of the data access path
- **LOCK TABLE**: concurrency Control

### Advantages of DBMS vs file system

- **Minimized redundancy and data inconsistency**: The data is **normalized** to minimize the redundancy which helps in keeping data consistent.
- **Simplified data access**: A user only need the name of the relation (not the exact location) to access the data.
- **Efficient memory management and indexing**: Object indexing takes place efficiently through database schema based on any attribute of the data or a data-property. This helps in fast retrieval of data based on the indexed attribute.
- **Multiple data views**: Different views of the same data can be created to cater the needs of different users.
- **Access control and data security**: Only authorized users are allowed to access the data. Also, the data can be encrypted.
- **Concurrent access**: The data can be accessed concurrently by different users at the same time.
- **Transaction management**: A DBMS implements **ACID** (atomicity, durability, isolation,consistency) properties to ensure efficient transaction management without data corruption.
- **Backup and recovery**: Avoid data loss and data inconsistency in case of catastrophic failures.

### Database Objects

They are used to store or reference data. Anything made with the CREATE command is known as a Database Object.

- **Table**: Basic unit of storage; composed of rows and columns
- **View**: Represents logical subsets of data from one or more tables
- **Sequence**: Generates integers for primary key values
- **Index**: An index provides direct and fast access to rows in a table
- **Synonym**: Provides another name for a database object that may exist on a local or another server

## Entity Relationship Model

### Basic Concepts

- Entity, Entity Type, Entity Set
- Attribute(s):
  - Key Attribute
  - Composite Attribute
  - Multivalued Attribute
  - Derived Attribute
- Relationship Type and Relationship Set
- Degree of a relationship set
  - Unary Relationship
  - Binary Relationship
  - n-ary Relationship
- Cardinality
  - One to one
  - Many to one
  - Many to many
- Participation Constraint
  - Total Participation
  - Partial Participation
- Weak Entity Type and Identifying Relationship

### Advanced Concepts

- Generalization and Specialization
- Constraints
  - Total or Partial
  - Overlapped or Disjoint
- Multiple Inheritance
- Union

## Relational Model

## Relational Algebra

## Functional Dependencies

## Normalisation

## Transactions and Concurrency Control

## Indexing, B and B+ trees

## File Organization

## Advanced Topics

## SQL

## Resources

- [Geeks for Geeks Database Management System](https://www.geeksforgeeks.org/dbms/?ref=lbp)
- [School of SRE Relational Databases](https://linkedin.github.io/school-of-sre/level101/databases_sql/intro/)
- [Select Star SQL](https://selectstarsql.com/)
- [Things I Wished More Developers Knew About Databases](https://rakyll.medium.com/things-i-wished-more-developers-knew-about-databases-2d0178464f78)
