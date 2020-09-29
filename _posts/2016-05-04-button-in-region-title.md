---
layout: post
title: Button in Region Title
tags: [Interface, Region, CSS]
---

> **Note:** Instead of using the below code, it's easier to simply use the built-in button positions. Have a look at my demo application for a preview of the all the button position.

If you ever needed to display a button in a report header. You probably tried the "Right of Title" button position and got something like this :

{% include images.html name="default_button_region.png" alt="Default Button Region" class="mx-auto" %}

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

{% include images.html name="button_region_attributes.png" alt="Button Region Attribute" class="mx-auto" %}

And you will get this:

{% include images.html name="custom_button_region.png" alt="Custom Button Region" class="mx-auto" %}

One thing to remember is that when you have multiple buttons, they will need to be reversed in the page designer because of the float.

You can have a look at my {% include demo.html label="Demo Application" page="1600" %}