---
layout:     post
title:      Elementary Web Development
author:     Allan Berry
date:       2016-09-24
slug:       intro-web-dev
categories: webdev tutorial html css javascript
---


Introduction to Web Development: <br>Concepts and a Basic Infrastructure
===

A simple, quality setup for web pages from scratch, using free software and Web standards.

Virtually every website in existence uses these basic concepts and technologies, although usually with greater sophistication.  You can apply skills employed here to the Web more broadly; after this, it's just specialization.

![Here's a fuzzy cat.  Please move along.](/static/{{ page.slug }}/test_cat.jpg "Just a fuzzy cat.  Please move along."){:width="1200px"}

## Requirements

### A Macintosh computer (probably)

The examples below have been tested on a Mac.  Using Linux should be quite similar; using Windows may work as well, but I don't know much about Windows, so you may have some extra work ahead.

### A terminal prompt

On a Mac, "Terminal.app" is available in your Utilities folder, inside of your usual Applications folder.

### A Web browser

I recommend the latest version of [Google Chrome](https://www.google.com/chrome/).

If you can't use Chrome, the latest versions of [Firefox](https://www.mozilla.org/en-US/firefox/new/) or [Safari](http://www.apple.com/safari/) will work, but you will need to figure out how their interfaces differ from the examples.  It's probably not a big deal though.

If you use Firefox, you may need to install the [Firebug](http://getfirebug.com/) extension.  If you use Safari, the Developer tools come in handy; if you don’t see the Develop menu in the menu bar, choose `Safari` ➙ `Preferences`, click `Advanced`, then select `Show Develop menu in menu bar`.

### A text editor

Pretty much all Web work happens in a text editor, so you should find one you like, and learn to use it.  Here are some good free options:

[Atom](https://atom.io/)
: Created by GitHub, the darling of Silicon Valley, Atom is supremely powerful and cool.

[Brackets](http://brackets.io/)
: Started by Adobe, the Brackets project is designed specifically for Web developers.

[Sublime Text](https://www.sublimetext.com/)
: Not technically free, but it's great, and you can use it for free for as long as you want.  I use it.

![A screenshot of my Sublime Text window, with a few customizations.  <br>This is the final code state of the short exercise below.](/static/{{ page.slug }}/screenshot_2.png "Screenshot of Sublime Text")

It doesn't really matter which editor you use, and there are others out there as well.  Just don't use Microsoft Word.


## Basic concepts and technologies

The internet is something like a conversation among computers.  The Web might be one such conversation: one computer requesting something from another, and receiving a response in return, often a webpage.  Following are some terms to help understand this conversation.


Client
:   A client is the computer doing the asking.

    In the parlance of the Web, however, the "client" usually specifically refers to the Web browser _on_ the client computer.  So when you read "client", think "Firefox" or "Chrome".


Server
:   A server is the computer providing the goods.

    This will get a bit confusing later in this exercise, because we will implement both the client and the server on a _single_ computer: our desktop or laptop or whatever.  This machine will be both client and server: a single computer asking itself for stuff.

    While confusing at first, the client/server distinction allows us to provide access to other computers, or to eventually move our server to another computer, perhaps on the broader Internet.


HTTP (Hypertext Transfer Protocol)
:   HTTP is the way computers ask one another about web stuff.

    Perhaps _the_ fundamental Web technology, HTTP directs every Web event, like a stage manager in the wings.  HTTP is our friend.  We won't look too closely at HTTP in this exercise, but you should know it exists.


IP (Internet Protocol) address
:   An IP address is the unique network ID for a computer.

    Until recently, IP addresses have looked like this: `123.234.123.234`.  Newer IP addresses are more complex; for the time being, however, most of the internet uses this older form.


Domain name
:   Domain names make IP addresses friendlier.

    Domain names are basically for humans, who have difficulty using the numerical IP addresses favored by machines, like the ones above.  They look like this:

    * `google.com`
    * `www.example.org`
    * `website.co.uk`


URL (Universal Resource Locator)
:   URLs point to stuff on computers.

    For our purposes this stuff is usually a particular webpage.  URLs can indicate any type of thing, though, like a video, an API (Application Programming Interface), a PDF document, or any other digital thing.

    Here are a couple example URLs with most of their constituent parts in place.  Note the IP addresses/domain names at their heart:

    * `http://0.0.0.0:8000/index.html`
    * `https://www.example.com/search?query=unicorn`


HTML (Hypertext Markup Language)
:   HTML structures information for consumption.

    Although ubiquitious, HTML is conceptually complex.  It is not a programming "language", like Python or JavaScript (see below), since it can't make decisions.  It's also not about presentation, or making things look any particular way; that's the job for CSS.

    Instead, in our conversation analogy, HTML might be the grammar: the defined set of nouns, verbs and adjectives allowing computers to understand what each other are talking about.


CSS (Cascading Stylesheets)
:   CSS makes HTML look cool.

    It's more than that, really; CSS also enables HTML to work on mobile phones, for example, or screen readers, or any desktop computer.  It (valiantly) encourages clients to present things as designers intend.  It doesn't always succeed.


JavaScript
:   JavaScript brings websites to life.

    JavaScript is the "programming language" of the Web, enabling websites to achieve more than mere consumption and presentation: rich experiences and useful tools.  It's basically everywhere; almost every drop-down menu, advertisement or animation on the Web comes from JavaScript.

    It's also a huge pain in the ass.  It's badly designed.  While it can be fun, with real potential for power, writing JavaScript can be frustrating and difficult.  Take your time and breathe deeply.

    Note that JavaScript is totally different from Java; the two have basically nothing in common.  JavaScript was named for stupid marketing reasons.


## First steps

So you want to make a website?  Great!  Start by opening your terminal prompt, and type:

* `mkdir ~/Desktop/myproject`

    `mkdir` literally means "make directory" (a directory is a "folder" in Mac jargon).  This creates a folder on your Desktop named `myproject`.  If you look on your Desktop (in the Macintosh Finder), you should see the `myproject` folder (directory) there somewhere.

* `cd ~/Desktop/myproject`

    `cd` literally means "change directories".  This shifts the context into the folder you just created.  Now you are "in" that folder.

* `touch index.html`

    `touch` updates a file, as to when it was last changed; if the file doesn't yet exist, `touch` just goes ahead and creates it: a quick way to make new files from scratch.

So you have just created an empty web page inside your new project.  If, in your Finder, you double click on the `myproject` folder (on your Desktop), you will now see that the file `index.html` is inside.  Lets go ahead and make one more file:

* `touch styles.css`

We'll use both of these files in a minute.

These commands use the UNIX subsystem of the Mac.  We won't get too deep into UNIX in this tutorial, but don't be frightened.  Steve Jobs had very good economic reasons for scaring everybody away from the so-called "command line" when he shipped the first Macs.  The command line is instead a lot simpler, and often easier, than the point-and-click interface we're used to.  It just takes some adjustment.

![A screen shot of the first few commands](/static/{{ page.slug }}/screenshot_1.png "A screen shot of the first few commands.")

By the way, here's a few more useful UNIX commands, which will let you move around if you want:

* `ls`
: This means "list": it tells you what's in your current directory.
* `pwd`
: Literally "print working directory": tells you what directory you're in.
* `cd ..`
: Goes back up one directory, to the parent directory.

Lots more UNIX commands exist; here's a few more [common ones](https://kb.iu.edu/d/afsk).

## Write a web page

Let's make some HTML. Fire up your text editor, and open the file `index.html`.  Put in the following code, and save the file:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>HTML test</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <p>Hello World!<p>
</body>
</html>
```

This is a fully-formed, basic web page, with all the necessary parts.


## Start the server

We're going to use Python to create a simple server on our computer, which we'll use to access the files we made above.

Python is a general programming language, in the same category as Java or JavaScript, which can be used for all sorts of things, from sophisticated statistical analysis, to sending rockets into outer space, or just running a little web server; we just need the web server here.

Let's check and make sure Python is installed OK.  In Terminal, run this command:

* `python --version`

    This command runs `python` and, using what's called a "flag", asks Python which version it is.  This both makes sure Python is installed correctly, and lets us know which command to use, since it has recently slightly changed with Python 3.

So, lets start our web server.

If the output of the above command says `Python 2.x.x`, run this command:

* `python -m SimpleHTTPServer`

Else, if the output says `Python 3.x.x`, run this command instead:

* `python -m http.server`

They both do the same thing.

This will let us access the files in the current directory from a client web browser.  Just let it run for the time being.  Note the initial output of the command:

`Serving HTTP on 0.0.0.0 port 8000 ...`

This tells us:

* HTTP is working correctly

* our server's local IP address is `0.0.0.0`.  Note this is not the computer's address on the broader internet, but only for our local network.

* our computer is using `port 8000` to provide access to content, in this case the current directory `~/Desktop/myproject`.  Ports are like digital equivalents of the analog plugs on a stereo receiver; one port for Blu-ray, one for your CD player, one for HDMI.  In this case, your computer is providing local network Web access.

If you ever want to stop the server, use the standard UNIX "stop" (interrupt) command: holding down the Control key on your keyboard, and pressing the letter "C": `ctrl-c`.


## Load a web page

Fire up your web browser, and type in this address:

* `http://0.0.0.0:8000/index.html`

You should now see your new "Hello World" webpage in all of its glory.


## Add some styles

In your `styles.css` file we created earlier, add this code:

```css
body {
    background-color: blue;
    color: white;
}
```

When you reload your browser, you should see some color changes.

For more information on CSS, check out the [CSS guides and tutorials](https://developer.mozilla.org/en-US/docs/Web/CSS) provided by Mozilla.


## Add some JavaScript

In your `index.html` file, add this code after the CSS `link` tag:

```html
...
<head>
    ...
    <link rel="stylesheet" href="styles.css">
    <script src="script.js"></script>
</head>
...
```

Create a file named `script.js` in the same directory as your other two files.  In that file, add this code:

```javascript
console.log("Hello JavaScript!")
```

When you reload your browser, you may not see anything at once; you must open the Chrome developer console, by selecting the `Chrome` menu ➙ `View` ➙ `Developer` ➙ `JavaScript Console`.  This will show the output of the `console.log()` function we called above.

![The final state of our simple webpage.](/static/{{ page.slug }}/screenshot_final.png "The final state of our simple webpage.")

Using JavaScript can quickly become an advanced lesson, and we won't discuss it more here.  With luck, this teaser has perked your interest; for more information, I recommend checking out the [JavaScript guides and tutorials](https://developer.mozilla.org/en-US/docs/Web/JavaScript) provided by Mozilla.


## Conclusion

Using the Web is complex, and takes a bit of groudwork to get going.  Once you get the basics, though, it can be really useful and fascinating.
