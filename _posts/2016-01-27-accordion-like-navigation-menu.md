---
layout: post
title: Accordion-Like Navigation Menu
date: '2016-01-27T13:43:00.001-05:00'
author: Maxime Tremblay
tags: [APEX5]
thumbnail: https://3.bp.blogspot.com/-wZnFBelsZjs/VryHuFVC52I/AAAAAAAAAFo/EyBjAfIspEk/s72-c/Accordion-Like%2BNavigation%2BMenu.gif
---

By default, it's only possible to expend the side navigation menu children submenu by clicking on the corresponding down arrow.

Here's how you can do if you would like to be able to do the same thing by simply clicking on the list entry text.

On your page 0, create a new dynamic action on page load that is going to run one the following javascript code depending on the target type you have on your list entry

*Use this one if you set your target type to URL and your URL target to #*
```
$('#t_Body_nav #t_TreeNav li.a-TreeView-node--topLevel > div.a-TreeView-content:has(a[href="#"])').click(function(){
    $(this).prev('span.a-TreeView-toggle').click();
});
```

*Use this one if you set your target type to - No Target -*
```
$('#t_Body_nav #t_TreeNav li.a-TreeView-node--topLevel > div.a-TreeView-content:not(:has(a))').click(function(){
     $(this).prev('span.a-TreeView-toggle').click();
});
```

This is going to look at all the top level list entries and if their link is equal to "#" (or if the entry has no link), it's going to trigger the arrow's click event when you click on the list entry text.
So basically, when you click on the text, it's going to be clicking on the arrow as well.

EDIT: If you want to use this for a multi-level menu, the javascript dynamic action code will need to be changed. After debug it, I found out that the submenu items are generated dynamically when expanding it's parent. So the click event from the above code is not registered for the new li tags. We need to
*Use this one if you set your target type to URL and your URL target to #*
```
$('#t_Body_nav #t_TreeNav').on('click', 'ul li.a-TreeView-node div.a-TreeView-content:has(a[href="#"])', function(){
    $(this).prev('span.a-TreeView-toggle').click();
});

```
*Use this one if you set your target type to - No Target -*
```
$('#t_Body_nav #t_TreeNav').on('click', 'ul li.a-TreeView-node div.a-TreeView-content:not(:has(a))', function(){
    $(this).prev('span.a-TreeView-toggle').click();
});

```
You can have a look at my <a href="http://max-playground.ddns.net/ords/f?p=DEMO:1000" target="_blank">Demo Application</a>

<div class="separator" style="clear: both; text-align: center;"><a href="https://3.bp.blogspot.com/-wZnFBelsZjs/VryHuFVC52I/AAAAAAAAAFo/EyBjAfIspEk/s1600/Accordion-Like%2BNavigation%2BMenu.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="240" src="https://3.bp.blogspot.com/-wZnFBelsZjs/VryHuFVC52I/AAAAAAAAAFo/EyBjAfIspEk/s320/Accordion-Like%2BNavigation%2BMenu.gif" width="320" /></a></div>