# Project 5: Web Crawler
## High Level Approach
## Challenges
### Logging In
The first major issue that we encountered was logging in. This was 
particularly challenging because
### Chunked Encoding
Chunked encoding was initially an issue because we weren't exactly sure how 
to ensure that we read the hexadecimal based length field and then ignore 
the unneeded data after the semicolon. Also, another issue arose when we 
didn't even know if we had to use chunked encoding; namely we didn't check 
the header field. After we discovered that, we made a fairly rudimentary 
transfer encoding parser that took every other line until a "0" showed up in 
an even numbered line. Then that would just be our "body"; primarily html.
## Testing
For testing, we primarily ran our code against the server. Like previous 
projects, when we could we added the code to a separate file and manually 
tested the code with mock data. For instance, with chunked-encoding, to 
ensure that we were parsing the chunked data correctly, we first wrote that 
code segment in a separate file and then fed that mock data. Mock data was 
gathered from the following links: 
[HTTP Made Easy](https://www.jmarshall.com/easy/http/#http1.1c2) and 
[Mozilla](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Transfer-Encoding). 
