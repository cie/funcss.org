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

You can define new stylesheet functions in JavaScript. Currently only nullary functions are supported.

As a simple example, let's make a function that returns the opacity of a layer of stars, according to the current time, in `stars.js`:

{% highlight javascript %}
function starsOpacity() {
    return 1.3+(Math.cos(new Date().getHours() / 24 * Math.PI * 2)-1) * 1.2;
}
{% endhighlight %}

Now you can use it in property values in FuncSS, in `stars.fcss`

{% highlight css %}
@import "stars.js";

body {
    background-color: navy;
}
.stars-layer {
    opacity: starsOpacity();
}
{% endhighlight %}

What you need to do now is to compile the FuncSS file and the JS file into one JS file with FuncSS Compiler.

    funcss stars.fcss > stars.min.js

Then you can include the generated file into your HTML:

{% highlight html %}
<script src="stars.min.js"></script>
<img src="stars.png" class="stars-layer">
{% endhighlight %}

