---
layout: post
title: Jekyll for Beginners (like me)
date: 2015-02-07 16:08:53
caegories: static blog
---

## Static webpages generators

Some static webpages generators are the following:

### Ruby

- [Jekyll](https://jekyllrb.com/)
- [Middleman](https://middlemanapp.com/)

### Node

- [Hexo](https://hexo.io/)
- [Hugo](https://gohugo.io/)

## Jekyll

> Jekyll uses the Liquid templating language to process templates. All of the standard Liquid tags and filters are supported. Jekyll even adds a few handy filters and tags of its own to make common tasks easier.

## Github pages

We can create a github pages just creating a branch **gh-pages** and commit our static files there or using jekyll.

### Using Bundle

> Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed. 

> Bundler is an exit from dependency hell, and ensures that the gems you need are present in development, staging, and production. Starting work on a project is as simple as bundle install.

#### Bundle with github pages

We must create a **Gemfile** in our **gh-pages** branch.

```
source 'https://rubygems.org'
gem 'github-pages'
```

And then just run

```bash
bundle install
```

#### Github flavored markdown (GFM)

In the file *_config.yml*

```
markdown: kramdown
kramdown:
    input: GFM
```

## Front Matter

Front matters are tags that are parsed and can be used in the *_layouts* using  *_liquid*.

```
---
layout: default
---

<p><i>{{ page.summary }}</i></p>

```

Common tags are:

- layout
- title
- featured_image
- comments
- tags
- summary
- permalink

## CNAME file

You can create a *CNAME* file and just write your domain url there.

```
www.my-awesome-blog.com
```

## Installing Jekyll without github pages

```bash
# on mac
sudo gem install jekyll

# to show help just type jekyll
jekyll

# create new site inside the <sitename> folder
jekyll new <sitename>

# run the server
jekyll serve
# or
jekyll s
```

## Creating a new post

Create a file in the folder *_posts*

```
_posts/2015-11-18-some-title.md
```


