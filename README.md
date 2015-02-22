# What Happens ...

1. **hackbulgaria.com** is typed in a browser.

2. If it is in the browser cache and is fresh, move on to 8.

3. DNS lookup to find the ip address of the hackbulgaria.com server.
When we want to connect to hackbulgaria.com, we actually want to reach out to a server where hackbulgaria is hosted. This server has an ip address of 178.62.181.165. Now, if you type "http://178.62.181.165" in your browser, this will take you to the hackbulgaria.com home page itself. Which means, "http://hackbulgaria.com" and "http://178.62.181.165" are nothing but the same thing.  
*Following is a summary of steps happening while DNS service is at work:*  
**Check browser cache:** browsers maintain cache of DNS records for some fixed duration. So, this is the first place to resolve DNS queries.  
**Check OS cache:** if browser doesn't contain the record in its cache, it makes a system call to underlying Operating System to fetch the record as OS also maintains a cache of recent DNS queries.  
**Router Cache:** if above steps fail to get a DNS record, the search continues to your router which has its own cache.
**ISP cache:** if everything fails, the search moves on to your ISP. First, it tries in its cache, if not found - ISP's DNS recursive search comes into picture. DNS lookup is again a complex process which finds the appropriate ip address from a list of many options available for large websites like Google.

4. Browser initiates a TCP connection with the server.

5. Browser sends an HTTP request to the server.
Browser sends a GET request to the server according to the specification of HTTP(Hyper Text Transfer Protocol) protocol. 
        
    ```html
    GET https://hackbulgaria.com/ HTTP/1.1
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:29.0) Gecko/20100101 Firefox/29.0
    Accept-Encoding: gzip, deflate
    Connection: Keep-Alive
    Host: hackbulgaria.com
    Cookie: datr=1241255234-[...]; locale=bg_BG; lsd=WW[...]; c_user=2401[...]
    ```  

    Here, browser passes some meta information in the form of headers to the server along with the URL - "https://hackbulgaria.com/". User-Agent header specifies the browser properties, Accept-Encoding headers specify the type of responses it will accept. Connection header tells the server to keep open the TCP connection established here. The request also contains Cookies, which are meta information stored at the client side and contain previous browsing session information for the same website in the form of key-value pairs e.g. the login name of the user.

6. Server handles the incoming request
HTTP request made from browsers are handled by a special software running on server - commonly known as web servers e.g. Apache, IIS etc. Web server passes on the request to the proper request handler - a program written to handle web services e.g. PHP, ASP.NET, Ruby, Servlets etc.  
For example URL- http://edusagar.com/index.php is handled by a program written in PHP file - index.php. As soon as GET request for index.php is received, Apache(our webserver at edusagar.com) prepares the environment to execute index.php file. Now, this php program will generate a response - in our case a HTML response. This response is then sent back to the browser according to HTTP guidelines.

7. Browser receives the HTTP response like in the example below.

    ```html 
    HTTP/1.1 200 OK
    Cache-Control: private, no-store, no-cache, must-revalidate, post-check=0, pre-check=0
    Expires: Thu, 19 Nov 1981 08:52:00 GMT
    Pragma: no-cache
    Content-Encoding: gzip
    Content-Type: text/html; charset=utf-8
    Connection: Keep-Alive
    Content-length: 1215
    Date: Fri, 20 Feb 2015 08:10:15 GMT  
    <!doctype html>
    <!--[if IE 9]><html class="lt-ie10" lang="en" > <![endif]-->
    <html class="no-js" lang="en" data-useragent="Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Trident/6.0)">
    <head>
      <meta charset="utf-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <meta name="google-site-verification" content="DkTcmszC1e0sdN6JOyAvdeyIYi3_YV0JTf4HTVZVfd4" />
      <link rel="shortcut icon" href="/static//img/favicon.ico">
  
  <title>HackBulgaria - Курсове по програмиране</title>
  .....................................................
  .....................................................
  .....................................................
    ```
  *HTTP response starts with the returned status code from the server. Following is a very brief summary of what a status code denotes:*
  - 1xx indicates an informational message only
  - 2xx indicates success of some kind
  - 3xx redirects the client to another URL
  - 4xx indicates an error on the client's part
  - 5xx indicates an error on the server's part  

  *Server sets various other headers to help browser render the proper content.*
  - Content-Type: tells the type of the content the browser has to show 
  - Content-length: tells the number of bytes of the response. 
  - Content-Encoding: tells the browser how to decode the blob data present at the end of the response.

8. Browsers displays the html content
Rendering of html content is also done in phases. The browser first renders the bare bone html structure, and then it sends multiple GET requests to fetch other hyper linked stuff e.g. If the html response contains an image in the form of img tags such as ``` <img src="/assets/img/logo.png" /> ```, browser will send a HTTP GET request to the server to fetch the image following the complete set of steps which we have seen till now. But this isn't that bad as it looks. Static files like images, javascript, css files are all cached by the browser so that in future it doesn't have to fetch them again.      
9. Client interaction with server
Once a html page is loaded, there are several ways a user can interact with the server. For example, he call fill out a login form to sign in to the website. This also follows all the steps listed above, the only difference is that the **HTTP** request this time would be a **POST** instead of **GET** and along with that request, browser will send the form data to the server for processing (username and password in this case).          
Once server authenticates the user, it will send the proper **HTML** content(may be user's profile) back to the browser and thus user will see that new webpage after his login request is processed.

10. AJAX queries
Another form of client interaction with server is through AJAX(Asynchronous JavaScript And XML) requests. This is an asynchronous GET/POST request to which server can send a response back in a variety of ways - json, xml, html etc. AJAX requests doesn't hinder the current view of the webpage and work in the background. Because of this, one can dynamically modify the content of a webpage by calling an AJAX request and updating the web elements using Javascript.

#### Sources used: [Edusagar] and [Pyechonest] just for the cat image.
[Edusagar]: http://edusagar.com/
[Pyechonest]: https://github.com/echonest/pyechonest/

-![alt text](http://i.imgur.com/WWLYo.gif "Frustrated cat can't believe this is the 12th time he's clicked on an auto-linked README.md URL")
