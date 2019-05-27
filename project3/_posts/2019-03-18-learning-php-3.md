---
layout: post
title: 3. Introduction to PHP
description: >
image: 
categories: notes
---
**Learning PHP, MySQL & JavaScript**<br/>
Chapter 3. Introduction to PHP (-p.62)

## Learning PHP
PHP is the language that you use to make the server generate dynamic output - output that is potentially different each time a browser requests a page.

In production, web pages will be a combination of PHP, HTML, JavaScript, and some MySQL statements laid out using CSS. For this chapter and on, let's focus on PHP only.

## Incorporating PHP within HTML
* By default, PHP files end with the extension `.php`. When a web server encounters this extention in a requested file, it automatically passes it to the PHP processor.
* Since web servers are highly configurable, some developers make .html files and force them to be parsed by the PHP processor to hide the use of PHP.

~~~php
<?php // Opening tag to trigger PHP commands
    echo "Hello world";
?> // Closing tag to end PHP commands
~~~

* Some programmers like to open the tag at the start and close it right at the end (says that the speed increase is so minimal that it doesn't justify the additional compleity of dropping in and out of PHP many times in a single file).
* Others choose to insert only in parts of the file (says that this style of coding results in faster code).
* This book adopted the approach of keeping the # of transfers between PHP and HTML to a minimum - only once or twice. But try to find my own style getting through the book.
* If I only have PHP code in a file, I can simply omit the closing `?>` tag. This ensures that I have no excess whitespace leaking from my PHP files, and this is important when I'm writing object-oriented code.

## The Structure of PHP

### Using Comments
Two ways to add commends to PHP code.
~~~php
// This is a single-line comment 
/* This is a section
    of multiline comments
    which will not be
    interpreted */
~~~
`//`: good way to temporarily remove a line of code from a program giving me errors (for debugging).
`/* */`: programmers use this to temporarily comment out entire sections of code that don't work. A common mistake is to use this to comment out already commented-out section. Comments can't be nested that way. 

### Basic Syntax
PHP is quite a simple language with roots in C and Perl, but looks more like Java. 

#### Semicolons
~~~php
$x += 10;
~~~
All PHP commands end with a ';(semicolon)'. One of the most common cause of erros while programming in PHP is forgetting semicolons. This results in a `Parse Error` message.

#### The $ Symbol
~~~
<?php
    $mycounter = 1;
    $mystring = "Hello";
    $myarray = array("One", "Two", "Three");
?>
~~~
In PHP, '$' should be placed in front of all variables. 

### Variables
Think of PHP variables as matchboxes - matchboxes with names written on.

#### String variables
~~~php
$username = "Fred Smith";
echo $username;
$current_user = $username;
~~~
* Here, we are placing "Fred Smith" in the username box.
* The quotation marks indicate that Fed Smith is a string of characters.
* Strings must be enclosed by either quotation marks or apostrophes (single quotes). There's a subtle difference between these two to be discussed later.
* I can print out the variable on the screen with `echo` command, or assign it to another variable.

Variable naming rules!
* Variable names after the dollar sign, must start with an alphabet or the _ (underscore) character.
* Variable names can contain only the characters a-z, A-Z, 0-9, and _ (underscore).
* Variable names may not contain spaces. If a variable name comprise more than one word, include _ (underscore) in between the words.
* Variable names are case-sensitive.

#### Numeric variables
Variables can contain numbers too. 
~~~php
$count = 17; // integer
$count = 17.5 // floating-point number (containing a decimal point)
~~~

#### Arrays
![array](http://mocha.dothome.co.kr/images/190319-php-1.png)

Arrays can be considered as several matchboxed glued together, with the word 'team' covering the set.

~~~php
$team = array('Jonghyun', 'Youngmin', 'Dongho', 'Minhyun', 'Minki');
echo $team[3]; // Displays the name Chris
~~~
* The array-building code consists of the following construct: `array();`.
* Each string is enclosed in apostrophes, and they must be separated by commas.
* The first element in a PHP array starts at index of 0. 

#### Two-dimensional arrays
![array](http://mocha.dothome.co.kr/images/190319-php-2.png)
~~~php
<?php
    $oxo = array(array('x', ' ', 'o'),
                array('o', 'o', 'x'),
                array('x', 'o', ' '));
?>
echo $oxo[1][2]; // Displays 'x'
~~~
* Three array() constructs nested inside the outer array() construct.

### Operators
~~~php
echo 6 + 2;

45p