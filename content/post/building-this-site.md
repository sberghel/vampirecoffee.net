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

### Yet Another Markdown Syntax Flavor

The syntax for tables is _almost_, but not quite, the same as the syntax that
GitHub uses for Markdown tables. It looks like this:

```
headers | headers | headers
--------|---------|--------
cell    | cell | cell
cell    | cell | cell
```

And if the dashes are too short, then the table won't render at all. So you
can't just do this:

```
header | header | header
---|---|---
cell | cell | cell
cell | cell | cell
```

I wish there was only one flavor of Markdown, instead of every single implementation
having slightly different flavors of Markdown. Oh well.

## Still Pretty Awesome, Though

What I spent most of my time doing wasn't writing Markdown, or changing configuration
variables, or changing the front page. I spent most of my time _actually writing
my Hugo post_. It was _really_ useful for me to be able to write the post in
a pretty simple markup language and then convert it to HTML through software.

### The Deployment Process Is Ridiculously Simple

I was able to deploy my site to my webhost by generating all the HTML files and
copying them over to my webhost. That's it. That was the entire process.

## Should You Use Hugo?

If you want to put up slideshows of your photos, probably not.
If you want to make a bunch of AJAX calls to a database to dynamically
display data, _definitely not_.

But if you're hosting your own site,
your content is mostly written[^1],
and you're ok having almost no dynamic content[^2],
Hugo is probably a good choice.


[^1]: Not multimedia, not full of Javascript animations, etc.

[^2]: Hugo supports Disqus comments. This is the extent of its dynamic content support.
