---
statistics: True
comments: true
---

# Chapter 3 | Introduction to SQL

## Data Definition Language

The SQL **data-definition language (DDL)** allows the specification of information about relations, including:

- The **schema** for each relation.
- The **domain** of values associated with each attribute.
- **Integrity constraints**
- The set of **indices** to be maintained for each relations.
- **Security** and **authorization** information for each relation.
- The **physical storage structure** of each relation on disk.

---

### Domain Types in SQL

- `char(n)` : **Fixed length character string**, with user-specified length n.
- `varchar(n)` : **Variable length character strings**, with user-specified maximum length n.
- `int` : Integer (a finite subset of the integers that is machinedependent).
- `smallint` : Small integer (a machine-dependent subset of the integer domain type).
- `numeric(p,d)` : Fixed point number, with user-specified precision of p digits, with d digits to the right of decimal point.
- `real, double precision` : Floating point and double-precision floating point numbers, with machine-dependent precision.
- `float(n)` : Floating point number, with user-specified precision of at least n digits.

!!! note
    定长字符串，在 c 语言中字符串结尾有 `\0`，但在 SQL 中不是，你说是多长就读到多长。

    整数长度与机器有关。

    p 是有效数字是几位，d 是小数点后几位。number(3,1) allows 44.5 to be store exactly, but neither 444.5 or 0.32 

**Built-in Data Types in SQL**

- `date` : Dates, containing a (4 digit) year, month and date
- `time` : Time of day, in hours, minutes and seconds.
- `timestamp` : date plus time of day
- `interval` : period of time

Interval values can be added to date/time/timestamp values
date, time functions: 

`current_date()`, `current_time()`

`year(x)`, `month(x)`, `day(x)`, `hour(x)`, `minute(x)`, `second(x)`

可以从 date/time/timestamp 中提取出年月日时分秒

??? Example
    date ‘2005-7-27’

    time ‘09:00:30’ time ‘09:00:30.75’

    timestamp ‘2005-7-27 09:00:30.75’

    interval ‘1’ day

    Subtracting a date/time/timestamp value from another gives an interval value.

---

## Create Table Construct

An SQL relation is defined using the create table command : 

create table $r(A_1 \ D_1, A_2 \ D_2, \cdots , A_n \ D_n,(integrity-constraint_1),\cdots,(integrity-constraint_k))$

- `r` is the name of the relation
- each $A_i$ is an attribute name in the schema of relation r
- $D_i$ is the data type of values in the domain of attribute $A_i$

??? Example
    ```sql
    create table instructor(
        ID char(5),
        name varchar(20) not null,
        dept_name varchar(20),
        salary numeric(8,2))
    insert into instructor values('10211', 'Smith', 'Biology', 66000); \\ legal
    insert into instructor values ('10211', null, 'Biology', 66000); \\ illegal
    ```

---

#### Integrity Constraints in Create Table

- not null
- primary key $(A_1, \cdots, A_n)$
- foreign key $(A_m, \cdots, A_n) \ references \ r$

??? Example "Declare ID as the primary key for instructor"
    ```sql
    create table instructor (
        ID char(5),
        name varchar(20) not null,
        dept_name varchar(20),
        salary numeric(8,2),
        primary key (ID),
        foreign key (dept_name) references department)
    ```

- primary key declaration on an attribute automatically ensures not null

---

#### And a Few More Relation Definitions

```sql
create table student (
    ID varchar(5),
    name varchar(20) not null,
    dept_name varchar(20),
    tot_cred numeric(3,0) default 0，
    primary key (ID),
    foreign key (dept_name) references department);
```

```sql
create table takes (
    ID varchar(5),
    course_id varchar(8),
    sec_id varchar(8),
    semester varchar(6),
    year numeric(4,0),
    grade varchar(2),
    primary key (ID, course_id, sec_id, semester, year),
    foreign key (ID) references student,
    foreign key (course_id, sec_id, semester, year) references section );
```

!!! note
    1. `DEFAULT` 关键字用于指定列的默认值。当插入新记录时，如果没有为该列提供值，数据库会自动使用默认值。
    
    2. sec_id can be dropped from primary key above, to ensure a student cannot be registered for two sections of the same course in the same semester.

---

#### And more still

```sql
create table course (
    course_id varchar(8) primary key,
    title varchar(50),
    dept_name varchar(20),
    credits numeric(2,0),
    foreign key (dept_name) references department (dept_name));
    foreign key (dept_name) references department
    on delete cascade |set null |restrict |set default
    on update cascade |set null |restrict |set default
```

被引用掉的元组，如果删掉了，级联（多米诺连锁反应）删除，或者设置为null，或者拒绝删除，或者设置为默认值。

---

## Drop and Alter Table Constructs

- `drop table student` : Deletes the table and its contents.
- `delete from student` : Deletes all contents of table, but retains table.
- `alter table` : 
    - `alter table r add A D` :
        - where A is the name of the attribute to be added to relation r and D is the domain of A.
        - All tuples in the relation are assigned null as the value for the new attribute. 
        - e.g. `alter table student add resume varchar(256);`
    - `alter table r drop A` :
        - where A is the name of an attribute of relation r.
        - Dropping of attributes not supported by many databases.

---

## SQL and Relational Algebra

e.g. 

```sql
select A1, A2, ... An
from r1, r2, ..., rm
where P
```

is equivalent to the following expression in multiset relational algebra

$$\Pi_{A1, A2, ..., An}(r1 \times r2 \times ... \times rm)$$

---

```sql
select A1, A2, sum(A3)
from r1, r2, ..., rm
where P
group by A1, A2
```

is equivalent to the following expression in multiset relational algebra

$$A1,A2 \ G_{sum(A3)}(\sigma_P(r1 \times r2 \times ... \times rm))$$

---

### Basic Query Structure

The SQL **data-manipulation language (DML)** provides the ability to query information, and insert, delete and update tuples.

A typical SQL query has the form:

```sql
select A1, A2, ..., An
from r1, r2, ..., rm
where P
```

- `A1` represents an attribute
- `r1` represents a relation
- `P` is a predicate

!!! info
    在 `sql` 中不区分大小写，这是历史遗留问题。

The result of an SQL query is a relation.

---

### The `select` Clause

The `select` clause list the attributes desired in the result of a query, corresponds to the projection operation of the relational algebra.

**Example**: find the names of all instructors:

??? Example "answer"
    ```sql
    select name
    from instructor
    ```

SQL allows duplicates in relations as well as in query results. 

- To force the elimination of duplicates, insert the keyword  `distinct` after select.

**Example**: Find the names of all departments with instructor, and remove duplicates

??? Example "answer"
    ```sql
    select distinct dept_name
    from instructor
    ```

- The keyword `all` specifies that duplicates not be removed.

??? Example "answer"
    ```sql
    select all dept_name
    from instructor
    ```

- An asterisk(`*`) in the select clause denotes "all attributes".

??? Example "answer"
    ```sql
    select *
    from instructor
    ```

The select clause can contain arithmetic expressions involving the operation, +, –, *, and /, and operating on constants or attributes of tuples.

**Example**: Find  a relation that is the same as the instructor relation, except that the value of the attribute salary is divided by 12.

??? Example "answer"
    ```sql
    select ID, name, dept_name, salary/12
    from instructor
    ```

---

### The `where` Clause

The `where` clause specifies conditions that the result must satisfy.

Corresponds to the **selection predicate** of the relational 
algebra.

**Example**: To find all instructors in Comp. Sci. dept with salary > 80000

??? Example "answer"
    ```sql
    select name
    from instructor
    where dept_name = 'Comp. Sci.' and salary > 80000
    ```

Comparison results can be combined using the logical connectives and, or, and not. Comparisons can be applied to results of arithmetic expressions.

SQL includes a between comparison operator.

**Example**: Find the names of all instructors with salary between $\$90,000 \ and \ \$100,000 \ (that \ is, \ge \$90,000 \ and \ \le \ \$100,000)$

??? Example "answer"
    ```sql
    select name
    from instructor
    where salary between 90000 and 100000
    ```

**Example**: Tuple comparison

??? Example "answer"
    ```sql
    select name, course_id
    from instructor, teaches
    where (instructor.ID, dept_name) = (teaches.ID, 'Biology');
    ```

---

### The `from` Clause

The `from` clause lists the relations involved in the query.

Corresponds to the **Cartesian product** operation of the relational algebra.

**Example**: Find the Cartesian product instructor $\times$ teaches.

??? Example "answer"
    ```sql
    select *
    from instructor, teaches
    ```

Cartesian product not very useful directly, but useful combined with where-clause condition (selection operation in relational algebra).

---

### `Joins`

**Example**: For all instructors who have taught some course, find their names and the course ID of the courses they taught.

??? Example "answer"
    ```sql
    select name, course_id
    from instructor, teaches
    where instructor.ID = teaches.ID
    ```

**Example**: Find the course ID, semester, year and title of each course offered by the Comp. Sci. department.

??? Example "answer"
    ```sql
    select section.course_id, semester, year, title
    from section, course
    where section.course_id = course.course_id and dept_name = 'Comp. Sci.'
    ```

---

### `Natural Join`

Natural join matches tuples with the same values for all common attributes, and retains only one copy of each common column.

**Example**: 

```sql
select name, course_id
from instructor, teaches
where instructor.ID = teaches.ID;

select name, course_id
from instructor natural join teaches;
```

!!! Attention
    Beware of **unrelated attributes with same name** which get equated incorrectly

**Example**: List the names of instructors along with the titles of courses that they teach.

course(course_id, title, dept_name, credits)
teaches(ID, course_id, sec_id,semester, year)
instructor(ID,name, dept_name, salary)

??? Example "Incorrect version"
    ```sql
    select name, title
    from instructor natural join teaches natural join course;
    ```

??? Example "Correct version"
    1. 

    ```sql
    select name, title
    from instructor natural join teaches, course
    where teaches.course_id = course.course_id;
    ```

    2. 

    ```sql
    select name, title
    from (instructor natural join teacher) join course using(course_id);
    ```

    3. 

    ```sql
    select name, title
    from instructor，teaches, course
    where instructor.ID = teaches .ID and teaches.course_id  = course.course_id;
    ```

**Example**: Find students who takes courses across his/her department.

student( ID, name, dept_name, tot_cred)
takes ( ID, course_id, sec_id, semester, year.grade)
course( course_id, title, dept_name, credits)

??? Example "answer"
    ```sql
    select distinct student.id
    from (student natural join takes) join course using (course_id)
    where student.dept_name <> course.dept_name
    ```

---

### The `Rename` Operation

The SQL allows renaming relations and attributes using the `as` clause:

old-name as new-name

```sql
select ID, name, salary/12 as monthly_salary
from instructor
```

Find the names of all instructors who have a higher salary than some instructor in 'Comp. Sci'.

??? Example "answer"
    ```sql
    select distinct T. name
    from instructor as T, instructor as S
    where T.salary > S.salary and S.dept_name = 'Comp. Sci.'
    ```

---

### `String` Operations

SQL includes a string-matching operator for comparisons on character strings. The operator `like` uses patterns that are described using two special characters:

- percent (`%`). The `%` character matches any **substring**.
- underscore (`_`). The `_` character matches any **character**.

**Example**: Find the names of all instructors whose name includes the substring "dar".

??? Example "answer"
    ```sql
    select name
    from instructor
    where name like '%dar%'
    ```

**Example**: Match the string "100 %"

??? Example "answer"
    ```sql
    like '100 \%' escape '\' 
    like '100 \%' 
    like '100 #%' escape '#'
    ```

Patters are case sensitive.

Pattern matching examples:

- 'Intro%' matches any string beginning with "Intro".
- '%Comp%' matches any string containing "Comp" as a substring.
- '_ _ _' matches any string of exactly three characters.
- '_ _ _ %' matches any string of at least three characters.

SQL supports a variety of string operations such as

- concatenation （using `||`）
- converting from upper to lower case (and vice versa)
- finding string length, extracting substrings, etc.

---

### Ordering the Display of Tuples

List in alphabetic order the names of all instructors

??? Example "answer"
    ```sql
    select distinct name
    from instructor
    order by name
    ```

We may specify desc for descending(降) order or asc forascending（升） order, for each attribute; ascending order is the default.

Example: `order by name desc`

Can sort on multiple attributes

Example: `order by dept_name, name`

查询结果会按照以下规则排序：首先按 dept_name 排序：结果集会根据 dept_name 列的值进行升序排序（默认是升序，即从 A 到 Z）。如果 dept_name 相同，再按 name 排序：在 dept_name 相同的情况下，结果集会根据 name 列的值进行升序排序。

---

### The limit Clause

The `limit` clause can be used to constrain the number of rows returned by the select statement.

`limit` clause takes one or two numeric arguments, which must both be nonnegative integer constants: 

- `limit offset, row_count`
- `limit row_count == limit 0, row_count`

**Example**: List names of instructors whose salary is among top 3. 

??? Example "answer"
    ```sql
    select name
    from instructor
    order by salary desc
    limit 3； // limit 0,3
    ```

- `row_count` : 限制查询结果返回的行数。
- `offset` : 指定从查询结果的第几行开始返回数据。

---

### Duplicates

In relations with duplicates, SQL can define how many copies of tuples appear in the result.

Multiset (多重集) versions of some of the relational algebra operators – given multiset relations $r_1$ and $r_2$ .

---

### Set Operations

这些是真正的集合操作，是需要去重的。

```sql
(select course_id from section where sem = ‘Fall’ and year = 2009)
union
(select course_id from section where sem = ‘Spring’ and year = 2010)

(select course_id from section where sem = ‘Fall’ and year = 2009)
intersect
(select course_id from section where sem = ‘Spring’ and year = 2010)

(select course_id from section where sem = ‘Fall’ and year = 2009)
except
(select course_id from section where sem = ‘Spring’ and year = 2010)
```

如果想要不去重，则需要使用 `all` 。

Suppose a tuple occurs m times in r and n times in s, then, it occurs:

- `m + n` times in r union all s
- `min(m,n)` times in r intersect all s
- `max(0, m – n)` times in r except all s

---

### Null Values

`null` signifies an unknown value or that a value does not exist.

The result of any arithmetic expression involving null is null

**Example**: 5 + null returns null

The predicate is null can be used to check for null values.

**Example**: Find all instructors whose salary is null.

??? Example "answer"
    ```sql
    select name
    from instructor
    where salary is null
    ```

```sql
select sum (salary)
from instructor
```

- Above statement ignores null amounts
- Result is null if there is no non-null amount
- All aggregate operations except count(*) ignore tuples with null values on the aggregated attributes
- Comparisons with null values return the special truth value: unknown.

Three-valued logic using the truth value unknown:

1. `OR`

- (unknown or true) = true
- (unknown or false) = unknown
- (unknown or unknown) = unknown

2. `AND`

- (true and unknown) = unknown
- (false and unknown) = false
- (unknown and unknown) = unknown

3. `NOT`

- (not unknown) = unknown

---

### Aggregate Functions

Find the names and average salaries of all departments whose average salary is greater than 42000

??? Example "answer"
    ```sql
    select dept_name, avg(salary)
    from instructor
    group by dept_name
    having avg(salary) > 42000
    ```

- `having` 也是筛选条件，但是是对组进行筛选

综合版本:

```sql
select dept_name, count (*) as cnt
from instructor
where salary >=100000
group by dept_name
having count (*) > 10
order by cnt;
```

这条 SQL 查询语句的作用是从 instructor 表中筛选出工资 (salary) 大于等于 100,000 的教师，按部门 (dept_name) 分组，统计每个部门的教师人数，并筛选出教师人数大于 10 的部门，最后按教师人数升序排序。

---

## Nested Subqueries

SQL provides a mechanism for the nesting of subqueries.

SQL 提供了一种嵌套子查询的机制。

A subquery is a select-from-where expression that is nested within another query.

A common use of subqueries is to perform tests for :

- set membership
- set comparisons
- set cardinality

---

#### Set Membership

Find courses offered in Fall 2009 and in Spring 2010

??? Example "answer"
    ```sql
    select distinct course_id
    from section
    where semester = 'Fall' and year= 2009 and 
    course_id in (select course_id
                from section
                where semester = 'Spring' and year= 2010);
    ```

真正执行的时候可能会被优化掉。

Find the total number of (distinct) students who have taken course sections taught by the instructor with ID 10101

??? Example "answer"
    ```sql
    select count (distinct ID)
    from takes
    where (course_id, sec_id, semester, year) in
                    (select course_id, sec_id, semester, year
                    from teaches
                    where teaches.ID= '10101');
    ```

---

#### Set Comparison

Find names of instructors with salary greater than that of some (at least one) instructor in the Biology department.

??? Example "answer"
    ```sql
    select distinct T.name
    from instructor as T, instructor as S
    where T.salary > S.salary and S.dept_name = 'Biology';
    ```

Same query using > some clause

??? Example "answer"
    ```sql
    select name
    from instructor
    where salary > some (select salary
                        from instructor
                        where dept_name = 'Biology');
    ```

Find the names of all instructors whose salary is greater than the salary of all instructors in the Biology department.

??? Example "answer"
    ```sql
    select name
    from instructor
    where salary > all (select salary
                        from instructor
                        where dept_name = 'Biology');
    ```

---

#### Scalar Subquery

Scalar (标量) subquery is one which is used where a single value is expected.

确认返回只有一个值的时候可以用。否则。 Runtime error if subquery returns more than one result tuple.

```sql
select name
from instructor
where salary * 10 > 
    (select budget from department 
    where department.dept_name = instructor.dept_name)
```

---

#### Test for Empty Relations

The exists construct returns the value true if the argument subquery is nonempty.

- exists $r \leftrightarrow r \neq \emptyset$
- not exists $r \leftrightarrow r = \emptyset$

---

#### Correlation Variables

Yet another way of specifying the query "Find all courses taught in both the Fall 2009 semester and in the Spring 2010 semester"

??? Example "answer"
    ```sql
    select course_id
    from section as S
    where semester = 'Fall' and year = 2009 and 
        exists (select *
            from section as T
            where semester = 'Spring' and year= 2010 
                    and S.course_id= T.course_id);
    ```

Find all students who have taken all courses offered in the Biology department.

??? Example "answer"
    ```sql
    select distinct S.ID, S.name
    from student as S
    where not exists ((select course_id
                    from course
                    where dept_name = ’Biology’)
                    except
                    (select T.course_id
                    from takes as T
                    where S.ID = T.ID));
    ```

Note that $X - Y = \emptyset \leftrightarrow X \subseteq Y$

Note : Cannot write this query using = all and its variants.

---

#### Test for Absence of Duplicate Tuples

The `unique` construct tests whether a subquery has any duplicate tuples in its result.

- Evaluates to “true” on an empty set

**Example**: Find all courses that were offered at most once in 2009.

??? Example "answer"
    ```sql
    select T.course_id
    from course as T
    where unique (select R.course_id
                from section as R
                where T.course_id= R.course_id 
                    and R.year = 2009) ;
    ```

!!! info
    子查询里面不能加 `distinct` ，只能加在最外面。

**Example**: Find all courses that were offered once in 2009.

??? Example "answer"
    ```sql
    select T.course_id
    from course as T
    where unique (select R.course_id
                from section as R
                where T.course_id= R.course_id 
                    and R.year = 2009) 
            and exists (select R.course_id
                from section as R
                where T.course_id= R.course_id 
                    and R.year = 2009) ;
    ```

    another version

    ```sql
           and course_id in (select course_id
                from section
                where year = 2009) ;
    ```

---

#### With Clause

The **with** clause provides a way of defining a temporary view whose definition is available only to the query in which the **with** clause occurs.

**Example**: Find all departments with the maximum budget

??? Example "answer"
    ```sql
    with max_budget (value) as 
        (select max(budget)
        from department)
    select dept_name
    from department, max_budget
    where department.budget = max_budget.value;

    select dept_name
    from department
    where budget = (select (max(budget) from department));
    ```

- `with` 语句打头先生成一个临时表。

`With` clause is very useful for writing complex queries.

**Example**: Find all departments where the total salary is greater than the average of the total salary at all departments.

??? Example "answer"
    ```sql
    with dept _total (dept_name, value) as
        (select dept_name, sum(salary)
        from instructor
        group by dept_name),
        dept_total_avg(value) as
        (select avg(value)
        from dept_total)
    select dept_name
    from dept_total, dept_total_avg
    where dept_total.value >= dept_total_avg.value;
    ```

---

## Modification of the Database

- Deletion of tuples from a given relation
- Insertion of new tuples into a given relation
- Updating values in some tuples in a given relation

---

### Deletion

- Delete all instructors. 

`delete from instructor`

- Delete all tuples in the instructor relation for those instructors associated with a department located in the Watson building.

```sql
delete from instructor
where dept_name in (select dept_name
                    from department
                    where building = 'Watson');
```

**Example**: Delete all instructors whose salary is less than the average salary of instructors.

??? Example "answer"
    ```sql
    delete from instructor
    where salary< (select avg (salary) from instructor);
    ```

    先算 `avg` 再删除，否则删除后 `avg` 就变了。

---

### Insertion

- Add a new tuple to course.

```sql
insert into course
    values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```

- or equivalently. 这条可以用于忘记了列的顺序的时候，只要列名和值对应即可。

```sql
insert into course (course_id, title, dept_name, credits)
    values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```

---

### Update

- Increase salaries of instructors whose salary is over $100,000 by 3%, and all others receive a 5% raise

```sql
update instructor
    set salary = salary * 1.03
    where salary > 100000;
update instructor
    set salary = salary * 1.05
    where salary <= 100000;
```

- Same query as before but with case statement

```sql
update instructor
    set salary = case
                when salary <= 100000 then salary * 1.05
                else salary * 1.03
                end
```
