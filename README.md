# Day10-MySql-Company-simple-db
## [In this lab we implemented the following Rational model.](https://docs.google.com/document/d/1zAr0oeCErP4PWxdaBg-X9PjBfVA9Fy5Yk2GBP2UzjZw/edit)

### How I created it using command line:
- Download [xampp](https://www.apachefriends.org/index.html).
- Start Xampp.
- In browser go to [php my admin](http://localhost/phpmyadmin/).
- Now open sql tab and create new database.

  ```sql
  CREATE DATABASE Company
  ```
- Create tables (Employee, Department, Dept_Locations, Project, Works_On, Dependent)  if not exist.

  ```sql
  CREATE TABLE if not EXISTS Employee(
      pname VARCHAR(50),
      minit VARCHAR(50),
      lname VARCHAR(50),
      ssn INT PRIMARY KEY AUTO_INCREMENT,
      bdate VARCHAR(50),
      address VARCHAR(50),
      gender ENUM('male', 'female'),
      dno int,
      superssn int
  );

  CREATE TABLE if not EXISTS Department(
      dname varchar(50),
      dnumber int PRIMARY KEY AUTO_INCREMENT NOT NULL,
      mgrssn int,
      msgStartDate varchar(50)    
  );

  CREATE TABLE if not EXISTS Dept_Locations(
      dnumber int,
      dlocation varchar(50) NOT NULL,
      CONSTRAINT pkey PRIMARY KEY (dnumber, dlocation)
  );


  CREATE TABLE if not EXISTS Project(
      pname varchar(50),
      pnumber int PRIMARY KEY AUTO_INCREMENT  NOT NULL,
      plocation varchar(50),
      dnum int
  );


  CREATE TABLE if not EXISTS Works_On(
      essn int,
      pno int,
      hours int,
      CONSTRAINT pkey PRIMARY KEY (essn, pno)  
  );


  CREATE TABLE if not EXISTS Dependent(
      essn int,
      dependent_name varchar(50),
      gender ENUM('male','female'),
      bdate varchar(50),
      relationship varchar(50),
      CONSTRAINT pkey PRIMARY KEY (essn, dependent_name)
  );
  ```
  
- Now we need to add FOREIGN KEYS and create COMPOSITE PRIMARY KEY for tables.
  
  ```sql
  alter table Employee add FOREIGN KEY (superssn) REFERENCES  Employee(ssn);

  alter table Employee add FOREIGN KEY (dno) REFERENCES Department(dnumber);

  alter table Department add FOREIGN KEY (mgrssn) REFERENCES Employee(ssn);

  alter table Dept_Locations add FOREIGN KEY (dnumber) REFERENCES Department(dnumber);

  alter table Project add FOREIGN KEY (dnum) REFERENCES Department(dnumber);

  alter table Works_On add FOREIGN KEY (essn) REFERENCES Employee(ssn);

  alter table Works_On add FOREIGN KEY (pno) REFERENCES Project(pnumber);

  alter table Dependent add FOREIGN KEY (essn) REFERENCES Employee(ssn);

  ```
