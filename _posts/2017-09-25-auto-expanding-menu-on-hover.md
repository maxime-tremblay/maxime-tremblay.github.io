---
layout: post
title: Auto Expanding Menu on Hover
tags: [Interface, Navigation, JavaScript]
---

Today someone on the apex.world Slack asked a question about having the side navigation menu auto-expand when hovering it. So I thought I would share this with others as well.

It can be easily be done using only a couple of JavaScript lines of code:

**APEX 5 and 18**
```javascript
(function(ut, $) {

var TREE_NAV_WIDGET_KEY = 'nav';

$(window).on('theme42ready', function() {
    /* Make sure that the navigation menu is collapsed on page load */
    if (ut.toggleWidgets.isExpanded(TREE_NAV_WIDGET_KEY)){
        ut.toggleWidgets.collapseWidget(TREE_NAV_WIDGET_KEY);
    }

    /* Expand on mouse over, collapse on mouse out */
    $('.apex-side-nav.js-navCollapsed .t-Body-nav').hover(
        function(){
            ut.toggleWidgets.expandWidget(TREE_NAV_WIDGET_KEY);
        },
        function() {
            ut.toggleWidgets.collapseWidget(TREE_NAV_WIDGET_KEY);
        }
    );
});

})(apex.theme42, apex.jQuery);
```


**APEX 19+**
Starting with APEX 19.1, the `apex.theme42.toggleWidgets` is not exposed anymore, so we have to rely on trigger the click event of the menu toggle button.
```javascript
(function($) {
    
$(window).on('theme42ready', function() {
    /* Make sure that the navigation menu is collapsed on page load */
    if ($('.t-PageBody').hasClass('js-navExpanded')) {
        $('#t_Button_navControl').click();
    }

    /* Expand on mouse over, collapse on mouse out */
    $('.apex-side-nav .t-Body-nav').hover(
        function(){
            //only expand if the side menu is collapsed
            $('.t-PageBody:not(.js-navExpanded) #t_Button_navControl').click();
        },
        function() {
            $('#t_Button_navControl').click();
        }
    );
});

})(apex.jQuery);
```

First thing we need to do is make sure that the side navigation is collapsed.
Then we add a hovering handler using the jQuery [.hover()](https://api.jquery.com/hover/){:target="_blank"} on the navigation menu container.

You'll end up with something like this:

{% include images.html name="Auto-Expanding-Menu-Hover.gif" alt="Auto Expanding Menu on Hover" class="center-block" %}

Have fun!

You can have a look at my {% include demo.html label="Demo Application" page="1200" %}

> **Edit 09-27**
> Now triggers the [custom navigation menu event](https://apex.oracle.com/pls/apex/f?p=42:6200){:target="_blank"}.
> Also calls the delayResize function so that any sticky headers get resized correctly when the side navigation menu is expanded and collapsed.

> **Edit 09-28**
> Rewrote to use namespacing, wrapped using the "theme42ready" event and replaced the collapsed/expand calls with the universal theme functions.