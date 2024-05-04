<p align="center">
    <a href="https://anafro.ru/quark">
        <img src="https://raw.githubusercontent.com/quark-database/.github/main/Assets/Banner.png" alt="Quark Banner">
    </a>
</p>

<h1 align="left">About Quark Documentation</h1>

The Quark Documentation describes not the actual implementation of Quark, but the specification of Quark products. Effectively this is a set of guidelines about how to create your own Quark!

<details open>
<summary><kbd>Table of contents</kbd></summary>


1. [📚 Database Management Specification](#database-management-specification)
    -  [The capitalized case](#the-capitalized-case)
    -  [Databases](#databases)
    -  [Tables](#table)
    -  [Table records](#table-records)
    -  [Table header](#table-header)
    -  [Records](#records)
2. [✍️ Query Language Specification](#query-language-specification) 


</details>

<h2 id="database-management-specification">📚 Database Management Specification</h2>

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

**The table header file** contains names of the table column and their types. Each line of table header contains the type, name, and the modifiers of the columns. The modifier list can be empty.

```
// Header.qhead:
int("Id", incrementing)
str("Name")
int("Age", positive)

int                                         ("Id",                                  incrementing)
^                                            ^                                      ^
| Type of column (here, it is integer)       | The column name (here, it is Id)     | The list of modifiers (here, it is one modifier: incrementing)
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

<h2 id="database-management-specification">✍️ Query Language Specification</h2>

> [!CAUTION]
> 🚧 The query language specification will soon be defined.