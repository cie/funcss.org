---
layout: default
permalink: /features/
title: Features
---

## Features

The **FuncSS Language** is currently under development. You can read about its planned features on its [Trello board](https://trello.com/b/EpfkVhaA/funcss).

The **specifications** will reflect the finalized plans for the language. They are also being developed, you can read their content at the [Specifications](/spec/) page.

FuncSS has a **reference implementation**, called FuncSS RI, which will satisfy the specifications. It is also under development, and currently it supports much less features than what the language plans contain. On this page, you can read about the currently available features of FuncSS RI.


### Functions defined in JavaScript

You can define new stylesheet functions in JavaScript. Currently only nullary functions are supported, and currently you cannot embed JavaScript in FuncSS, only use the Api to create the functions.

As a simple example, let's make a function that returns the opacity of a layer of stars, according to the current time.

{% highlight javascript %}
FuncSS.functions({
    "starsOpacity()": function() {
        var d = new Date();
        return 1.3+(Math.cos(d.getHours() / 24 * Math.PI * 2)-1) * 1.2;
    }
});
{% endhighlight %}

Now you can use it in property values in FuncSS:

{% highlight css %}
.stars-layer {
    opacity: starsOpacity();
}
{% endhighlight %}

