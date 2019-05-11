---
author: smi
title: "Layouts and Themes"
date: 2019-04-21 21:01:59 +0200
categories: jekyll update
img: jekyll01.png
---

Jekyll themes specify plugins and package up assets, layouts, includes and stylesheets in a way that can easily be overridden by the site's content. Community developed gem-based themes store some site's directories (e.g assets, _layouts, _includes) inside a gem, hidden from the user. All of these directories can be read, processed and their content can be extended or overridden as needed. 

The default Jekyll theme is called `minima`. Layouts are templates that wrap around content and allow for an easy definition of a site-wide navigation, footer, page style... Minima theme has two layouts - the `page` and the `post` layout (and the `home` and `default` layouts).



## Community Developed Themes

It is possible to find existing themes on following links:

* https://jekyllthemes.io/free
* http://jekyllthemes.org/
* https://rubygems.org/search?utf8=%E2%9C%93&query=jekyll-theme

As an example we will use the [Cayman theme](https://github.com/pages-themes/cayman). Open the *Gemfile* file and add the following line:

```ruby
gem 'jekyll-theme-cayman', '~> 0.1.1'
```

After that run `bundle install` in order to install the new theme. In order to use this theme, open the *_config.yml* file and change the line `theme: minima` to `theme: jekyll-theme-cayman`. The cayman theme does not provide `post` , `page` and `home` layouts so it is important to define them. 



## Layouts

It is possible to redefine existing layouts or define new layouts. To do this we make a new folder **_layouts** and inside make new files that will represent our layouts. A usual approach is to define a default layout ( **default.html**) with site-wide menu and footer and have other layouts inherit from it. It is also possible to define multiple page elements and use them as needed. Inside the **_layouts** folder we will define files *post.html*, *page.html* and *home.html*. We will use <u>**Liquid**</u> templating language to process templates and display content on the page. **<u>Liquid</u>** language can access variables using the `{{ variable }}` syntax and can perform logic statements using the `{% if statement %} {% endif %}`  syntax. The **<u>Liquid</u>** templating language will be described in more detail in the later posts. 

A simple layout for *post.html*:

```yaml
---
layout: default
---

{{ content }}
```

In order to list all the posts on the main page, we will define a new layout *home.html*:

```yaml
---
layout: default
title: "Home"
---

{{ content }}

{% for post in site.posts %}
  <article>
    <h2>
      <a href="{{ post.url }}">
        {{ post.title }}
      </a>
    </h2>
    <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
  </article>
{% endfor %}
```

**<u>Liquid</u>** language allows for a lot more customization. 



## References

1. Jekyll docs - themes: https://jekyllrb.com/docs/themes/
2. Jekyll docs - layouts: https://jekyllrb.com/docs/layouts/
3. Jekyll docs - Liquid: https://jekyllrb.com/docs/liquid/