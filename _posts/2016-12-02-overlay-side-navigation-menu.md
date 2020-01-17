---
layout: post
title: Overlay Side Navigation Menu
tags: [Interface, Navigation, CSS]
---

In the last couple of weeks, I've been playing with the side navigation menu. By default, the side navigation menu "pushes" the page content back and forth as it expands and collapses.
Which looks just like this:
{% include images.html name="Default_Side_Menu.gif" alt="Default Side Menu" class="center-block" width="320px" %}

By overriding the Universal Theme's CSS related to the side navigation menu, I was able to make the menu display as an overlay.

I've also tested the solution on the Apex 5.1 EA2 and noticed that the html markup of the menu changed quite a bit in order to handle RTL applications.

You can retrieve both CSS here:
[https://github.com/maxime-tremblay/apex-css-overlay-sidemenu](https://github.com/maxime-tremblay/apex-css-overlay-sidemenu){:target="_blank"}

Then will need to include the corresponding CSS file either in the theme roller's custom CSS attribute or as an external file in your application's CSS files.

Additionally, by default, the side navigation menu remembers the previous state it was in. So if on a page you expand the menu and refresh it, the menu will be rendered as expanded.

What we can do to prevent that from happening is have some JavaScript code execute on page load that is going to collapse the menu if it's expanded.
```javascript
$('.t-PageBody.js-navExpanded #t_Button_navControl').click();
```

That code can be executed as a dynamic action on page 0 or in a global JavaScript file so that it's going to affect all pages in the application.

You will get something that looks like this:
{% include images.html name="Overlay_Side_Menu.gif" alt="Overlay Side Menu" class="center-block" width="320px" %}

If you would like to have the menu be fullscreen you can simply uncomment the fullscreen part at the end of the CSS file.

You can have a look at my {% include demo.html label="Demo Application" page="2600" %}