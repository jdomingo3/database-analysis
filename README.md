<h1>Database Analysis</h1>

 ### [YouTube Demonstration](#)

<h2>Description</h2>
This database evaluation will demonstrate the fundamentals of databases by reviewing SQL statements, relational database design through normalization and ERD (entity relationship diagram). The entity relationship diagram will visually demonstrate the sample database’s transformation into 3NF (or 3rd normal form). Third normal form further reduces the disorder and dependencies which remain between the first and second normal form work.
<br />


<h2>Languages and Utilities Used</h2>

- <b>MySQL</b> 
- <b>SQL (Structed Query Language)</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> 

<h2>Analysis & Action Plan walk-through:</h2>

<p align="center">
<br /><b>Retrieve Data From a Database</b></p>
In this section, example SQL (structured query language) statements will demonstrate how to retrieve data from a database. <br /><br />
Table 1. Example SQL statements<br />
*The field BookAuthor in the Book table should be AuthorID, for there to be a relationship between the Author table and Book table. As the DBA in the scenario, I’ve taken the liberty to resolve the issue in order to proceed with Example 3. AuthorID will be the Primary Key in the Author table while AuthorID will be the Foriegn Key in the Book table.

| Ex #        | Query           | Result  |
| ------------- |:-------------| -----|
| 1     | SELECT * FROM Borrower; </br > ![alt text](https://i.imgur.com/y2PjqY9.png "Logo Title Text 1") | Select all borrowers |
| 2     | SELECT Book.BookTitle, Borrower.BorrowDate </br >FROM Book </br >INNER JOIN Borrower </br >ON Book.bookID = Borrower.bookID </br > ORDER BY Borrower.BorrowDate;</br > ![alt text](https://i.imgur.com/Xag9s8f.png "Logo Title Text 1") |   Select all books borrowed by borrowers, order by borrow date |
| 3 | SELECT Book.BookTitle, Author.AuthorFirstName, Author.AuthorLastName </br >FROM Book </br >INNER JOIN Author </br >ON Book.AuthorID = Author.AuthorID;</br > ![alt text](https://i.imgur.com/3cqXa5g.png "Logo Title Text 1") | Select all books and include the author first and last name |
| 4 | INSERT INTO Client VALUES ('7', 'Orville', 'Wright', '1921-03-06','Pilot');</br > ![alt text](https://i.imgur.com/YJ3Wtbq.png "Logo Title Text 1") | Insert a new client with an occupation of pilot |

<p align="center">
<br /><b>Database Normalization</b></p>
   In part 2, we will explore “the process of normalizing a database … which ensures that the tables within the database are organized and fit in with each other” (Third Normal Form in DBMS with Examples, 2020) by utilizing the miniature database supplied. The first step in accomplishing a third normal form database is to ensure it is already in 2NF (Second Normal Form). There are 3 steps in database normalization. Recall, the purpose of normalization is to reduce complexity.    <br /><br />
However, before proceeding to 2NF, we must ensure the database is already at 1NF. This means the following must be completed for 1NF to be reached: “All tables have a primary key, fields have unique names, data is not repeated across fields and there's no redundant data, like a field that is a combination of other fields” (First Normal Form in DBMS with Examples, 2020). <br /><br />
   In order to reach the third normal form, we will address redundancy and confusion. In the present, there are too many redundant and dependent attributes across the Produce, Animal Product and Grain tables such as: ITEMID, SUPPLIERID, TYPE, STOCKQTY, and NXTDELIVERY. A dependent attribute relies on another column and/or attribute.Therefore, it would be best to completely remove the three tables. To remove complexity PRODUCTNAME, will replace three attributes PRODUCENAME, ANPRDNAME, GRAINNAME in the new table.  <br /><br />

The following should be ran in order to remove the Produce, Animal Product and Grain tables with bad scructures from the minaturedb schema:
<br />DROP TABLE IF EXISTS produce, `animal test`, grain;

Next, a new table called “Item” will replace the previous Produce, Animal Product and Grain tables. The attributes for the new table called “Item” table will be: ITEMID, SUPPLIERID, CATEGORYID, PLUCODE, ITEMNAME, TYPE, STOCKQTY, NXTDELIVERY. (There is a new attribute/foriegn key CATEGORYID that will identify the product as Produce, Animal Product and Grain.) 

The SQL command for creating the new “Item” table is as follows:<br />
CREATE TABLE `tblalbum`.`item` (<br />
`ITEMID` INT NOT NULL AUTO_INCREMENT,<br />
`SUPPLIERID` INT NULL,<br />
`CATEGORYID` INT NULL,<br />
`PLUCODE` INT NULL,<br />
`ITEMNAME` VARCHAR(45) NULL,<br />
`TYPE` VARCHAR(45) NULL,<br />
`STOCKQTY` INT NULL,<br />
`NXTDELIVERY` DATE NULL,<br />
PRIMARY KEY (`ITEMID`));<br />

Then execute the following command to create a new “intermediate table” called Category with CATEGORYID as the primary key: <br />
CREATE TABLE `miniaturedb`.`Category` (<br />
  `CATEGORYID` INT NOT NULL AUTO_INCREMENT,<br />
  `CATEGORYNAME` VARCHAR(45) NULL,<br />
  PRIMARY KEY (`CATEGORYID`));<br />

Next, primary keys should be addressed. A primary key is a field or attribute that has a unique value for each tuple, entry or row. In other words, the data contained within can not be duplicated.  

We will add the PURCHASEID attribute to the Purchases table and set it to the primary key in order for the table to reach 2NF:<br />
ALTER TABLE `miniaturedb`.`purchases` <br />
ADD COLUMN `PURCHASEID` VARCHAR(45) NOT NULL AFTER `MARGIN`,<br />
ADD PRIMARY KEY (`PURCHASEID`);<br />

Overall, there may be times where achieving 3NF is near impossible but it should be a goal. For example, sometimes the 2NF version of the tables is easier to work with and therefore less complex, leading to the table being kept at a lower level of normalization. As Albert Einstein once said "Make everything as simple as possible, but not simpler."

<p align="center">
<br /><b>Entity Relationship Diagram</b></p>

Figure 1. Entity Relationship Diagram <br />
The following ERD depicts how to bring the database to 3NF.<br /><p align="center">
![alt text](https://i.imgur.com/nIKtCL5.png "Logo Title Text 1")</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
