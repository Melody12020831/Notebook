---
statistics: True
comments: true
---

# Chapter 8 | Complex Data Types

## Object-based Databases

1. Advanced Database Applications need Complex Data Types
2. Applications are often written in object-oriented programming languages（OOPL）

    - Type system does not match relational type system
    - Switching between imperative language and SQL is troublesome

3. Approaches for integrating object-orientation with databases

    - Build an object-oriented database（OODB） that natively supports object-oriented data and direct access from programming language
    - Build an object-relational database（ORDB）， adding object-oriented features to a relational database
    - Automatically convert data between programming language model and relational model; data conversion specified by object-relational mapping(ORM)

---

## Object-Relational Mapping

1. Object-relational mapping (ORM) systems allow 

    - Specification of mapping between programming language objects and database tuples 
    - Automatic creation of database tuples upon creation of objects 
    - Automatic update/delete of database tuples when objects are update/deleted
    - Interface to retrieve objects satisfying specified conditions
        - Tuples in database are queried, and object created from the tuples

2. Details in Section 9.6.2

    - Hibernate ORM for Java
    - Django ORM for Python

---

## Semi-Structured Data

1. Many applications require storage of complex data, whose schema changes often
2. The relational model’s requirement of atomic data types may be an overkill
    
    - E.g., storing set of interests as a set-valued attribute of a user profile may be simpler than normalizing it

3. Data exchange can benefit greatly from semi-structured data

    - Exchange can be between applications, or between back-end and front-end of an application
    - Web-services are widely used today, with complex data fetched to the front-end and displayed using a mobile app or JavaScript
    
4. XML and JSON are widely used semi-structured data models

    - XML: Extensible Markup Language
        - Earlier generation notation, still used extensively
    - JSON: JavaScript Object Notation
        - Widely used today

---  
