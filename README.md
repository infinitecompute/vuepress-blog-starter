# VuePress blog

## Installation

### Create a new project 

Create a new project following first time [setup instructions](https://vuepress.vuejs.org/guide/getting-started.html#global-installation).  

```sh
# create a top website directory
mkdir website && cd website

# install as a local dependency
# deprecated: npm install -D vuepress
yarn add --dev vuepress

# create a directory for your content
mkdir blog
```

After installation you will see `node_modules` with VuePress dependencies within your directory and a `yarn.lock` and `package.json` files have been created.

You may call your content directory anything you wish.  Since I may end up with a separate docs directory in the future, I have chosen to put content in a `blog` directory.

```
.
├─ blog
├─ node_modules/ ...
├─ package.json
└─ yarn.lock
```

### Install the Casper theme 

This setup uses a [Casper theme](https://github.com/alexander-heimbuch/vuepress-theme-casper) by Alexander Heimbuch (see [live example](http://alexander.heimbu.ch/vuepress-theme-casper/)). If you've used [Ghost blog](https://github.com/TryGhost/Casper) you'll recognize this as the default theme. I like it because the default layout is based on the post's picture size.  

If building the site content from the ground up just add the dependency:

```sh
# install theme package
# deprecated: npm i vuepress-theme-casper --save
yarn add --dev vuepress-theme-casper
```

### Theme starter content

If you would rather start with content then grab a copy of the theme project locally. It's a little confusing here, because the sample content is mixed in with the theme package files you installed above. We'll just grab the content out of a copy of the project to bootstrap our blog.

```sh
# Pop out of our website directory
cd ..

# get a copy of the them locally
git clone https://github.com/alexander-heimbuch/vuepress-theme-casper.git 

# copy the interesting bits
cp -R vuepress-theme-casper/blog website
```

This adds the following stock content files:

```
.
└─ blog
   ├─ index.md
   ├─ about.md
   ├─ media.md
   ├─ posts/ ...
   └─ .vuepress
      └─ config.js
```

Note it has a skeleton config.js that we will add to later.

## Take it for a test run

Add a scripts section to your `package.json`

```json
{
  "scripts": {
    "blog:dev": "vuepress dev ./blog",
    "blog:build": "vuepress build blog"
  }
  "devDependencies": {
    "vuepress": "^1.5.0",
    "vuepress-theme-casper": "^3.0.1"
  }
}
```

Build and run locally with:

```sh
yarn blog:dev
```

You should see the brand new site if you open http://localhost:8080 in a browser.

Alternatively, to generate the static assets:

```sh
yarn blog:build
```
After running build, you will see the `dist` directory was added with the static output:
```
.
└─ blog
   └─ .vuepress
      └─ dist/ ...
```

## Configuration

Adapt your vuepress config `config.js`:

```js
module.exports = {
  title: 'Theme Title',
  description: 'Theme description',
  base: '/',
  theme: 'casper',
  head: [
    ['link', { rel: 'icon', href: '/favicon.png' }]
  ],
  markdown: {
    anchor: {
      permalink: false,
      permalinkBefore: false
    }
  },
  themeConfig: {
    cover: '/images/cover.jpg',
    logo: '/images/logo.png',
    nav: [{
      text: 'Home',
      link: '/'
    }, {
      text: 'Posts',
      link: '/posts'
    }, {
      text: 'Category',
      link: '/category/some-category'
    }, {
      text: 'Page',
      link: '/a-page.html'
    }],

    footer: [{
      text: 'Latest Posts',
      link: '/posts'
    }, {
      text: 'Facebook',
      link: 'https://facebook.com/'
    }, {
      text: 'Twitter',
      link: 'https://twitter.com'
    }, {
      text: 'Github',
      link: 'https://github.com/'
    }],
    social: {
      github: 'https://github.com',
      twitter: 'https://twitter.com',
      facebook: 'https://facebook.com',
      xing: 'https://xing.de',
      instagram: 'https://instagram.com',
      linkedin: 'https://linkedin.com'
    }
  }
}
```

## Blog Posts

When creating a post, a front matter block is defined to specify attributes of the post use for organizing site content.  The front matter starts and ends with three dashes `---`. The blog synopsis will include all text prior to the `<!-- more -->` tag.  

```markdown
---
title: title here
image: https://picsum.photos/1920/1080/?random&date=2018-06-06
publish: 2020-05-06
type: post
tags:
  - tag one
  - tage two
categories:
  - category one
readingTime: 10 Minutes
---

Beginning of article to include in abstract.

<!-- more -->

The rest of the article.
```