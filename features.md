---
layout: default
permalink: /features/
title: Features
---

## Features

Whose features would you like to hear about?

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

### Reactive variables

Now let's make it depend on the position of the mouse pointer. In JS:

{% highlight javascript %}
var mouseY = new ReactiveVar;
$(body).on("mousemove", function(e) {
    mouseY.set(e.pageY);
});
FuncSS.functions({
    starsOpacity: function() {
        return mouseY.get();
    }
});
{% endhighlight %}

The FuncSS code is the same:

{% highlight css %}
.stars-layer {
    opacity: starsOpacity();
}
{% endhighlight %}

Now the style will automatically apply when the mouse is moved.


### Custom pseudoclasses

Not only you can define custom properties, but also pseudoclasses.

{% highlight javascript %}
var chosenItem = new ReactiveVar;
$(".item").on("click", function(e) {
    chosenItem.set(this);
});
FuncSS.pseudoclasses({
    ":chosen": function() {
        chosenItem.equals(this);
    }
});
{% endhighlight %}

Now you can use it in selectors:

{% highlight css %}
.item:chosen {
    background: yellow;
}
{% endhighlight %}

