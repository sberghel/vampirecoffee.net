+++
date = "2015-09-10T18:18:36-07:00"
draft = true
title = "Building This Site"
tags = ["computers","web","meta","gohugo.io"]
+++

I've had a couple people ask me how I built this site. This is the short version.

## Hugo

I used [Hugo](http://gohugo.io) to build my website.
This means that my first two posts are both "about Hugo", which is confusing.
Oh well.

## The Cool Thing

Here's the initial setup that I did:

```
mkdir vampirecoffee.net
cd vampirecoffee.net
hugo new site
hugo new post/hugo-2015.md
```

After that, I [tooled around with some themes](http://gohugo.io/overview/quickstart/)
to find one I liked, and then I could got straight to editing the Markdown for
my post on the Hugo Awards. 

This has a couple of advantages:

* It's less effort than trying to build any website more advanced than 
    [this](http://motherfuckingwebsite.com/) in plain HTML+CSS
* I still get the shinyness of "responsive web design".
* I can use someone else's code to put my posts on both the front page of my 
    site *and* their own pages, instead of hacking together my own code to do so.
* I can write my posts in plain Markdown, instead of wearing out the shift 
    keys on my keyboard typing HTML

## The Annoying Parts

### Having Only Posts Show Up On The Main Page

When I first set up the site, the [about page]({{< relref "about.md" >}}) was
showing up on the front page, right under my first post. This was annoying, and
I wanted to show only content from `/post/` on the front page.  
The syntax for this wasn't at all clear to me. I wound up changing
`layouts/index.html` so that instead of

```
{{ range .Data.Pages }}
```

I had

```
{{ range where .Data.Pages.ByDate "Section" "post" }}
```

I'm _reasonably_ certain that only shows pages from the `/post` directory on the
main page - as per the [Hugo documentation about sections](http://gohugo.io/content/sections/) - but I'm not entirely sure.

### What Are Configuration Variables? We Just Don't Know.

The documentation on how to _set_ your own configuration variables isn't in
a place I would have thought to look for it. It's
[under "Getting Started", on a link labeled "Configuration"](http://gohugo.io/overview/configuration/). 
Doing a Google search for "hugo variables" shows the page on _template_ use of variables.
I initally wound up setting up a `config.toml` file based on the
[documentation about how _templates_ should use variables](http://gohugo.io/templates/variables/#site-variables:2b8b8ac4006be88c769f5e3fd99b009a),
instead of the documentation on how _sites themselves_ should set the variables.

### Weird Markdown Syntax Is Weird
