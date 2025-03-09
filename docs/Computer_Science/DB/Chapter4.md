---
statistics: True
comments: true
---

# Chapter 4 | Intermediate SQL

## Joined Relations

**Join** operations take two relations and return as a result another relation.

Join operations are typically used as subquery expressions in the **from** clause.

---

## SQL Data Types and Schemas

### User-Defined Types

create type construct in SQL creates user-defined type

```sql
create type Dollars as numeric (12,2) final
```

- `final` means that this type cannot be further extended. 已经是最后一个了，不能再继承。
- 更加方便直观，不用再去写了。
- 这是为了强类型化，防止类型错误，可以在编译的时候就发现错误。

---

### Domains

create domain construct in SQL-92 creates user-defined domain types.

```sql
create domain person_name char(20) not null
```

- Types and domains are similar. Domains can have constraints, such as `not null`, specified on them. 然而 `type` 就没有约束了。

```sql
create domain degree_level varchar(10)
constraint degree_level_test
check (value in ('Bachelors', 'Masters', 'Doctorate')); // 只能取这几个值
```

---

### Large-Object Types

Large objects (photos, videos, CAD files, etc.) are stored as a large object:

`blob` (二进制大对象): binary large object -- object is a large collection of uninterpreted binary data (whose interpretation is left to an application outside of the database system)

MySQL BLOB datatypes:

- `TinyBlob` ： 0 ~ 255 bytes.
- `Blob`： 0 ~ 64K bytes.
- `MediumBlob` ： 0 ~ 16M bytes.
- `LargeBlob` : 0 ~ 4G bytes.

`clob` (字符大对象): character large object -- object is a large collection of character data. 

When a query returns a large object, a pointer is returned rather than the large object itself.

---

## Integrity Constraints

Integrity Constraints on a Single Relation

- `not null` : Declare name and budget to be not null:

```sql
name varchar(20) not null
budget numeric(12,2) not null
```

- `primary key`
- `unique` : The unique specification states that the attributes $A_1, A_2, \cdots, A_m$ form a super key. Candidate keys are permitted to be null (in contrast to primary keys).
- `check (P)`, where P is a predicate. 检验每一行是否满足P。
- `foreign key`

---

### Integrity Constraint Violation During Transactions

```sql
create table person (
ID char(10),
name char(40),
mother char(10),
father char(10),
primary key (ID),
foreign key (father) references person,
foreign key (mother) references person);
```

How to insert a tuple without causing constraint violation?

- insert father and mother of a person before inserting person.
- OR, set father and mother to null initially, update after inserting all persons (not possible if father and mother attributes declared to be not null) .
- OR defer constraint checking to transaction end.

---

### Check

不能用 `foreign key` 的条件来，因为 `foreign key` 要求被引用的一定是 `primary key`。

```sql
check (time_slot_id in (select time_slot_id from time_slot))
```

Unfortunately: subquery in check clause not supported by pretty much any database.

而 `check` 语句不会单独用，而是在 `create table` 语句中使用。

---

### assertion

查询整个表，然后判断是否满足条件。

```sql
create assertion <assertion-name> check 
<predicate>;
create assertion credits_earned_constraint check
(not exists 
    (select ID
    from student
    where tot_cred <> (
        select sum(credits)
        from takes natural join course
        where student.ID=takes.ID
            and grade is not null 
            and grade<>'F')))
 ```

实现这个功能代价很大。

---

## Views (视图)

A view provides a mechanism to hide certain data from the view of certain users. 

Consider a person who needs to know an instructors name and department, but not the salary. This person should see a relation described, in SQL, by 

```sql
select ID, name, dept_name
from instructor
```

Any relation that is not of the conceptual model but is made visible to a user as a “virtual relation” is called a view.

A view is defined using the create view statement which has the form

```
create view v as < query expression >
```

where `<query expression>` is any legal SQL expression. The view name is represented by v.

Once a view is defined, the view name can be used to refer to the virtual relation that the view generates.

View definition is not the same as creating a new relation by evaluating the query expression 

Rather, a view definition causes the saving of an expression; the expression is substituted into queries using the view.

!!! note
    可以理解为 view 是一个虚的表，有表的名字与属性，但是没有表的内容。

1. A view of instructors without their salary

```sql
create view faculty as
    select ID, name, dept_name
    from instructor
```

2. Find the names of all instructors in the Biology department

```sql
    select name
    from faculty
    where dept_name = 'Biology'
```

---

### Update of a View

Add a new tuple to faculty view which we defined earlier

```sql
create view faculty as
    select ID, name, dept_name
    from instructor

insert into faculty values ('30765', 'Green', 'Music');
```

