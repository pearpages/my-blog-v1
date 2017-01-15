# pearpages.github.io

My personal Blog [pearpages.com](http://www.pearpages.com)

```shell
bundle exec jekyll serve
# or
./run.sh
```

[Markdown Cheat Sheet](Markdown.pdf)

---

## Installation

### Gemfile

```
source 'https://rubygems.org'

require 'json'
require 'open-uri'
versions = JSON.parse(open('https://pages.github.com/versions.json').read)

gem 'github-pages', versions['github-pages']
````

```bash
bundle install
```

```bash
bundle update
```

```bash
bundle exec jekyll serve
```

---

## Pending

+ Check highlighting
+ Defining all posts summary page
+ Definining bio page
+ Defining home page

---

## Tips

### Configuring Permalink

```
# _config.yml
permalink: /posts/:categories/:year/:month/:day/:title.html
```

--- 

## Post Attributes

```
layout: post
title:  "Welcome to Jekyll!"
date:   2016-10-03 19:41:07 -0600
categories: jekyll update
image: /images/pic09.jpg
```

---

## Considerations

Right now is using a CSS folder, create a **_sass** folder to start using *sass* again.

## Columns

*6u* would be the equivalent to 6 columns in bootstrap. 

12u$(medium) meaning 12 columns for medium size.

```html
<div class="6u 12u$(medium)" >
</div>
```

## Old folder (_old)

Old layouts and includes to use as inspiration and migration.

## TOC (Table of Contents)

Add this in the *markdown* file.

```
* TOC
{:toc}
```

## elements.html

In the *elements.html* there are all the examples predefined by the style.

---

## Warnings

**jekyll-toc** is installed [jekyll-toc](https://github.com/toshimaru/jekyll-toc) but not working.

Right now the *post.html* template is using *jQuery* to move the TOC (table of contents).

---
## Static Pages

+ about / pere-pages-soms
+ 404
+ fun