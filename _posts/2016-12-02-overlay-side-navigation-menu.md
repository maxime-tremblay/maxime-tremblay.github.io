---
layout: post
title: Overlay Side Navigation Menu
tags: [OVERLAY, CSS, NAVIGATION, Universal Theme, MENU, APEX5]
thumbnail: https://2.bp.blogspot.com/-jivlBcfyQHg/WEHgknEsS2I/AAAAAAAAAUs/zMuHQo5ueVEalgR0ccJWmfW2ncaTyYStgCLcB/s72-c/Default%2BSide%2BMenu.gif
---

In the last couple of weeks, I've been playing with the side navigation menu. By default, the side navigation menu "pushes" the page content back and forth as it expands and collapses.
Which looks just like this:
![Default Side Menu](https://2.bp.blogspot.com/-jivlBcfyQHg/WEHgknEsS2I/AAAAAAAAAUs/zMuHQo5ueVEalgR0ccJWmfW2ncaTyYStgCLcB/s1600/Default%2BSide%2BMenu.gif "Default Side Menu"){:width="320px" class="img-responsive center-block"}

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
![Overlay Side Menu](https://2.bp.blogspot.com/-zK1XIoqRUc0/WEHhCNrVh3I/AAAAAAAAAUw/Ml7yRHoQS5UhCLYZsn5i3cpXiL50tuXpACLcB/s1600/Overlay%2BSide%2BMenu.gif "Overlay Side Menu"){:width="320px" class="img-responsive center-block"}

If you would like to have the menu be fullscreen you can simply uncomment the fullscreen part at the end of the CSS file.

You can have a look at my [Demo Application]({{ site.demo-app }}:2600){:target="_blank"}