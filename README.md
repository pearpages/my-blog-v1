# pearpages.github.io

My peronal Blog [pearpages.com](http://www.pearpages.com)

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
