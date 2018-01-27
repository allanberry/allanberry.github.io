---
layout:     post
title:      "Install Ruby and Jekyll for Github Pages"
date:       2017-04-04
categories: ruby jekyll github
---

So, Jekyll is great.

Readme: `https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/`

Win instructions
    https://labs.sverrirs.com/jekyll/


Getting Started
---

Following is some "[command-line BS](http://www.pgbovine.net/command-line-bullshittery.htm)" to get started with the latest [Ruby](https://www.ruby-lang.org/en/) and [Jekyll](https://jekyllrb.com/), and deploy to GitHub Pages.

If you want, you can just use the [official Jekyll install docs](https://jekyllrb.com/docs/installation/) for the first part of this guide; this provides a way to separate your Jekyll project from any already installed Ruby environment, or any other Ruby projects.  I've had trouble in the past with managing Ruby; this should provide a good basis for development going forward.  If you're all set, skip past the installation parts.

These instructions are for Mac.  Linux should be similar, except for the Homebrew (`brew`) parts; instructions for compiling are on the respective project homepages.  I don't know how to do this on Windows; it might be totally different.  I think you need something like [RubyInstaller](http://rubyinstaller.org/), and then you can move on to the "install Jekyll" part later on.

So, without further ado, let's get started.  We're going to use the latest hipster stuff; things have actually progressed nicely since a few years ago.

* [ruby-install](https://github.com/postmodern/ruby-install): to install Rubies
* [chruby](https://github.com/postmodern/chruby): to switch between Rubies

Chruby is also great.

    https://pbrisbin.com/posts/chruby/

Install Homebrew on your Mac, if you don't already have it.

    $ ruby -e "$(curl -fsSL https://raw.github.com/Homebrew/homebrew/go/install)"

Later on, we'll need Git, so [install that too](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don't already have it.  Unfortunately, the Homebrew version is quite old, so it's better todo this by the book.  If you're on a Mac, [this looks nice](https://desktop.github.com/).

You should also setup a [GitHub account](https://help.github.com/articles/signing-up-for-a-new-github-account/) if you don't have one already.

Note that last command used Ruby to install Homebrew; it's a Ruby app, and uses the OSX standard system Ruby.  That's the last time we need to use the System Ruby; OSX currently is only v2.0, and Jekyll requires v2.1.


Building a Ruby environment
---

Let's install the basics using Homebrew.

    $ brew install ruby-install
    $ brew install chruby
    $ brew install --HEAD https://raw.github.com/postmodern/gem_home/master/homebrew/gem_home.rb

We are supposed to put some stuff in `~/.bashrc` or `/etc/profile`; I tend to put my config details in `~/.profile`, because it's kinda the Mac way, I always have in the past, and I get confused easily.  YMMV.  Seems to work.

    $ source /usr/local/share/gem_home/gem_home.sh
    $ source /usr/local/share/chruby/chruby.sh
    $ source /usr/local/share/chruby/auto.sh

After that, reload the config file.

    $ source ~/.profile

We need a place to put our Rubies.

    $ mkdir ~/.rubies

Install the current stable Ruby version, currently `2.4.1`.  Ruby-Install is relatively quick, but it may still take a bit; 5-10 mins or so on my iMac.  Get a coffee.

    $ ruby-install ruby 2.4.1

You can now find the Ruby you just installed by looking in your `rubies` directory:

    $ ls -lap ~/.rubies

lets make a folder for our Jekyll project.

    $ mkdir ~/Documents/jekyll_app
    $ cd ~/Documents/jekyll_app

If we examine our current Ruby version, we should still be using the OSX system Ruby.

    $ ruby --version
    ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]

Let's put in a simple config file, which Chruby uses to switch versions automatically, depending on which directory we're in.

    echo '2.4.1' > .ruby-version
    cat .ruby-version

That was enough for Chruby to switch to a different version of Ruby. If we switch temporarily to the parent directory and back, we'll see the Ruby gets changed back to the system Ruby, and then back again to our current Ruby, without any fuss.  Slick.

    $ ruby --version
    ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-darwin16]
    cd ..
    $ ruby --version
    ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin16]
    $ cd jekyll_app
    $ ruby --version
    ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-darwin16]

Extra credit: if you want to keep your Gems (i.e. libraries/modules) discrete and tidy as well, you might want to check out [Gem Home](https://github.com/postmodern/gem_home), which keeps Ruby Gems in a local directory, instead of installing them globally.  This is useful if you're doing a lot of Ruby work, but it's overkill for our purposes.

Installing Jekyll
---

Now that we have a discreet Ruby, we can install Jekyll.  At this point, I'm leaning on the [official install docs](https://jekyllrb.com/docs/installation/).  This uses the Ruby package manager, RubyGems, to install Jekyll.
    gem install jekyll
    $ jekyll --version
    jekyll 3.4.3

At this point, we can move on to the [standard Jekyll docs](https://jekyllrb.com/docs/usage/).  Woohoo!  But let's keep going.

Let's initialize our project with a Git repository, and do a first commit, just to make sure everything is wired up correctly.

    $ git init .
    $ git add -A
    $ git commit -m "First commit."

We'll need Bundler, which Jekyll uses to install stuff.

    $ gem install bundler

Create a new Jekyll project in our current directory, and serve it via HTTP.

    $ jekyll new .
    $ jekyll serve

Now, if you visit `http://127.0.0.1:4000/` in a web browser, you can see a "Hello World" kind of site.  Lets keep this running for a while; you could press `Ctrl-C` to kill the process, but instead just open a new terminal tab/window.  This will let you work on your site while Jekyll continues to serve it in the background.

You can find a file called "welcome-to-jekyll" (or something) in the `_posts` directory.  Open it up in your text editor, and change some text.  When you reload your browser, you'll find that Jekyll has updated the page for you, without having to restart the server.  You'll also find a `_config.yml` file; take a moment to edit the Title, Description, Email fields; changing the site configuration will require you to restart the server, however.


Putting our Jekyll site on GitHub Pages
---

Next, we'll get our Jekyll site up on GitHub.  We'll rely heavily on [GitHub's own documentation](https://help.github.com/articles/about-github-pages-and-jekyll/) on the subject: worthwhile to peruse.

Follow these instructions.

    `https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/`

Getting tired.  Now follow these instructions.

    `https://www.smashingmagazine.com/2014/08/build-blog-jekyll-github-pages/#2-host-on-your-github-account`

I'll fill this out in the coming weeks.
