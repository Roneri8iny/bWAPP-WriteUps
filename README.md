# bWAPP-WriteUps

The purpose of this repo is to go through some of the bWAPP bugs in both XSS and SQL Injection.

## XSS:

Fisrt of all, we will go through some stored and reflected XSS.

### What is Reflected XSS?

It is a type of security vulnerability that allows an attacker to inject malicious code into a web page viewed by other users. This can be done by injecting code into a web page that is then executed by the user’s browser. Reflected XSS attacks are often used to steal sensitive information such as login credentials or credit card numbers.
Mostly, we are looking for an input field or any thing else that when we enter an input in it reflects somewhere in the webpage.

### What is Stored XSS?

It is a type of security vulnerability that allows an attacker to inject malicious code into a web page that is then stored on the server and viewed by other users. This can be done by injecting code into a web form or other input field that is then stored in a database and displayed to other users. Stored XSS attacks are often used to steal sensitive information such as login credentials or credit card numbers. We are basically looking for a place where the input to the webpage gets stored in the database, such as comments section or cookies etc.

## SQL Injection:

### What is SQL Injection ?

It is a type of security vulnerability that allows an attacker to execute malicious SQL statements that control a web application’s database server. This can be done by injecting SQL code into a web form or other input field that is then executed by the database server. SQL Injection attacks are often used to steal sensitive information such as login credentials or credit card numbers.

### What do we aim to get from a SQL Injection Attack?

Here are some things that we can try to know about the database through SQL Injection:

1. Database Version
2. User of the Database
3. Usernames & passwords if the webpage has those
4. Table Names 

