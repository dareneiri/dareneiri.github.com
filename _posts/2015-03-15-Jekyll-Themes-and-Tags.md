---
title: Adding Tags to the Jekyll Theme, Minimal Mistakes
tags: [jekyll]
published: true
excerpt: "Tags are a nice way to categorize posts, but aren't built into some themes. The jekyll theme Minimal Mistakes is awesome, and I provide detail on how to integrate tags."
comments: true
---

Please note that the latest version of Minimal Mistakes has tag support built in, so the process below is not required. Actually it was supported in [2016](https://github.com/mmistakes/minimal-mistakes/issues/243), and I originally wrote this in 2015. See [this an example of tag support in Minimal Mistakes here](https://mmistakes.github.io/minimal-mistakes/tags/)
{: .notice--warning}

I really like using the Jekyll theme [Minimal Mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/), made by [Michael Rose](https://mademistakes.com/). As I'm slowly working my way to build content on this site, I knew it would be helpful to organize my posts through tags, which Jekyll has support for through the [YAML front matter](http://jekyllbootstrap.com/lessons/jekyll-introduction.html#toc_9). However, much more is involved to really make use of tags and to have them nicely organized. There are [Jekyll tag plug-ins](http://jekyllrb.com/docs/plugins/#tags) you can add, but if you host your site on GitHub for free like me, they may not work if it's not part of the [GitHub plug-in repo](https://help.github.com/articles/using-jekyll-plugins-with-github-pages/).

This is a short write-up on how to integrate tags in the Jekyll theme Minimal Mistakes. It'll probably work similarly in other themes too, but I haven't explored that. The end result should look similar to the picture below:

<figure>
    <img src="{{ site.url }}/images/jekylltags.png" alt="tags">
</figure>

1. In your primary GitHub directory, create a new directory called `tags`
2. Create an `index.md` file, and copy-paste the following (courtesy of [lanyonm](https://github.com/lanyonm/lanyonm.github.io/blob/master/tags.html)):
{% gist dareneiri/571e163435df75959afb %}
3. If you commit the changes, you'll end up with an unstylized page with all your posts listed, sorted by their tags. Now to add some style.
4. Go to `_sass/site.scss` and add the following to the top of the page, but below the first comment line (again, courtesy of [lanyonm](https://github.com/lanyonm/lanyonm.github.io/blob/master/_sass/main.scss):
{% gist dareneiri/00c5aabc3bea37971935 %}
5. Commit those changes and you should be set!
