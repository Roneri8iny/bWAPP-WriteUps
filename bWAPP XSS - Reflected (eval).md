## What is Eval()?

The `eval()` method evaluates or executes an argument.
If the argument is an expression, `eval()` evaluates the expression. If the argument is one or more JavaScript statements, `eval()` executes the statements.

## Why shouldn't you use Eval()?

1. With eval(), malicious code can run inside your application without permission.
2. With eval(), third-party code can see the scope of your application, which can lead to possible attacks.

## Page Content:

On entering the page, we will see no input fields and the following message written:

>The current date on your computer is:
>Tue Mar 28 2023 20:25:59 GMT-0400 (Eastern Daylight Time)

So, we conclude that the webpage somehow gets the current date and time of the device you are logged in with.
On opening the page source we will see the following code snippet:

```javascript
<script>

    eval("document.write(Date())");

</script>
```

And we will notice that in the URL of the wepbage there is a Date() function that is being called, as follows:

> http://10.0.2.15/bWAPP/xss_eval.php?date=Date()

So, we can simply replace the part of the Date() function with alert("XSS") for example , as follows:

> http://10.0.2.15/bWAPP/xss_eval.php?date=alert(1)

And on pressing enter an alert box will appear with 1 in it.
So, we successfully managed to exploit the XSS vunerability in this webpage.