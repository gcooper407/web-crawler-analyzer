# Project 5: Web Crawler
## High Level Approach
Our program first traverses to the main page of Fakebook to gather the
necessary cookies (csrf token and session id) and then passes that to the login
page which passes that token along with login information over to the login
page. From there, we keep track of the session id and csrf token and pass
those cookies to the requests whenever scraping a page. And then on the
web-scraping portion, we use HTMLParser (from `html.parser`) to search for
`<a>` tags indicating a link, we add that link to a `set` of links if we
have not already traversed it. Then on that page we also look out if there
is a flag, essentially any data that contains the format for a flag `FLAG:
xxxx--`, if so, add to flags. And then just continue till 5 flags are found.

While we did attempt to implement multithreading, we were unable to accomplish
it within the assignment timeframe.
## Challenges
### Logging In
The first major issue that we encountered was logging in. This was
particularly challenging because while we knew that we had to send some sort
of 'payload' to get the login information through, we were not sure how to
go about that. What proved to be really helpful in this situation was using
[Postman](https://www.postman.com/) to formulate how the initial few
requests would go. For instance, I first tested with just sending a request
to 'https://www.3700.network/fakebook' to see what we would get back (just
the general format of the data). From there, I tested with a post request at
'https://www.3700.network/accounts/login' with the body being a
'x-www-form-urlencoded' with the username, password, and csrfmiddlewaretoken
attached. I found how out to include these fields from viewing the 'payload'
portion of the network tab (inspect element). It became obvious on how to
approach the sending of the form data after viewing the code snippet for
HTTP requests in Postman.
### Chunked Encoding
Chunked encoding was initially an issue just because of how rare a chunked
encoding segment was, we weren't exactly sure how to ensure that we read the
hexadecimal based length field and then ignore the unneeded data after the
semicolon. Also, another issue arose when we didn't even know if we had to
use chunked encoding; namely we didn't check the header field. After we
discovered that, we made a fairly rudimentary transfer encoding parser that
took every other line until a "0" showed up in an even numbered line. Then
that would just be our "body"; primarily html.
## Testing
For testing, we primarily ran our code against the server. Like previous
projects, when we could we added the code to a separate file and manually
tested the code with mock data. For instance, with chunked-encoding, to
ensure that we were parsing the chunked data correctly, we first wrote that
code segment in a separate file and then fed that mock data. Mock data was
gathered from the following links:
[HTTP Made Easy](https://www.jmarshall.com/easy/http/#http1.1c2) and
[Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding). 
