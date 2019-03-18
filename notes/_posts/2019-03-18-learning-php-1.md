---
layout: post
title: 1. Introduction to Dynamic Web Content
description: >
image: 
categories: notes
---

Learning PHP, MySQL & JavaScript<br/>
Chapter 1. Introduction to Dynamic Web Content (-15p)

## Internet History
* Early 1910s, CERN were producing incredible amounts of data hard to distribute to the scientists around the world.
* The internet was already in place at the time, connecting several hundred thousand computers. The most connectivity experienced by home modem users was dialing up and connecting to a bulletin board hosted by a single computer, where you could communicate and exchange data only with other users of that service.
* Tim Berners-Lee (a CERN fellow) devised a method of navigating between them using a hyperlinking framework - **Hypertext Transfer Protocol (HTTP)**, and invented a markup language called **Hypertext Markup Language (HTML)**.
* With these technologies, he created the first web browser and web server.
* In this chapter, we look at the various components that make up the web, and the software that helps using it a rich and dynamic experience.

## HTTP and HTML: Berners-Lee's Basics
* HTTP is a communication standard governing the requests and responses sent between the browser on the end user's computer and the web server.
* The server accepts requests from the client and attempts to reply, usually by serving up a requested web page (reason why it's called a server).
* Between the client and the server - routers, proxies, gateways, etc.
* These devices serve different roles ensuring that the requests and responses are correctly transferred between the client and server.
* These transfers can become more speedy by storing information locally in cache and serving them up.
* Web server handles multiple connections, spends its time listening for an incoming connection and sending back responses.

## The Request/Response Procedure
The request/response process consists of a web browser(requests and displaying) and the server(sends).

### Non-dynamic Web Pages
![web](http://mocha.dothome.co.kr/images/190318-php-1.png)
1. Enter the address into the browser's address bar.
2. Browser looks up the Internet Protocol(IP) address for mochastudy.github.io. (Every machine attached to the internet has an IP address, including my own computer. However, we generally access web servers by name, which is called DNS (ex. mochastudy.github.io), to find the server's associated IP address and, uses it to communicate with the computer).
3. Browser sends a request for the home page at mochastudy.github.io.
4. The request crosses the internet and arrives at the mochastudy.github.io web server.
5. The web server, having received the request, looks for the web page on its disk.
6. The web server retrieves the page and returns it to the browser.
7. Browser displays the web page.

### Dynamic Web Pages
For dynamic web pages, the procedure is little more involved (including PHP, MySQL, etc.)
![web](http://mocha.dothome.co.kr/images/190318-php-2.png)
1. mocha.dothome.io entered into browser's address bar.
2. Browser looks up the IP address for mocha.dothome.io.
3. Browser issues a request to that address.
4. The request crosses the internet and arrives at mocha.dothome.io web server.
5. The web server, having received the request, fetches the home page from its hard disk.
6. With the home page now in memory, the web server notices that it is a file incorporating PHP scripting and passes the page to the PHP interpreter.
7. The PHP interpreter executes the PHP code.
8. Some of the PHP contains SQL statements, which the PHP interpreter now passes to the MySQL Database engine.
9. The MySQL database returns the results of the statements to the PHP interpreter.
10. THE PHP interpreter returns the result of the executed PHP code, along with the results from the MySQL database, to the web server.
11. The web server returns the page to the requesting client, which displays it.

## Components
### MariaDB: The MySQL Clone
After Oracle purchased Sun Microsystems (the owners of MySQL), the community became wary that MySQL might not remain fully open source, so MariaDB was forked from it to keep it free under the GNU GPL. 
* Developed by some of the original developers of MySQL. 
* Based on the same code base as MySQL Server 5.5, so it's highly compatible with MySQL.

### Using PHP
* With .php extension, they have instant access to the scripting language.
* `<?php>` tells the web server to allow the PHP program to interpret all the code up to the `?>`.
* Outside of these opening and closing tag, everything is sent to the client as direct HTML.
* With PHP, developers have a scripting language that is incredibly speedy and integrates seamlessly with HTML markup.

### Using MySQL
* In the early days, many sites used flat text files to store data such as usernames and passwords. This can cause problems if the file wasn't correctedly locked against corruption. Also, this can get so big to manage. -> Need for relational databases with structured querying
* MySQL is a robust and exceptionally fast database management system that uses English-like commands.
* There are a lot of things you can do with MySQL (combining related data sets to bring related pieces of info together, ask for result in different orders, etc.).

### Using JavaScript
* Created to enable scripting access to all the elements of an HTML document.
* Dynamic user interaction (checking email address validity, displaying prompts...).
* These days, it's also used for asynchronous communication, the process of accessing the web server in the background.
* Asynchronous communication is what allows web pages to begin to resemble standlone programs, because they don't have to be reloaded in their entirety to display new content. An asynchronous call can pull in and update a single element on a web page.

### Using CSS
* CSS3 offers a level of dynamic intereactively previously supported only by JavaScript (Annimated transitions and transformations...).

### Using HTML5
* HTML5's developement began as long ago as 2004, when the first draft was drawn up by the Mozilla Foundation and Opera Software. In 2013, the final draft was submitted to the World Wide Web Consortium (W3C), the international governing body for web standards.
* New features in HTML5 include `<audio>, <video>, <canvas>`...
* With previous versions of HTML, closing / character was to be included in the self-closing tags, but now I can use either `<br>` or `<br/>`.

### Apache Web Server
* In addition to PHP, MySQL, JavaScript, CSS, and HTML5, there's also the web server (In this book, the Apache Web Server).
* Apache doesn't only serve up HTML files, it also handles a wide range of files including images, audio files, RSS feeds, etc.
* These objects don't have to be static files. They can all be generated by programs such as PHP scripts. To do this, we need modules either precompiled into Apache/PHP or called up at runtime. One such module is GD (Graphic Draw) library, which PHP uses to create and handle graphics.
* Apache also supports a huge range of modules in addition to the PHP module, such as the Security module, Rewrite module, Proxy module,...

### Handling Mobile Devices
* Concept of developing websites solely for desktop computers has become rather dated. 
* In this book, we will look at jQuery Mobile library to create web apps.

### Bringing It All Together
* PHP, MySQL, JavaScript, CSS, and HTML5 all work together to produce dynamic web content.
* PHP handles all the main work on the web server.
* MySQL manages all the data.
* CSS looks after the web page presentation and overall design.
* JavaScript handles interactivity and also talk with PHP code whenever it need to update something.
* HTML5 manages the structure of the website and the new features of HTML5(canvas, audio, video, etc.) can help you make your web pages highly dynamic, interactive, and multimedia-packed.

## Wrapping up
![web](http://mocha.dothome.co.kr/images/190318-php-3.png)
1. Server outputs the HTML to create the web form
2. At the same time, the server attaches some JavaScript to the HTML to monitor the username input box and check for two things: whether some text has been typed into it, and whether the input has been deselected because the user has clicked on another input box.
3. Once the text has been entered and the field deselected, in the background the JaVascript code passes the username that was entered back to a PHP script on the web server and awaits a response.
4. The web server looks up the username and replied back to the JavaScript regarding whether that name has already been taken.
5. The JavaScript then places an indication next to the username input box to show whether the name is available to the user - perhaps a green checkmark or a red cross graphic, along with some text.
6. If the username is not available and the user still submits the form, the JavaScript interrupts the submission and reemphasizes
7. Optionally, an improved version of this process could even look at the username requested by the user and suggest an alternative that is currently available.

## Questions
1. What four components (at the minimum) are needed to create a fully dynamic web page?
2. What does HTML stand for?
3. Why does the name MySQL contains the letters SQL?
4. PHP and JavaScript are both programming languages that generate dynamic results for web pages. What is their main difference, and why would you use both of them?
5. What does CSS stand for?
6. List three major new elements introduced in HTML5.
7. If you encounter a bug (which is rare) in one of the open source tools, how do you think you could get it fixed?
8. Why is a framework such as jQuery Mobile so important for developing modern websites and web apps?
