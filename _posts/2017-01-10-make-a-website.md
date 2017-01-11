---
layout: post
title:  "Make a Website with Jekyll, Github, and Cloudflare"
date:   2017-01-10 20:02.01
categories: blog
image: /assets/article_images/2017-01-10-make-a-website/website.jpg
---

After launching this site, I had a lot of friends, with varying levels
of technical ability, ask me how I set it up and where it was
hosted. Yesterday, I launched another site,
[graybox-testing.org](https://graybox-testing.org) using the same
software and services, and I wrote down the steps I used to make
it. Hopefully this will be helpful to others who want a freely hosted,
easy to manage site.

I should mention that I did not come up with this myself. My coworker,
[Scott Doxey](https://neo-geek.net) showed me how he hosted his site
and helped me get set up. So all credit goes to him.

I'll try and be as clear as I can for those non-developers out
there. If you're technically inclined you should be able to figure
most of this stuff out. If you want a simpler solution, I'd suggest
Wordpress or Squarespace or some other easy to use service.

## Software and Services

First we'll cover the software and services I used, so you can get
familar with them.

### Jekyll

[Jekyll](http://jekyllrb.com) is a static site generator. It takes
content you write in
[Markdown](http://daringfireball.net/projects/markdown/) and generates
a complete website from it. Unlike content management systems like
[Wordpress](https://wordpress.com) or
[Drupal](https://www.drupal.org), it doesn't generate web pages on the
fly from a database. Instead, it just converts the Markdown documents
into static HTML files, which you can serve from any basic web
server. With plugins, themes, and other features, it gives you the
same functionality as a CMS, but without needing all the
infrastructure. Most importantly, Jekyll is the technology behind
[Github Pages](https://pages.github.com), which is how this site is
served.

### Git

[Git](https://git-scm.com) is
[version control](https://en.wikipedia.org/wiki/Version_control)
software. It saves every change you make to a set of files over
time. Software developers use it to manage source code, but it can
really manage any kind of file. It will manage the content of the
website and make it easy to publish new updates. Because it stores
every change to the site, it can be used to undo any change all the
way back to the beginning of your site.

### Github

[Github](https://github.com) is a source code management platform
built on [Git](https://git-scm.com). It will store a copy of your site
content and uses Jekyll to generate the site from them.

### Cloudflare

[Cloudflare](https://www.cloudflare.com) is a
[content delivery network](https://en.wikipedia.org/wiki/Content_delivery_network)
with security features like
[DDOS](https://en.wikipedia.org/wiki/Denial-of-service_attack)
protection,
[SSL](https://en.wikipedia.org/wiki/Transport_Layer_Security) and
more. For large sites, these features are a nessesity on today's
internet, but the company also provides them free of charge for sites
with minimal traffic.

### Domain Registrar

If you want a custom domain, you'll need to register it
somewhere. There are a ton of services available, just
[google it](http://lmgtfy.com/?q=domain+registration). I used
[name.com](https://www.name.com).

## Steps

Follow these steps and you'll have a website up in less than 1/2 hour.

### 1) Create an account on Github

Go to the [Github signup page](https://github.com/join) and create an
account. 

### 2) Make a new repository

After you create your account, add a new repository. This is on the
bottom right of your home page on github:

![Adding a new repository](/assets/article_images/2017-01-10-make-a-website/new-repository.png)

Call the new repository username.github.io, where "username" is
replaced with the username you used to sign up for Github. If you don't
have your own domain name, it will be served from this
[subdomain](https://en.wikipedia.org/wiki/Subdomain) of the the
github.io domain. For example, I called my repository
[dfox.github.io](https://github.com/dfox/dfox.github.io) because my username is dfox.

![Creating the repository](/assets/article_images/2017-01-10-make-a-website/creating-the-repository.png)

### 3) Set source branch

Now, from your repository page, go to "Settings". Scroll down to the
GitHub Pages section and select "master branch" as the source
branch. This will make it easier to publish. 

![Setting the source branch](/assets/article_images/2017-01-10-make-a-website/set-branch.png)

### 4) Download Homebrew

If you're on OSX, you can just install [Homebrew](http://brew.sh). It
will make it really easy to install the rest of the things you'll need
and give you easy access to a ton of other software. If you are on
Windows, you'll most likely need to install these things separately. I
haven't used Windows in many years so I don't know the steps for that
platform.

### 5) Install Git

If you are a developer, you most likely already have
[Git](https://git-scm.com). If not, you'll need to install it. With
homebrew it's just `$ brew install git`. How to use Git is a huge topic
and I'm not going to cover it. There are
[lots of resources](https://git-scm.com/doc) available to help you
there. If you are not comfortable on the command line, there are
[lots of GUI clients](https://git-scm.com/downloads/guis) available.

### 6) Install Jekyll

Again with homebrew, you can just run `$ brew install
jekyll`. Otherwise you'll need to follow the instructions on
[the Jekyll site](http://jekyllrb.com)

### 7) Clone your repo

Now you will clone your repo so you can work on it locally. What this
does is make a copy of the repository on your computer. You will make
changes to the site and save them locally, then you can push your
change up to Github to publish the site.

![Cloning the repo](/assets/article_images/2017-01-10-make-a-website/cloning.png)

### 8) Initialize the Jekyll site

In the command line, cd into the parent directory of the repository
you just cloned and run:

`jekyll new username.github.io --force`

Note you want to replace "*username.github.io*" with the name of the
repository directory.

### 9) Push your new website

Now you can add the files Jekyll created to your repository and push
the changes to Github:

```cd username.github.io
git add .
git commit -a -m 'Initial site'
git push origin master
```

## Your Site is Live

Now your site is live!

You should be able to go to the URL http://username.github.io and see
the default Jekyll site now (again, replace "username" with your
github username).

## Setting Up Your Custom Domain

This next part will make it so your custom domain name points to your
site. We're going to use Cloudflare to handle the DNS and cache your
site so it's really fast. 

### 1) Make a Cloudflare account

Go to [Cloudflare](https://www.cloudflare.com/a/sign-up) and make an
account.

### 2) Set up DNS

Go to your account on Cloudflare and click on "+ Add Site" at the
top. Enter your domain into the box and click "Begin Scan".

![Adding your site](/assets/article_images/2017-01-10-make-a-website/add-site.png)

### 3) Add DNS Records

Now, you'll need to set up CNAME records for the site. You need to add
at least a CNAME record with the name of your domain and a value of
"username.github.io" where "username" is the username you used for
Github. You can see how I configured my settings here:

![Adding your site](/assets/article_images/2017-01-10-make-a-website/dns-records.png)

### 4) Set up nameservers

At the bottom of the page you set up the DNS records on, it will list
2 nameservers. You will need to log into your domain registrar's
website and put the names of those servers into the area they specify
so that traffic will be routed to Cloudflare. How this is done is
different for every registrar, so you'll need to look up the
information on their site or ask a support person how to do it.

### 5) Add a CNAME File to Github

Now, in the repository directory for your website, create a file
called "CNAME" and in it, just put your domain name. I put
"dfox.io". Then just push it up to Github with `git push origin master`.

## Conclusion

That's it! In a few minutes you should now be able to type your domain
and see the default Jekyll site you set up.

Next, you'll want to start editing your site and adding content. See
the [Jekyll site](http://jekyllrb.com) for how to do that. There is
also a pretty good site with templates, plugins, themes and more at
[Jekyll Tips](http://jekyll.tips).


