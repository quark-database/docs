<p align="center">
    <a href="https://anafro.ru/quark">
        <img src="https://raw.githubusercontent.com/quark-database/.github/main/Assets/Banner.png" alt="Quark Banner">
    </a>
</p>

<h1 align="left">About Quark Documentation</h1>

The Quark Documentation describes not the actual implementation of Quark, but the specification of Quark products. Effectively this is a set of guidelines about how to create your own Quark!

<details open>
<summary><kbd>Table of contents</kbd></summary>


1. [📁 Databases in File System](#-databases-in-file-system)
    -  [The capitalized case](#the-capitalized-case)
    -  [Databases](#databases)
    -  [Tables](#table)
    -  [Table records](#table-records)
    -  [Table header](#table-header)
    -  [Records](#records)
    -  [Table variables](#table-variables)
2. [📚 Database Management Specification](#-database-management-specification)
    - [Operations for databases](#operations-for-databases)
    - [Operations for tables](#operations-for-tables)
    - [Operations for records](#operations-for-records)
    - [Operations for columns](#operations-for-columns)
    - [Operations for variables](#operations-for-variables)
    - [Operations for auth tokens](#operations-for-auth-tokens)
    - [Operations for a cloud](#operations-for-a-cloud)
3. [✍️ Query Language Specification](#️-query-language-specification) 
4. [❌ Error Specification](#-error-specification) 


</details>

## 📁 Databases in File System

**Quark** is a relational database management system. It means that the instance of Quark DBMS contains multiple databases with tables inside. Every element, which is any named entity inside Quark, including databases, tables, etc., of the Quark DBMS hierarchy must be named in a special capitalized case.

### The capitalized case

**The capitalized case** used in Quark naming requires words to be capitalized and separated with spaces. The words must only contain latin letters, and digits. Words are allowed to be uppercase, but only if they are abbreviations. 

### Databases

**A database** is a named set of tables. In Quark, each database is a folder. The folder name is considered to be the name of database. All the databases must be stored in one folder (canonically named `Databases`). Every folder inside the database is considered to be a table of this database. 

### Tables

**A table** is a named set of records, and information about columns. A table, like databases, is a folder, which is contained by a database. A table is structured the following way:

```
My Database                     <-- The database folder
|
|---- Users                     <-- The table folder
    |
    |---- Variables             <-- The variables folder
    |   |
    |   |---- Next Id.qvar
    |   |---- Next Token.qvar
    |   |---- ...
    |
    |---- Records.qrecs         <-- The records file of the table
    |---- Header.qhead          <-- The header file of the table
```

Any other file or folder must be ignored.

### Table records

**The table records file** contains all the records. Each line of the file represents one record. 

```
// Records.qrecs
"1","Anatoly",22
"2","Aleksandr",21
"3","Egor",22
```

### Table header

**The table header file** contains names of the table column and their types. Each line of table header contains the type, name, and the properties of the columns. The property list can be empty.

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

int                                         ("Id",                                  incrementing)
^                                            ^                                      ^
| Type of column (here, it is integer)       | The column name (here, it is Id)     | The list of properties (here, it is one property: incrementing)
 \____________________________________        \________________________________      \______________________________________________________________
```

The column definition is a Quark query language expression. <a href="#expressions">Learn more about Quark QL expressions</a>.

### Records

**A record** is a set of cells. Each record contains zero, one, or more values called cells. Effectively each cell is named because of the table header:

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

// Records.qrecs
"1","Anatoly",22
"2","Aleksandr",21
"3","Egor",22


1,                              "Anatoly",                    22
^                               ^                             ^
| Considered to be an Id.       | Considered to be a Name.    | Considered to be an Age.
 \_________________________      \_____________________        \_________________________________
```

**A record inside a record file** is several double-quoted strings separated with commas:

```
"this is a string","123","true"
```

Even though some strings can be stored without quotes, and be not misrecognized (for example, `"strings without commas"`), they must be double-quoted anyways. The quotation mark can be stored into a cell via escaping:
```
                              V              V Just put the backslash in front of the symbols to espace them!
...,"Hi, do you know the book \"War and Peace\"?",...
```

Besides the quotation marks, there is a line break (`\n`) that can be escaped. To store backslash itself, escape it (`\\`).
Any other character cannot be escaped, and is an error.

Inside one table, each record must contain an equal count of cells, same as columns in the table header. It means that the following example is an error:

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

// Records.qrecs
"1","Anatoly",22,"Hello"    <-- ❌ The 4th cell is redundant.
"2","Aleksandr"             <-- ❌ The 3rd cell is missing.
"3","Egor",22               <-- ✅ Ok!
```

### Table variables

**A table variable** contains only one value (for example, a string or an integer). At this moment, in Quark `v4.0`, table variables are only used for the `incrementing` property to store the next integer value for an incrementing column, but variables is a great feature with many undiscovered possibilities.

**A table variable file** contains one line - a Quark expression. <a href="#expressions">Learn more about Quark QL expressions</a>.

All the table variable files are stored inside the `Variables` folder inside the table folder.

```
// Next Id.qvar
100                         <-- 100 will be taken as an Id for the next insertion. 
```

## 📚 Database Management Specification

A user can perform operations on databases, tables, records, columns, variables, auth tokens, and a cloud.

### Operations for databases

#### Create a database

##### Parameters

* 📦 `name` of type `str` - the name of a database;

##### Errors

- ❌ 

#### Rename a database

#### List databases

#### Clone a database

#### Clone a database skeleton

#### List tables in a database

#### Clear a database

#### Delete a database

### Operations for tables

#### Create a table

#### Rename a table

#### List tables

#### Clone a table

#### Clone a table skeleton

#### List tables in a table

#### Clear a table

#### Delete a table

### Operations for records

#### Change records

#### Count records

#### Insert a record

#### Select a record

#### Delete records

### Operations for columns

#### Create a column

#### Rename a column

#### Swap columns

#### Reorder columns

#### List columns

#### Delete a column

### Operations for variables

#### Create a variable

#### Get a variable value

#### Set a variable value

#### List variables in a table

#### Delete a variable

### Operations for auth tokens

#### Create a token

#### Grant a permission to a token

#### Revoke a permission to a token

#### Redefine permissions for a token

#### Delete a token

### Operations for a cloud

#### Get a server name

#### Rename a server

#### Evaluate Quark expression

#### Change the server port

#### Secret instruction

## ✍️ Query Language Specification

> [!CAUTION]
> 🚧 The query language specification will soon be defined.

## ❌ Error Specification

**Errors** must be descriptive in any computer system due to their purpose: describe the problem and help to find a fixing solution. The errors in Quark are based on reports.

### Reports

**A report** is an extension for exceptions, which contains more information about the problematic situation. Besides the error message, there are several messages in it in addition:

* **A context** is an environment of the situation, in what circumstances the problem was born. For example, `The calculator was trying to calculate the expression value`.
* **An error message** is a good old exception message. Describe here the situation, the error itself. For example, `The division by zero is prohibited`. 
* **A piece of advice** is what a user should do to fix the problem. `Please, do not enter zeros for the division operator.`
* **Fix steps** are the steps to fix the problem. In other words, it is a piece of advice, but split to a set of steps. Since a piece of advice is enough, an empty list of steps can be passed.

For example, this is how a string formatted report would look:

```
❌  An error occurred in Quark.

The context:  The server was trying to launch;
The error:    The port is configuration is missing;
What to do:   Please, add the port to a configuration;

Try following these steps:
    1.  Open the configuration file `D:/Quark Cloud/Configuration.json`
    2.  Find the `port` option (if it's not here, add it)
    3.  Set the `port` to any port you would like to use (I recommend to set it to 10000).

Doesn't work? Ask a question!
https://github.com/quark-database/cloud/issues
```