# Web Crawler
## High Level Approach
This program first traverses to the main page of the social media page to gather the
necessary cookies (csrf token and session id) and then passes that to the login
page which passes that token along with login information over to the login
page. From there, it keeps track of the session id and csrf token and pass
those cookies to the requests whenever scraping a page. And then on the
web-scraping portion, it uses HTMLParser (from `html.parser`) to search for
`<a>` tags indicating a link, adding that link to a `set` of links if it
has not already traversed it.


## Challenges
### Logging In
The first major issue that arose was logging in. This was
particularly challenging because while it was clear that it was necessary to send some sort
of 'payload' to get the login information through, it was unclear exactly how to
go about that. What proved to be really helpful in this situation was using
[Postman](https://www.postman.com/) to formulate how the initial few
requests would go. For instance, I first tested with just sending a request
to 'https://www.3700.network/fakebook' to see what would get sent back (just
the general format of the data). From there, I tested with a post request at
'https://www.3700.network/accounts/login' with the body being a
'x-www-form-urlencoded' with the username, password, and csrfmiddlewaretoken
attached. I found how out to include these fields from viewing the 'payload'
portion of the network tab (inspect element). It became obvious on how to
approach the sending of the form data after viewing the code snippet for
HTTP requests in Postman.

### Chunked Encoding
Chunked encoding was initially an issue just because of how rare a chunked
encoding segment was, I wasn't exactly sure how to ensure that the program read the
hexadecimal based length field and then ignore the unneeded data after the
semicolon. Also, another issue arose when I didn't even know if chunked encoding
was necessary; namely I didn't check the header field. After discovering that, 
I made a fairly rudimentary transfer encoding parser that took every other line 
until a "0" showed up in an even numbered line. Then that would just be the "body"; 
primarily html.

## Testing
Testing consisted primarily trial and error, running the code incrementally against the server
in order to determine what the next required step to implement would be. When possible,
I added the code to a separate file and manually tested the code with mock data. 
For instance, with chunked-encoding, to ensure that the program was parsing the chunked data 
correctly, I first wrote that code segment in a separate file and then fed that mock data.
Mock data was gathered from the following links:
[HTTP Made Easy](https://www.jmarshall.com/easy/http/#http1.1c2) and
[Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding). 
