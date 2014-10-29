---
layout: post
title: How I filter posts in my Jekyll blog
category: articles
tags: [jekyll]
lang: eng
---
Some time ago I decided to write a part of my blog in english. There already was articles written in russian, thus I needed to apply some filtering mechanism to separate they into different pages.
At first, I had moved my old posts index page template into _includes directory and created two different layouts for both languages with simple content

{% highlight ruby %}
{% raw %}
{% include posts-index.html lang="eng" %}
{% endraw %}
{% endhighlight %}
and 
{% highlight ruby %}
{% raw %}
{% include posts-index.html lang="rus" %}
{% endraw %}
{% endhighlight %} 
Next, I added ```lang``` variable with corresponding value to the front matter of every post and used it in my partial template. Since my Jekyll theme uses non-trivial grouping of posts, it's impossible to use ```if``` statement, but Jekyll supports filtering and assigning to a new variable:
{% highlight ruby %}
{% raw %}
{% assign filtered = (site.posts | where: "lang", include.lang) %}
{% endraw %}
{% endhighlight %}
Now, ```filtered``` contains only required posts.