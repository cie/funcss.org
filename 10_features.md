---
layout: default
permalink: /features/
title: Features
---

## Features

In the currently developed version of FuncSS (Level 1), the following features are available:

### Functions with a JavaScript body

You can define new stylesheet functions with a JavaScript body. Currently only nullary functions are supported. As a simple example, let's make a function that always returns the same value. In JS:

    FuncSS.functions({
        starsOpacity: function() {
            return 1/2;
        }
    });

You can use it in property values in FuncSS:

    .stars-layer {
        opacity: starsOpacity();
    }

### Reactive variables

Now let's make it depend on the position of the mouse pointer. In JS:

    var mouseY = new ReactiveVar;
    $(body).on("mousemove", function(e) {
        mouseY.set(e.pageY);
    });
    FuncSS.functions({
        starsOpacity: function() {
            return mouseY.get();
        }
    });

The FuncSS code is the same:

    .stars-layer {
        opacity: starsOpacity();
    }

Now the style will automatically apply when the mouse is moved.


### Custom pseudoclasses

Not only you can define custom properties, but also pseudoclasses.

    var chosenItem = new ReactiveVar;
    $(".item").on("click", function(e) {
        chosenItem.set(this);
    });
    @pseudoclass :chosen js(
        chosenItem.equals(this);
    );

Now you can use it in selectors:

    .item:chosen {
        background: yellow;
    }

## The future

In the planned future of FuncSS, there are plenty of new features besides these. You can read around on the
[Trello board](https://trello.com/b/EpfkVhaA/funcss) of the project.
