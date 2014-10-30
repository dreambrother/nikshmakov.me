---
layout: post
title: Some useful Bash one-liners
category: articles
tags: [bash, unix]
lang: eng
---
I've collected a few useful Bash one-liners and I want to share it with you. Unfortunately, this thought came to me very late and many snippets I've written so far are lost. But I will try to collect new one's and publish it.

Iteration over another program result

{% highlight bash %}
for i in `curl http://...`; do echo $i; done
{% endhighlight %}

Iteration with variable creation

{% highlight bash %}
arr=(`grep smth file`); for i in ${arr[@]}; do echo $i; done
{% endhighlight %}

Previous examples will split result by whitespaces (if you don't change ```$IFS```) but you can iterate line by line using this command

{% highlight bash %}
while read -r line; do
    echo $line
done < <(grep smth file)
{% endhighlight %}

Find substring in JSON

{% highlight bash %}
echo "\"foo\":\"111\",\"target\":\"OK\",\"bar\":\"222\"" | sed 's/.*"target":"\([^"]*\)",.*/\1/'
{% endhighlight %}

Take value of 10th column, remove following comma and print value if it's greater than 1000000

{% highlight bash %}
echo "2014-09-26 15:40:58,780 ...id... type=UploadToDefault, stage=payloadInfo, duration=0.034, sha256=..., md5=..., media-type=image, content_length=1922695, mime-type=image/jpeg, success=true" | awk '{ split($10, arr, "="); str=substr(arr[2],0,length(arr[2])-1); if ((str+0) > 1000000) print str }'
{% endhighlight %}

P.S.: [amazing tool](http://www.explainshell.com/)

**To be continued...**