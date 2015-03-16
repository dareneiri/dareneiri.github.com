---
layout: post
title: Adding Tags to the Jekyll Theme, Minimal Mistakes
tags: [jekyll]
published: true
excerpt: "Tags are a nice way to categorize posts, but aren't built into some themes. The jekyll theme Minimal Mistakes is awesome, and I provide detail on how to integrate tags."
comments: true
---

I really like using the Jekyll theme [Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/), made by [Michael Rose](https://mademistakes.com/). As I'm slowly working my way to build content on this site, I knew it would be helpful to organize my posts through tags, which Jekyll has support for through the [YAML front matter](http://jekyllbootstrap.com/lessons/jekyll-introduction.html#toc_9). However, much more is involved to really make use of tags and to have them nicely organized. There are [Jekyll tag plug-ins](http://jekyllrb.com/docs/plugins/#tags) you can add, but if you host your site on GitHub for free like me, they may not work if it's not part of the [GitHub plug-in repo](https://help.github.com/articles/using-jekyll-plugins-with-github-pages/).

This is a short write-up on how to integrate tags in the Jekyll theme Minimal Mistakes. It'll probably work similarly in other themes too, but I haven't explored that. The end result should look similar to the picture below:

<figure>
    <img src="{{ site.url }}/images/jekylltags.png" alt="tags">
</figure>

1. In your primary GitHub directory, create a new directory called `tags`
2. Create an `index.md` file, and copy-paste the following (courtesy of [https://github.com/lanyonm/lanyonm.github.io/blob/master/tags.html](lanyonm)):
```
---
layout: page
title: Tags
comments: false
---

{% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
<!-- site_tags: {{ site_tags }} -->
{% assign tag_words = site_tags | split:',' | sort %}
<!-- tag_words: {{ tag_words }} -->

<div id="tags">
  <ul class="tag-box inline">
  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
    <li><a href="#{{ this_word | cgi_escape }}">{{ this_word }} <span>{{ site.tags[this_word].size }}</span></a></li>
  {% endunless %}{% endfor %}
  </ul>

  {% for item in (0..site.tags.size) %}{% unless forloop.last %}
    {% capture this_word %}{{ tag_words[item] | strip_newlines }}{% endcapture %}
  <h2 id="{{ this_word | cgi_escape }}">{{ this_word }}</h2>
  <ul class="posts">
    {% for post in site.tags[this_word] %}{% if post.title != null %}
    <li itemscope><span class="entry-date"><time datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time></span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endif %}{% endfor %}
  </ul>
  {% endunless %}{% endfor %}
</div>
```
3. If you commit the changes, you'll end up with an unstylized page with all your posts listed, sorted by their tags. Now to add some style.
4. Go to `_sass/site.scss` and add the following to the top of the page, but below the first comment line (again, courtesy of [lanyonm](https://github.com/lanyonm/lanyonm.github.io/blob/master/_sass/main.scss):
<pre>
/*****************************************************************************/
/*
/* Tags
/*
/*****************************************************************************/

.tag-box {
  list-style: none;
  margin: 0;
  padding: 4px 0;
  overflow: hidden;
  *zoom: 1;
}

.tag-box:before, .tag-box:after {
  display: table;
  content: "";
  line-height: 0;
}

.tag-box:after {
  clear: both;
}

.tag-box.inline li {
  float: left;
  font-size: 14px;
  font-size: 0.875rem;
  line-height: 2.5;
}

.tag-box a {
  padding: 4px 6px;
  margin: 2px;
  background-color: #e6e6e6;
  -webkit-border-radius: 4px;
  -moz-border-radius: 4px;
  border-radius: 4px;
  text-decoration: none;
}

.tag-box a span {
  vertical-align: super;
  font-size: 10px;
  font-size: 0.625rem;
}

/*
```
5. Commit those changes and you should be set!
