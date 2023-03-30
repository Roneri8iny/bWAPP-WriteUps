## Page Content:

When we open the webpage we will see a drop-down menu that has three film genres;
action, horror and science fiction. Beside it there is a 'like' button. We can see that there are no input fields and based on the name of this bug we can guess that we will have to use burpsuite to solve this.

When we choose a movie genre then press the like button, we will see thst the request was interrupted. Now let us notice something about the request that was made. 

There is a part in the equest which tells us that there are three cookies, which is:

> Cookie: security_level=0; PHPSESSID=c7c802af852ff04134b2936991eba585; movie_genre=action

The part which seems to be of use the cookie named "movie_genre" we will see that it matches the movie genre we chose and liked.

So, let us try to change the movie genre in the GET part of the request with a genre that is not one of the three we already have:

+ The Request before Alterations:

> GET /bWAPP/xss_stored_2.php?__genre=action__&form=like HTTP/1.1

+ The Request after Alterations:

> GET /bWAPP/xss_stored_2.php?__genre=comedy__&form=like HTTP/1.1

We have swapped the action movie genre with comedy which is non-existent in the list of genres we were given.

Now, if we forward the request and open the inspect section of the webpage and go to the storage part, we will see that in the cookies section a new cookie with the value "comedy" was added which means that we have managed to exploit the XSS vulnerability in this webpage.