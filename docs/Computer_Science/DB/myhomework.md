# My Homework

## 第一次作业

### 1.7

List four significant differences between a file-processing system and a DBMS.

1. Data Redundancy and Consistency:

For File-Processing System, data redundancy is common because the same data may be duplicated across multiple files. This can lead to inconsistencies if updates are not applied uniformly. However, as for DBMS, redundancy is minimized.

2. Data Integrity and Security:

Integrity constraints and security measures are typically implemented at the application level in File-Processing System. But for DBMS, it provides robust mechanisms for enforcing data integrity and security at the system level.

3. Data Isolation:

Data in File-Processing System is typically isolated within specific applications, compared to data in DBMS, which is centralized and can be shared across multiple applications and users.

4. Concurrency Control for Multiple User:

Concurrency control is typically not built into file-processing systems. But a DBMS provides built-in concurrency control mechanisms to ensure that multiple users can access and modify data simultaneously without conflicts.

---

### 1.8

Explain the concept of physical data independence and its importance in database systems.

Physical data independence is the ability to modify the physical schema without changing the logical schema. It is a fundamental principle in database systems that enhances flexibility, scalability, and maintainability. By decoupling the physical storage details from the logical data representation, it allows for efficient management and optimization of data storage without impacting the applications that rely on the database.

---

### 1.9

List five responsibilities of a database-management system. For each responsibility, explain the problems that would arise if the responsibility were not discharged.

1. Efficiency and Scalability in Data Access

Users might experience slow response times, and the system could become unusable under heavy load, if the responsibility were not discharged.

2. Reduced Application Development Time

Without it, developers would have to manually manage data storage and retrieval for every application feature, slowing down the development process.

3. Data Independence

If the storage system will be upgrated, applications might break if they are tightly coupled to the physical storage details.

4. Data Integrity and Security

For example, in a banking system, without integrity constraints, account balances could become incorrect, and without security measures, hackers could steal customer information.

5. Concurrent Access and Robustness

Such as in an e-commerce platform, without concurrency control, two users might purchase the last item in stock simultaneously, leading to overselling. Without recovery mechanisms, a system crash could result in lost orders or payment data.

---

### 1.15 

Describe at least three tables that might be used to store information in a socialnetworking system such as Facebook.

1. **Users Table**

This table stores information about the users of the social networking platform, containing user_id, username, email, first_name, last_name, date_of_birth and profile_picture.

2. **Posts Table**

This table stores information about the posts made by users, containing post_id, user_id, content and media_url.

3. **Friends Table**

This table stores relationships between users, containing friendship_id, user_id1, user_id2 and status.

---