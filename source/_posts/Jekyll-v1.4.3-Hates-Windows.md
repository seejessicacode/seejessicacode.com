---
title: Jekyll v1.4.3 Hates Windows.
date: 2014-04-07
categories:
- coding
tags:
- jekyll
- jekyll v1.4.3
- windows
---

I mentioned in a previous post that I couldn't use the latest version of Jekyll (v1.4.3 at the time of this post) and included a reference to <!-- more -->a [stackoverflow post][so-post]. While what I have to say is nothing you wouldn't be able to find out on your own by following that thread, maybe I can summarize it for you.

Jekyll commands:
```bash
jekyll build
jekyll serve

```

Resulted in this nonsense:
```bash
C:\Users\campbeja\Projects\campbeja.github.io>jekyll build
&nbsp;
Configuration file: C:/Users/campbeja/Projects/campbeja.github.io/_config.yml
&nbsp;
Source: C:/Users/campbeja/Projects/campbeja.github.io
&nbsp;
Destination: C:/Users/campbeja/Projects/campbeja.github.io/_site
&nbsp;
Generating... C:/Ruby193/lib/ruby/1.9.1/fileutils.rb:247:in `mkdir': Invalid argument - C:/Users/campbeja/Projects/campbeja.github.io/_site/C: (Errno::EINVAL)
```

Notice the extra <code>C:</code> in the last line? For reasons that I still don't fully understand, a Ruby script received an invalid file path. I had no idea how, am not familiar with Ruby, and my Google searches failed to find similar reported issues (this was back in December 2013 or January 2014.) Eventually I started looking at Ruby files listed in the stack trace.

Inexperienced with Ruby, I managed to debug by typing print statements throughout the called methods to show values returned, modified, digitally enhanced or whatever. I was lead to Page.rb's desitination() in the Jekyll source code. Though I identified that it was there that the file path string was getting messed up--I didn't know how to fix it and by this point I was fed up and focused on something else for a win.

Luckily when I returned to this issue, someone else had reported this issue (see linked stackoverflow post) and [Jekyll contributors were already talking about it][gh-issue].

Looks like Windows users will have to stick with version 1.4.2 until Jekyll v2.0.0 is out.

[so-post]: http://stackoverflow.com/questions/21137096/jekyll-error-running-jekyll-serve#
[gh-issue]: https://github.com/jekyll/jekyll/issues/1948
