---
layout: post
title: Button in Region Title
tags: [Button, APEX5, Region]
thumbnail: https://3.bp.blogspot.com/-tlrQaSzYd8o/VyjUCYggODI/AAAAAAAAAI4/s6AaJah2jvMd0RI1_3rGlQrsB98_HG6LgCLcB/s72-c/default_button_region.png
---


> **Note:** Instead of using the below code, it's easier to simply use the built-in button positions. Have a look at my demo application for a preview of the all the button position.

If you ever needed to display a button in a report header. You probably tried the "Right of Title" button position and got something like this :

![Default Button Region](https://3.bp.blogspot.com/-tlrQaSzYd8o/VyjUCYggODI/AAAAAAAAAI4/s6AaJah2jvMd0RI1_3rGlQrsB98_HG6LgCLcB/s1600/default_button_region.png "Default Button Region"){:class="img-responsive"}

The button is not right aligned in the region header, similar to what we get in an interactive report region using "Right of Interactive Report Search Bar" button region. You could always copy the region template and change it so that there is one button position in the header, but then you loose the subscription to the UT and you also have to copy every template you would want this to work.

We can achieve all that by simply using some CSS.

Let's start by defining the required CSS:

```css
/* Make sure the title container is stretched */
.buttonInHeader .t-Region-headerItems.t-Region-headerItems--title h2,
.buttonInHeaderWithExpand .t-Region-headerItems.t-Region-headerItems--title h2{
    display: block;
}

/* Have the buttons float right */
.buttonInHeader .t-Region-headerItems.t-Region-headerItems--title button,
.buttonInHeaderWithExpand .t-Region-headerItems.t-Region-headerItems--title button{
    float: right;
    margin-left: 5px;
}

/* Add extra space for the expand button */
.buttonInHeaderWithExpand .t-Region-headerItems.t-Region-headerItems--buttons{
    width: 40px;
}
```

I like to add these class in the Theme Roller CSS so that I can then use them from anywhere. 

Then we can simply add the class name in the region Class attribute.

![Button Region Attribute](https://3.bp.blogspot.com/-4Y-jnpR4mr8/Vypoh04SYPI/AAAAAAAAAJU/78YFolrl-lUpf5cRpGPWn60nOsqvMwqRACKgB/s1600/button_region_attributes.png "Button Region Attribute"){:class="img-responsive"}

And you will get this:

![Custom Button Region](https://4.bp.blogspot.com/-FRf_QQENTts/Vypo6IyVSwI/AAAAAAAAAJY/I5L0zXhVpuQ2BV_wty-f0cEFX1r2hlNFwCLcB/s1600/custom_button_region.png "Custom Button Region"){:class="img-responsive"}

One thing to remember is that when you have multiple buttons, they will need to be reversed in the page designer because of the float.

You can have a look at my [Demo Application]({{ site.demo-app }}:1600){:target="_blank"}