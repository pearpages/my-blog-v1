# pearpages.github.io

My peronal Blog [pearpages.com](http://www.pearpages.com)

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

## Considerations

Right now is using a CSS folder, create a **_sass** folder to start using *sass* again.

## Old folder (_old)

Old layouts and includes to use as inspiration and migration.

---

## Warnings

**jekyll-toc** is installed [jekyll-toc](https://github.com/toshimaru/jekyll-toc) but not working.

Right now the *post.html* template is using *jQuery* to move the TOC (table of contents).

---

## Pending Tasks

+ 