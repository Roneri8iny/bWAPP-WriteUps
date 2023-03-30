## Initial Trial:

First thing, I tried entering a single quote in the input field to see the behaviour of the webpage. After entering it, a message with an error was returned which said:

>Error: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '%'' at line 1

So, in order to overcome this, I used the single quote together with the commenting in MySQL to formulate the next line of code:

```MySQL
' order by 1-- -
```

This orders the response table according to the number of column supplied, so I then tried incrementing the number 1 by 1 in order to know the number of columns in the table. On the 8th trial, the following error occured:

> Error: Unknown column '8' in 'order clause'

Which means that the table has 7 columns.

After that we have to know which columns of the seven that are in the table are displayed to us. So we can do this using the following line:

```MySQL
iron’ union select 1,2,3,4,5,6,7– –
```

This will lead to a table that has the numbers of columns that we are able to see.

Which shows that we can see the 2nd, 3rd, 5th and 4th columns.

Then we can use one of the columns to display any desired data of related to the database. WE can get to know the user of the database using the following line:

```MySQL
iron' union select 1, user() , 3,4,5,6,7-- -
```

We can see that we want to display the result in the second column which is te first one in the columns that are displayed to us.

We can see in the first column that the user is called root@localhost.

## What is information_schema?

The `information_schema` is a database that stores metadata about all other databases on that server instance. It contains read-only views that we can query for information.
It provides access to database metadata, information about the MySQL server such as the name of a database or table, the data type of a column, or access privileges.
Now we can use it to know more information about the database.
First, we can get names of the tables in the database using the following line:

```MySQL
iron' union select 1,table_schema,table_name,4,5,6,7 from information_schema.tables-- -
```

This gives us a table with all the table names and the databases the database schemas they elong to.

We can see that the database which is called bWAPP has a table in it that is called users which by using common sense leads us to think that this table could have the usernames and hopefully the password of the users, so we can pursue that table.

We can use the following line to explore that table:

```MySQL
iron' union select 1,table_name,column_name,4,5,6,7 from information_schema.columns where table_schema = 'bWAPP' and table_name = 'users'-- -
```

This gives a table which has the name of all the columns in the users table.

Now we have all the information we need to know all the users' sensitive data and we can do just that by using the following line:

```MySQL
iron' union select 1,login,password,email,admin,6,7 from users-- -
```

This gives a table that has the username, password, email and admin of each user in the table.

Now, we have successfully managed to exploit the SQL Injection vulnerability in this webpage.