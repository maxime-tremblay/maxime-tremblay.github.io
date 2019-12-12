---
layout: post
title: iOS Modal Scrolling
tags: [SCROLLING, MODAL, APEX5]
---

If you ever tried to scroll a modal page from within Safari on iOS you probably noticed that what is getting scrolled is the parent page content and not the actual modal content.

There is a simple fix for that:
```css
body .ui-dialog .ui-dialog-content{
    -webkit-overflow-scrolling: touch;
}
```

If you're not using the built-in modal, the idea is to add the css property to the wrapping element of the iframe.  
Let's say you're using Skillbuilders' Modal Plugin, you can use the following: 
```css
#cboxLoadedContent{
    -webkit-overflow-scrolling: touch;
}
```

You can have a look at my [Demo Application]({{ site.demo-app }}:2400){:target="_blank"}