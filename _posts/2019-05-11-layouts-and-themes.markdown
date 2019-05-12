---
author: smi
title: "Layouts and Themes"
date: 2019-05-11 12:01:39 +0200
categories: jekyll
img: jekyll01.png
---

Jekyll themes specify plugins and package up assets, layouts, includes and stylesheets in a way that can easily be overridden by the site's content. 

Community developed gem-based themes store some site's directories (e.g assets, _layouts, _includes) inside a gem, hidden from the user. All of these directories can be read, processed and their content can be extended or overridden as needed. 

The default Jekyll theme is called `minima`. Layouts are templates that wrap around content and allow for an easy definition of a site-wide navigation, footer, page style... Minima theme has two layouts - the `page` and the `post` layout (and the `home` and `default` layouts).



## Community Developed Themes

It is possible to find existing themes on following links:

- https://jekyllthemes.io/free
- http://jekyllthemes.org/
- https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme

As an example we can use the [Cayman theme](https://github.com/pages-themes/cayman). by opening the *Gemfile* file and adding the following line:

```ruby
gem 'jekyll-theme-cayman', '~> 0.1.1'
```

After that we run `bundle install` in order to install the new theme. In order to use this theme, we need to open the *_config.yml* file and change the line `theme: minima` to `theme: jekyll-theme-cayman`. The cayman theme does not provide `post` , `page` and `home` layouts so it is important to define them. 

Instead of using existing jekyll themes, we will modify the (Retrospect)[<https://templated.co/>] HTML/CSS theme and edit it for use with jekyll.

## Layouts

It is possible to redefine existing layouts or define new layouts. To do this we make a new folder **_layouts** and inside make new files that will represent our layouts. A usual approach is to define a default layout ( **default.html**) with site-wide menu and footer and have other layouts inherit from it. It is also possible to define multiple page elements and use them as needed. Inside the **_layouts** folder we will define files *post.html*, *page.html* and *home.html*. We will use <u>**Liquid**</u> templating language to process templates and display content on the page. **<u>Liquid</u>** language can access variables using the `{{ variable }}` syntax and can perform logic statements using the `{% if statement %} {% endif %}`  syntax.  

A simple layout for *post.html*:

```yaml
---
layout: default
---

// content
```

It is common to break complex pages into smaller elements that can be reused in different pages. All this elements are placed in the **_include** folder. 

Existing **assets** and **images** template folder are copied into the Jekyll project folder. Because of this, we will have to adjust all *.html* files and replace `assets` and `images` with the new paths `{{site.url}}/assets/` and `{{site.url}}/assets/`, respectively. This also needs to be done in all *.markdown* files. 

All posts need to include the `author`, `title` and  `date` in the front matter, because this information will be used for listing the post on the home page. The short post description also includes the first paragraph in the post as well as an image. Image name (which is located in the **images** folder) and category can be changed using the `img` and `categories` tags in the front matter. If the image values is not set, it will default to the Pharo lighthouse image. 

All posts are listed using the paginate plugin for jekyll. 



## References

1. Jekyll docs - themes: https://jekyllrb.com/docs/themes/
2. Jekyll docs - layouts: https://jekyllrb.com/docs/layouts/
3. Jekyll docs - Liquid: https://jekyllrb.com/docs/liquid/
4. Jekyll docs - Paginate: https://jekyllrb.com/docs/pagination/
