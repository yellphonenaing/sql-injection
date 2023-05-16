# SQL Injection Basic To Advanced

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
```

```
https://vuln-web.vuln/product.php?id=1' GROUP BY 1-- -
```
