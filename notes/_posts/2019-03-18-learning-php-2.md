---
layout: post
title: 2. Setting Up a Development Server
description: >
image: 
categories: notes
---
**Learning PHP, MySQL & JavaScript**<br/>
Chapter 2. Setting Up a Development Server (-p.33)

## Why a Development Server?
* If I want to develop web applications, but don't have a development server, I will have to upload every modification to a server. This will slow down development time. 

### Advantages of Using a Development Server
* On a local computer, testing can be as easy as saving an update and hitting the refresh button on the browser.
* Don't have to worry about security problems during testing.

## What is WAMP, MAMP, or LAMP?
* WAMP: Windows, Apache, MySQL, and PHP
* MAMP: Mac, Apache, MySQL, and PHP
* LAMP: Linux, Apache, MySQL, and PHP

All these come in the form of packages that bind the bundled programs together so that I don't have to install and set them up separately. I can simply install a single program and follow instructions to get my web dev server up and running fast.

However, the security configs of such an installation will not be as tight as on a production web server, so this is only optimized for local use. I should never install such on a production server.

### Installing AMPPS on MacOS
I can use the already installed MAMP, but the book shows instructions for AMPPS, so just use AMPPS for now.

* Visit [AMPPS](https://www.ampps.com/downloads), download and install the software for Mac OS.
* Click the menu icon on the very left, change PHP version to 7.1
* The default document root is `/Applications/Ampps/www`. 
* Test by creating a small HTML file, test.html
* Enter localhost/test.html on the address bar
![installation](http://mocha.dothome.co.kr/images/190318-php-2-1.png)

## Working Remotely
* If I have access to a web server already configured with PHP and MySQL, I can always use that for my web dev. However, developing locally would be preferable, since I can test modification with no upload delay.
* To access MySQL, I need to use the secure SSH protocol to log into my server to manually create databases and set permissions from the command line. 

### Logging in
On a Mac, SSH is already available. Launch Terminal and log in to a server using SSH as follows:
`ssh mylogin@server.com`
server.com is the name of the server, and mylogin is the username I will log in under.

### Using FTP
To transfer files to and from web server, I need a FTP program. For now, use FileZilla.

### Using a code editor
There are a variety of code editors including Atom, VS Code, Brackets, Sublime Text, etc. For this book, I will stick with VS Code.

### Using an IDE
IDEs offer many additional features such as in-editor debugging and program testing, as well as function descriptions and much more. But for now, stick with VS Code.

Just for my information, these are the commonly used PHP IDEs.
* PHPStorm
* NetBeans
* PHPeclipse

## Questions
1. What is the difference between a WAMP, a MAMP, and a LAMP?
2. What do the IP address 127.0.0.1 and the URL http://localhost have in common?
3. What is the purpose of an FTP program?
4. Name the main disadvantage of working on a remote web server.
5. Why is it better to use a program editor instead of a plain-text editor?

