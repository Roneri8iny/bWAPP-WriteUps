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

