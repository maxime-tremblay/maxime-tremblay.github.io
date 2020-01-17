---
layout: post
title: Required Asterisk Left of Item Label
tags: [Interface, CSS]
---

If you ever had a customer asked you to move the required asterisk of the item's label before the item itself, you probably had to copy the existing template and move the span that holds the asterisk before the item itself then you had to go through all you labels to change the template.

Lately, I've been testing my demo application in the EA of APEX 5.1 and looking at the code and how things changed from 5.0 to 5.1.

Among all the changes, I noticed that the APEX team started to use the CSS3 [Order property](http://www.w3schools.com/cssreF/css3_pr_order.asp){:target="_blank"}.

> **Definition**  
> The order property specifies the order of a flexible item relative to the rest of the flexible items inside the same container.  
> **Note:** If the element is not a flexible item, the order property has no effect.

Basically, this property can reorder items within the same container granted that the container is using the flex property.

To move the asterisk span using only CSS, we can use the following code: 
```css
.t-Form-fieldContainer .t-Form-labelContainer {
  display: flex; /* Make sure the container is using flex */
  justify-content: flex-end; /* Keep items right aligned */
}

.t-Form--labelsAbove .t-Form-fieldContainer .t-Form-labelContainer,
.t-Form--leftLabels .t-Form-fieldContainer .t-Form-labelContainer,
.t-Form-fieldContainer.t-Form-fieldContainer--stacked .t-Form-labelContainer {
  justify-content: flex-start; /* Keep items left aligned */
}

.t-Form-fieldContainer .t-Form-labelContainer .t-Form-required {
  order: 1; /* Asterisk as first element */
}

.t-Form-fieldContainer .t-Form-labelContainer .t-Form-label {
  order: 2; /* Label as second element */
}
```

You can have a look at my {% include demo.html label="Demo Application" page="2700" %}

> **EDIT1:** Fix an issue with above labels. 

> **EDIT2:** Fix an issue with "Blank with Attributes" region template.

> **EDIT3:** APEX 5.1 now handles the required asterisk using CSS only and the position now depends on the label's alignment.
> Right aligned: asterisk before
> Left aligned: asterisk after