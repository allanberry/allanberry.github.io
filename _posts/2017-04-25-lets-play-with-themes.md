---
layout:     post
title:      "Let's play with Jekyll themes"
date:       2017-04-25
categories: ruby jekyll github themes
---


Jekyll has a robust, well-designed theming system, on par with the likes of Ruby on Rails, Wordpress, or Django.  With some HTML skills, Jekyll themes aren't too hard to adapt from [free](http://themes.jekyllrc.org/) or even [professionally-designed](https://jekyllthemes.io/) themes, readily available on the web.  They're also simple enough to roll your own.

That's great, since Jekyll ships with a very simple theme called `minima`, which might be __too__ minimal.  In this exercise, we're going to gussy it up.

You'll want to start with a fresh Jekyll installation; perhaps get up to speed [using this Jekyll tutorial]({% post_url 2017-04-04-install-ruby-jekyll-github-pages %}).  Start by entering your Jekyll project's directory in your terminal.

    cd ~/Documents/jekyll_app

... or wherever your new project lives.

## Modifying the standard Minima theme

`minima` is a ["Gem-based theme"](https://jekyllrb.com/docs/themes/), i.e. Jekyll's new style of theme packaging.  This means it uses Ruby's native packaging system for distribution, providing (in theory) seamless installation and updating of themes.  [In practice things can get more complicated, but for simple tasks, the Gem system works well.]

You can modify the standard `minima` theme in place, without altering its code, to make small, discrete edits.  This is done by duplicating `minima` files into your own Jekyll site, to then override `minima`'s own files.

To see the `minima` files which might be overridden, consult it directly:

    bundle show minima

This shows the directory where `minima`'s files are kept.  Let's take a peek in there; you can either locate the folder in the Mac Finder/Windows Explorer, or just open it directly in your text editor.   Here's how I do it with [Sublime Text](https://www.sublimetext.com/)):

    subl $(bundle show minima)

Inside are several files which might be useful to override:

    _includes   # includes are "partials": little snippets of code, small components, meant for reuse
    _layouts    # layouts are full page structures, which you can nest within other layouts
    _sass       # Sass is like super CSS

In this case, we'll just alter a few Sass variables to see how it works.  In practice, however, you can overload any of these files to your heart's content, safe in the knowledge that you're not actually changing the Gem files, so your changes can't hurt anything.  This really provides a lot of creative freedom.

To start, duplicate the primary `minima` Sass file into your project.

    mkdir _sass
    cp $(bundle show minima)/_sass/minima.scss _sass/

A file named `minima.scss` should now be in the new `_sass` directory you just created.  This file is `minima`'s primary set of base default styles, stuffed with variables which we can alter however we like.  It is consulted whenever your Jekyll site is rebuilt, and is compiled automatically into browser-safe CSS.

Sass is like super CSS: it provides a lot of fancy features to CSS, like variables and module imports, which CSS doesn't support.  It is a strict superset of CSS, however, so all CSS is valid Sass.  Note the file extension: Sass uses the `scss` extension these days, mostly for [historical reasons](http://thesassway.com/editorial/sass-vs-scss-which-syntax-is-better).

To demonstrate possible changes you can perform, near the top of this file, change this line...

    $base-font-family: "Helvetica Neue", Helvetica, Arial, sans-serif !default;

...to the more prosaic...

    $base-font-family: "Times New Roman", Times, serif !default;

...which, when you reload your site with `jekyll serve` should change how your base font gets rendered.  Then, so our headings aren't all in Serif fonts, lets change them back to Helvetica, by placing this CSS code at the bottom of this file, below the `@import` directives:

    h1, h2, h3, h4, h5, h6 {
        font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
    }

So, really you can change any CSS for your entire site from this file, or import other Sass files to do more drastic changes.


## Installing a Rubygems-based theme

As of version 3.2, themes can be installed via "Rubygems": Ruby's package manager system.  This is the newest, cleanest method, minimizing the need to write or maintain code in the future.  Gem-installed themes can be modified in the same way as we modified `minima` in the preceding section.

That's all true "in theory".  In practice, the Gem-based theme system is quite new, and has a few teething problems.  There also just aren't many Gem themes available, at least in comparison to the number of older, so-called "classic" themes.

Installation of a Gem-based theme is straightforward.  In the interest of simplicity, we'll install a theme largely compatible with the standard Jekyll setup, using `post`s and `page`s like `minima` does, called [__Jekyll Swiss__](https://rubygems.org/gems/jekyll-swiss).

1. Update your `Gemfile` to include `jekyll-swiss`, by adding `jekyll-swiss`...

    ```ruby
    gem "minima", "~> 2.0"
    gem "jekyll-swiss"  # <-- new
    ```

    (For now, we're going to keep `minima` in there, because of a silly bug.)

2. Update your `_config.yml` by changing this line...

        theme: "minima", "~> 2.0"

    ...to this:

        theme: "jekyll-swiss"

3. Then we need Bundler to take note of these changes:

        bundle install
        bundle update

    ...which will install Jekyll Swiss for us.

4. At this point, we __should__ be able to simply run...

        jekyll serve

    ...but on my machine, however, Jekyll complains that it can't find some Github Pages-related files.  Let's copy them from the Minima gem (first creating the necessary container directories):

    ```bash
    mkdir _includes
    cp $(bundle show minima)/_includes/icon-github.html _includes/
    cp $(bundle show minima)/_includes/icon-github.svg _includes/
    jekyll serve
    ```

    Now we can remove `gem "minima", "~> 2.0"` from our Gemfile, and boot up our site, with its snazzy new theme.

        open http://localost:4000/

Whew; a little bit of ugliness there.  While this particular bug is related to GitHub pages in particular, it underlines how Gem themes are still crusty around the edges.  When they finally get mature, they'll be great.
