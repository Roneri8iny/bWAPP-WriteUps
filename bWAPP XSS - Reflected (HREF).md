## First Page Content:

After opening the first page we will get an input field that requires a name,
after we enter the name then press enter, we get a message that says:

> Hello \<Name\>, please vote for your favourite movie.

Thus , we can see that the input that we entered was reflected in the next page, that means that this input field is the place that we will use to exploit the XSS vulnerability.

On the page where the input got reflected we view page source , we find the followinfg piece of code:

```javascript
<td align="center"> <a href=[xss_href-3.php? movie=1&name=Raneem&action=vote>Vote</a></td>
```

Since we have access to the part where the name is required then we must close the ">" and then insert our script then open the "<", as follows:

```javascript
><script> alert("XSS") </script><
```

So the code after injection will look like this:

```javascript
<td align="center"> <a href=[xss_href-3.php?movie=1&name=><script>alert("XSS")</script><&action=vote>Vote</a></td>
```

And then an alert box will appear with the message "XSS" in it.
Therefore, we successfully managed to exploit the XSS vulnerability.