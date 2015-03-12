---
layout: default
---



## Ever dreamed about real programming in CSS?

<div class="well">
<strong>Disclaimer:</strong> FuncSS is in the planning phase. <span style="color:inherit"><strong>Nothing on this page is reality yet</strong>, this is just the initial plan.</span>
</div>

### What is it?

**FunCSS** will be a stylesheet language that looks much like CSS. But it is a *real* programming language, with advanced features for structuring code. You can define your own versions of most CSS elements, e.g. functions, selectors, properties, but also more exotic ones like units or media queries. All these will be dynamically handled either compile-time or run-time, depending on the definition.

### What is it good for?

FuncSS aims to fulfill the following goals for a better CSS coding experience:

* **Cleaner, structured code.** FuncSS lets you define new elements from existing ones or with JavaScript, and this helps to avoid code repetition. You can define custom shorthand properties, which may influence child elements, add new elements, or even have a different definition in different conditions (e.g. different appearance in older browsers). This enables an aspect-oriented programming style. There's no need to add vendor prefixed properties -- FuncSS can do it automatically. 

* **Use CSS to code behavior.** CSS selectors are so powerful for specifying styles, why not use them for behavior also? Actually, jQuery does extactly that. But in FuncSS you can use a truly declarative language for defining behavior -- and it will automatically handle changes in the DOM: e.g. when the class of an element changes, its behavior will change, without writing any update code. You can define new state pseudoclasses, similar to `:hover` and `:focus`, and change style or behavior based on a custom condition or an event. You can use JavaScript to define property values and make it depend on the state of DOM elements or JavaScript variables.

* **Better animations.** CSS transitions and animations are cool, but there are too few easing types in CSS. No problem, in FuncSS you can define new easings, or use the ones in easings.js. In this case, FuncSS will take over the animation and do it in pure JavaScript in the background. Or do you want to do an easing in the function of scroll position? Just use an easing function in combination with the `page-scroll-y()` library function, and there you go. All styles that depend on the scroll position will be updated when the user scrolls the page.

* **Browser compatibility for free.** A compatibility layer ensures that if a browser does not support a selector or a property, the page will still work as you coded it with the latest CSS. You have to specify the browser versions you want the compiled code to support.


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
#picture:toggled {
    transform:
        translate(0,-48%)
        rotate(pictureAngle())
        translate(0,48%);
}
@pseudoclass :toggled :on(click/click);
@function pictureAngle():<angle>
    sin(t() / 3s * 360deg) * 10deg;
{% endhighlight %}


</div>
</div>

### How will it work?

Library functions like `t()` (which returns the time spent since page loading) will track calls to them and update the system when their value changes. Then the CSS will be updated whenever their value changes. If needed, it will set up an interval or an event handler. All this will be done by a tasty mixture of the hilarious [jQuery](http://jquery.com/) and the awesome [Tracker](http://www.meteor.com/tracker) libraries.

### When can we get it?

A working prototype will be released in the following months. You can already look at the [FuncSS repository](https://github.com/funcss-lang/funcss) on Github.

### What other features will it have?

For a complete list of planned features, see the [Trello board](https://trello.com/b/EpfkVhaA/funcss).

### Will it be open-source?

Yes. The language specifications will be released with an open license, and the Reference Implementation will be open-source, with MIT license. 

### Will it support my CSS preprocessor?

Probably. The syntax of FuncSS is similar to pure CSS. Most CSS preprocessors will be able to process and generate the code needed for FuncSS, except for custom at-rules. So a solution is to only pass your preprocessor through a pure CSS-like part of your FuncSS code. This can be achieved with `@include`s. You can `@include "myfile.less";`, and the FuncSS compiler will run LESS on it before parsing it.


