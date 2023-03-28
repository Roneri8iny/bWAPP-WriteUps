## Contents of the Login Form:

There are two input fields; one for to input a username and the other one is to input a password. All this plus a confirm button.

## First Trial:

First thing, like anyone would probably do, I tried entering common usernames and passwords, but of course as I had predicted it did not work out.

## Second Trial:

I then tried to enter a script that is divided on both fields in order to concatenate both when the button is pressed, but I got the response:

> Wrong Password

## Third Trial:

After this, I tried entering a single quote in the field of the of the username in order to  see if the SQL command that the data is selected by will raise a syntax error.
Fortunately, it did give me the message:

> *Error: You have an error in your SQL syntax check the manual that corresponds to your MySQL server version for the right syntax to use near "" AND password="" at line 1

That means that that single quote ruined the syntax of the SQL command, that means that we have to put the single quote somehow in the script that we are going to use to exploit the XSS vulnerability.
So in the username field I put the SQL command:

```MySQl
SELECT uname="" & password="" OR 1=1 from users';
```

Notice the single quote at the end of the command.

And in the password field I put the script:

```javascript
'<script> alert("XSS")</script>
```

And we notice that the single quote is used before the script in order to somewhat decieve the webpage.

And, thankfully, an alert box with the message "XSS" in it, so that means we have managed to exploit the XSS vulnerability in the webpage.
