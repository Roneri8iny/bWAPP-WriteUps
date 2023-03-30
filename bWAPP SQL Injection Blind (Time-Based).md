
## What is Blind SQL Injection?

Blind SQL injection is a type of SQL injection attack that asks the database a series of true or false questions to steal data when the database does not output data to the web page. It arises when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the relevant SQL query or the details of any database errors.

So, knowing these pieces of information we can guess that we won't be able to see the result of any payload of the usual ones that usually give us an output that we can use to our benefit. 
That means that our only hope is using a function that somehow delays the response for us to say that we have managed to solve this one.

There is a function in MySQL that does this and that is sleep( ), it takes time as an argument and this time is in seconds.

```MySQL
iron' or 1=(select sleep(2));#
```

The effect of this payload once entered will be noticed when we look at the tab we are working in and see that is buffering for a considerably long period of time.