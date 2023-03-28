# First Trial:

First thing we see is two input fields that require first name and second name to be entered, so I tried entering names as required to see the usual behaviour of the webpage. 
The output was in the format: 

>*Welcome  \<First name\> \<Last name\>*

# Second Trial:

After seeing the behaviour of the webpage, I tried leaving one of the two required fields empty to see the response.
The response was that there is Invalid Input because both fields are required.

# Third Trial:

I tried some scripts to see if a response will be returned, so I wrote the following script:

```javascript
<script> alert("XSS") </script>
```

The result I got is an alert box with the message "XSS" in it, so we exploited the XSS vulnerability in this webpage.



