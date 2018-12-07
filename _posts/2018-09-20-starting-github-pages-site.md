---
layout: post
title: "Starting my GitHub Pages site"
categories: misc
---

Over the last few days, I have learned how to set up a website using GitHub
Pages using the Jekyll static site generator.  This allows you to set up and
maintain your own website for free.  You really want to use Jekyll for your
website because it allows you to create and edit simple
[Markdown](https://guides.github.com/features/mastering-markdown/) `*.md`
files for your web content.  Also, it automatically provides a nice
representation on mobile browsers (which is very hard to do with static HTML).

Setting up to create a GitHub Pages site using Jekyll was not as easy to do as
I would have hoped.  First, you have to install a newer version of Ruby on
your local machine and then use that to install something call "bundler" and
then use that to install Jekyll.  This is really important because to test the
building of your website and view what it looks like locally, you have to be
able to run an updated Jekyll server locally over and over again on your local
machine.  To install Ruby and Jekyll, I followed the instructions on various
GitHub and other sites
(e.g. [here](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)). I
was able to install these on a Windows 7 Laptop using Cygwin (and therefore
followed the Linux instructions).  I was able to build Ruby 2.5.1 from source
with GCC 5.4.0 from within the Cygwin environment.  From there, I was off to
the races.  (One little hitch was that the `gem` command that gets run in the
`bundler install` command would not work to download files off the remote
server until I got off of my company's VPN.)

Once I had Ruby and Jekyll installed locally, the fastest path that I found to
get a GitHub Pages website working with Jekyll was to just copy one of the
[officially supported GitHub Pages Jekyll
Themes](https://pages.github.com/themes/).  I went with the [Minima
theme](https://github.com/jekyll/minima) since it is very simple looking, has
a nice set of menu links at the top.  And in mobile mode, those menu items
show up as the three-bar icon at the top right.  This makes the site very nice
to view in mobile mode.  (The other themes did not do that and I thought were
not as elegant in mobile mode as the Minima theme.)  To use this theme to
create my own site, I just forked the [Minima github
repo](https://github.com/jekyll/minima) into my personal GitHub account and
then renamed it to make it clear what it was and then cloned the repo locally
on my Windows 7 Cygwin laptop.  I then created a `gh-pages` branch from the
existing `master` branch.  From there I was able to install the needed
dependencies with the command:

```
$ bundler install
```

and then build and view the site locally by running the blocking command:

```
$ bundle exec jekyll serve
```

in a Cygwin terminal and then going to `localhost:4000` in my Chrome browser
on my Windows 7 machine.  (While that command runs in blocking mode, you can
edit your files locally and by default Jekyll will automatically rebuilt your
site and you can just refresh your browser to see the updated pages.  Very
nice!).  By forking this Minima Theme GitHub repo, it is my hope that it
should be easy to update my template and files by merging in updated versions
from the main GitHub repo (of course carefully resolving merge conflicts).

After I verified that I could generate and view the existing Minima page
locally and after pushing to github, I then set out to customize it for
myself.  You can look at the git commit history for how I did that and what
files I changed.  (The first commit just creates a skeleton to make this my
site and should be a good place to start.)  Once I am finished making the site
looking the way that I want, I will use it to replace my current (antiquated)
static HTML site currently at `https://bartlettroscoe.github.io`.  (To do
this, I will just hard reset the `master` branch in my
[bartlettroscoe.github.io
repo](https://github.com/bartlettroscoe/bartlettroscoe.github.io) and force
push and that should be it.  And if you are reading this, then that is what I
did!)

I am very happy with how this site looks so far.  This is really something
special when you think about it.  With GitHub Pages and Jekyll, you get a free
semi-professional looking website that you can edit simple Markdown `*.md`
files with full git version-control history and it gets served on the web for
free!  That is pretty slick!

Hopefully this short blog will help other people who might be interested in
setting up their own website using GitHub Pages with minimal effort.
