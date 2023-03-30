## First Phase:

There is a hint given to us which says:

>HINT: CVE-2012-5105

When searching this hint I found the following:

> CVE-2012-5105 is a vulnerability in SQLiteManager 1.2.4 that allows remote attackers to inject arbitrary web script or HTML via the `dbsel` parameter to (1) main.php or (2) index.php; or (3) `nsextt` parameter to index.php.

In the first page we a link that is written as SQLiteManger, so when we click on it, we are redirected to another webpage.

## Second Phase:

We view the source of the second webpage, we find a line in it that goes as follows:

```HTML
<frame src="main.php?" name="main" scrolling="auto">
```

And using the hint we got the vulnerability was exploited to inject script via the dbsel parameter to main.php, therefore we click on it.

## Third Phase:

We get another view source page then we can then remove the part of "view-source" from the URL to get the original page.

That leads us to another webpage that we can then use to insert a payload in the input field in it to exploit the XSS vulnerability.

## What is the dbsel parameter?

The `dbsel` parameter is used in SQLiteManager 1.2.0 and 1.2.4 to select a database from a list of databases. It is also used in a SQL injection vulnerability.

We want to inject an arbitary database so we want to match with any database name so we want to use the apostropho but not explicitly , that is whay we need to find its equivalent i HTML which is &#039 .

That means that our payload will look like this:

```javascript
?dbsel=&#039;"</script><script>alert(document.cookie)</script>
```

Then when we press save the cookies will be dispalyed in an alert box successfully.