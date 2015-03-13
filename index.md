---
layout: default
---



## Ever dreamed about real programming in CSS?

<div class="well">
<strong>Disclaimer:</strong> FunCSS is in the planning phase. <span style="color:inherit"><strong>Nothing on this page is reality yet</strong>, this is just the initial plan.</span>
</div>

### What is it?

**FunCSS** will be a stylesheet language that is a superset of CSS. But it is also a *real* programming language, with a rule-based + functional reactive paradigm. CSS elements (functions, selectors, properties, units, etc.) are first-class citizens, you can define your own versions of them, either using existing ones or with JavaScript. FunCSS code is compiled to a mixture of plain CSS and JavaScript, and runs in the browser.

*FunCSS aims to be for CSS what AngularJS is for HTML and jQuery is for JavaScript: giving superpowers while keeping the original syntax and semantics.*

### What is it good for?

It aims to fulfill the following goals:

* **Cleaner, structured code.** FunCSS lets you define new elements from existing ones, and this helps to avoid code repetition. For example, you can define custom selectors to avoid repeating selector patterns. Similarly for functions, colors, units and many more.  You can define custom shorthand properties, which can change many properties at once -- this enables an aspect-oriented programming style. 

* **Safer coding.** FunCSS is statically typed, with a type system taken directly from the CSS specification. The static type system helps you find bugs compile-time. The FuncSS Lib contains the declaration of all standard CSS properties, so you can know if you have misspelled a property name, or given an invalid value (even a computed value), without rendering the page.

* **Use CSS to code behavior.** CSS selectors are so powerful for specifying styles, why not use them for behavior also? (Actually, jQuery does exactly that, but from the other direction.) In FunCSS you can use a truly declarative language for defining behavior. A minimal support for event handling is included: you can define new state pseudoclasses, similar to `:hover` and `:focus`, and change style or behavior based on an event. You can use JavaScript to define property values and make it depend on the state of DOM elements or JavaScript variables. Write less JavaScript, more FunCSS.

* **Better animations.** CSS transitions and animations are nice, but there are only a few easing types in CSS. In FunCSS you can define new easings, or use the ones from easing.js (FuncSS will take over the animation and do it in JavaScript if a custom easing is used). Or do you want to make a style depend on the scroll position? Just use an easing function in combination with the `page-scroll-y()` library function, and there you go. All styles that depend on the scroll position will be updated  automatically when the user scrolls the page.

* **Browser compatibility made easier.** A compatibility layer ensures that if a browser does not support a selector or a property, the page will still work as you coded it with the latest CSS. It will add vendor prefixes or polyfills automatically if available, without using mixins. You can define your own workarounds when no polyfill is available.

### How does it differ from LESS/Sass?

There are quite a few qualities in which FunCSS supersedes LESS or Sass:

* **Dynamic.** LESS and  Sass are CSS preprocessors: they output CSS, so their output is static. FunCSS is a programming language that compiles to CSS and JavaScript -- it can do anything JavaScript can do. In FunCSS you can define a property that depends on the mouse position or the scroll position. In LESS and Sass you cannot.

* **Semantic.** In LESS and Sass you can define variables for, say, colors. This is purely syntactic: the value of the variable is copied to the property value where you use it. In FunCSS you can define new named colors, and the compiler knows when an identifier is meant to be a color. 

* **Type-safe.** FunCSS has a static type sytem, and it knows the complete CSS specification. If you specify a value that is not allowed for a property, it will notify you compile-time. In LESS and Sass you don't really notice this until you render a page which uses that particular property.

* **Cleaner syntax.**  In LESS and Sass you often use mixins for tasks like vendor prefixing and responsiveness. In FunCSS, you mostly use standard CSS syntax with non-standard names.

### How will we use it?

In this example we define a pseudoclass which activates and deactivates when the element is clicked. We also define a custom function.
Click on the picture.

<div class="row">
<div class="col-md-6">

<!--
{% highlight javascript %}
$F.pictureAngle = function() {
    return Math.sin($F.t() * 3) * 0.08;
}
{% endhighlight %}
-->
<center>
<img src='img/picture.svg' id="picture" width='120'>
</center>

<script>
pictureAngle = function() {
    return Math.sin(new Date().getTime() / 1000 * 3) * 0.08;
}
$(function() {
    var $picture = $("#picture");
    var int;
    $picture.click(function() {
        if(int) {
            clearInterval(int);
            $picture.css("transform", "");
            int = false;
        } else {
            int = setInterval(function() {
                $picture.css("transform", "translate(0,-48%)rotate("+pictureAngle()+"rad)translate(0,48%)");
            }, 40);
        }
    });
})
</script>


</div>
<div class="col-md-6">

{% highlight css %}
@pseudoclass :toggled :on(click/click);
#picture:toggled {
    transform:
        translate(0,-48%)
        rotate(pictureAngle())
        translate(0,48%);
}
@function pictureAngle():<angle>
    sin(t() / 3s * 360deg) * 10deg;
{% endhighlight %}


</div>
</div>

### How will it work?

Library functions like `t()` (which returns the time spent since page loading) will track calls to them and update the system when their value changes. Then the CSS will be updated whenever their value changes. If needed, it will set up an interval or an event handler. All this will be done by a tasty mixture of the hilarious [jQuery](http://jquery.com/) and the awesome [Tracker](http://www.meteor.com/tracker) libraries.

### When can we get it?

A working prototype will be released in the following months. You can already look at the [FunCSS repository](https://github.com/funcss-lang/funcss) on Github.

### What features will it have?

The following custom elements are planned to be definable:

- functions
- pseudoclasses
- shorthand properties
- types
- units
- media queries
- pseudoelements
- at-rules
- colors
- easings
- transforms

For a complete list of planned features and details, see the [Trello board](https://trello.com/b/EpfkVhaA/funcss).

### Will it be open-source?

Yes. The language specifications will be released with an open license, and the Reference Implementation will be open-source, with MIT license. But anyone will be allowed to make a commercial implementation.

### Can I support the project?

Please, send comments, suggestions and questions to <kallo.bernat@gmail.com>. Your advice is very needed.

### Who is developing it?

I'm Bernát Kalló, a student of EIT ICT Labs Master School at ELTE, Budapest. This is my Master's thesis project. I'm working as a web developer part-time. I'm living with my parents, my grandma, my two brothers and my sister.
