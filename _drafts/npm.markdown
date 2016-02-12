 ---
layout: post
title: "NPM Playbook"
categories: Javascript NPM
date:  2016-02-10 19:44:10
---

#### Contents

{:.no_toc}
* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Intro

- Track your dependencies
- Write simple scripts
- Publish your own module

## NPM Basics

### Typical Usage

```bash
npm install # install all the dependencies
npm start
npm test
```

package.json

```json
"dependencies": {
},
"devDependencies": {
},
"scripts": {
    "start": "node server.js",
    "test": "node test.js"
}
```

### help

```bash
npm -h
npm --help
npm help <command> # This opens a web page with the info of the command
npm help-search <what-to-search>
```

### Package.json

Type of projects:

- for users
- 3rd party package

Reasons for package.json

- track dependencies
- create scripts

```bash
npm init
npm init -y # with all the default values
```

#### Setting default values

These are kept in the **.npmrc** of the user directory.

```bash
npm set init-author-name 'Pere Pages'
npm set init-license 'MIT'
npm get init-author-name
npm config delete init-author-name
```

### npm install

```bash
npm install <package>
npm install --global <package>
npm list --depth 0 --global true
npm install lodash --save
npm install lodash -S  # is the same as --save
npm i lodash -S # it is also the same

npm install karma --save-dev
```

#### Installing a specific version

0.0.x are usually just patches and fixes that don't change any functionality.

##### Minor Release

0.x.0 are new functionalities added.

##### Major Release

```
1.9.0 would mean new functionality, nothing broken yet.
```

x.0.0 are major changes that break the distribution, something that is not backwards compatible.

##### General cases

- Installing last version
- Instaling a specific version

##### Examples

```bash
npm install underscore@1.8.2
npm install underscore@1.8.x
npm install underscore@1.x
npm install underscore@">1.1.0"
npm install underscore@">=1.1.0"
npm install underscore@">=1.1.0 < 1.4.0"
npm install underscore@1.8.2 --save --save-exact
```

The first means that the version is 1.8.3 but can be updated with the most recent (major release).

The second that we want only the latest version of the minor release.

```json
"dependencies": {
    "underscore": "^1.8.3",
    "karma": "~1.5.2"
}
```

### Listing installed packages

```bash
npm list
npm ls # the same than above
npm list --depth 1
npm list --depth 0 --long true # long shows lots of information
npm list --global true
npm list --global true --depth 1
npm list --depth 0 --json true
npm list --depth 0 --parseable true
npm list --depth 0 --dev true
npm list --depth 0 --prod true
```

### Removing a Package

```bash
npm uninstall <package> # but it will still be in the dependencies
npm uninstall <package> --save
npm uninstall -g # if it's been previously installed globally
```

### Updating packages

```bash
npm update
npm update --dev
npm update --prod
```

## Publishing a Package

Registiring to [npm](https://www.npmjs.com)

Setting up your npm user in the system

```bash
npm adduser
```

