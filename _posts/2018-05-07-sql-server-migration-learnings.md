---
layout: post
title: SQL Server migration learnings
date: 2018-05-07 12:27
author: tmasabari
comments: true
categories: [Databases, SQL Server Migration]
---
https://www.c-sharpcorner.com/article/user-defined-types-in-sql-server/
We have mainly two types of User-defined types in SQL

User-Defined data type
User-Defined Tables Type
User Defined Data Types

When do we have to use it?

When there is a requirement to create a column with a datatype in the database and creating the same data type columns multiple times by multiple people. Here there is no guarantee that all developers will create the same type. In this situation we can make use of User-Defined data types. So, we create at one time and using the type wherever you need.

&nbsp;

&nbsp;

User Defined Table Types

When we have to use it?

Generally, we declare tables to store temp data and use it in the next lines of the script

DECLARE @empTempTab Table (name varchar(100, age int, location VARCHAR(100))
Suppose we need to create the same kind of temp table in multiple SPs. In this case, instead of creating temp tables multiple times we can create required table type once and use it where ever we require.

How to create User defined Table types?

We don’t have UI to create the User-Defined Table as I explained in the Data types. We can create User-Defined Table types using script method.

Spatial Types
https://docs.microsoft.com/en-us/sql/t-sql/spatial-geography/spatial-types-geography?view=sql-server-2017
The geography spatial data type, geography, is implemented as a .NET common language runtime (CLR) data type in SQL Server. This type represents data in a round-earth coordinate system. The SQL Server geography data type stores ellipsoidal (round-earth) data, such as GPS latitude and longitude coordinates.

https://www.mssqltips.com/sqlservertip/1965/sql-server-geography-data-type/
The Geography Data Type
Like the geometry data type, the geography data type is housed as a binary representation of the coordinate, known as the Well-Known Binary Representation, a data type created through the .NET Common Language Runtime (CLR). But the geography data type, unlike the geometry data type, requires the specification of a Spatial Reference System. A Spatial Reference System is system used to identify a particular coordinate system and is specified by an integer. Information on available Spatial Reference Systems available in SQL Server 2008 can be found in the sys.spatial_reference_systems catalog view:

in general, should every table in a database have an identity field to use as a PK?

https://stackoverflow.com/questions/1207983/in-general-should-every-table-in-a-database-have-an-identity-field-to-use-as-a

Surrogate vs. natural/business keys [closed] https://stackoverflow.com/questions/63090/surrogate-vs-natural-business-keys

in 'Patterns of Enterprise Archtecture' [Fowler] it has a good explanation of why you shouldn't use anything other than a key with no meaning other than being a key. It boils down to the fact that it should have one job and one job only.

Remember there is nothing special about a primary key, except that it is labelled as such. It is nothing more than a NOT NULL UNIQUE constraint, and a table can have more than one.

If you use a surrogate key, you still want a business key to ensure uniqueness according to the business rules.

&nbsp;

Just a few reasons for using surrogate keys:

Stability: Changing a key because of a business or natural need will negatively affect related tables. Surrogate keys rarely, if ever, need to be changed because there is no meaning tied to the value.

Convention: Allows you to have a standardized Primary Key column naming convention rather than having to think about how to join tables with various names for their PKs.

Speed: Depending on the PK value and type, a surrogate key of an integer may be smaller, faster to index and search.

It is often the case where some outside body (the customer) legislates that a natural key needs to be edited, and therefore propagated throughout the system. I see this happen regularly. The only way you can be sure that the key won't ever need to change is when it is by definition meaningless. Furthermore, modern databases handle inner joins extremely efficiently, so the potentially large space gains from using surrogates typically outweighs the advantage of not having to do as many inner joins.

A disadvantage of surrogate keys is that they are meaningless (cited as an advantage by some, but...). This sometimes forces you to join a lot more tables into your query than should really be necessary. Compare:

select sum(t.hours)
from timesheets t
where t.dept_code = 'HR'
and t.status = 'VALID'
and t.project_code = 'MYPROJECT'
and t.task = 'BUILD';

against:

select sum(t.hours)
from timesheets t
join departents d on d.dept_id = t.dept_id
join timesheet_statuses s on s.status_id = t.status_id
join projects p on p.project_id = t.project_id
join tasks k on k.task_id = t.task_id
where d.dept_code = 'HR'
and s.status = 'VALID'
and p.project_code = 'MYPROJECT'
and k.task_code = 'BUILD';

&nbsp;

&nbsp;
