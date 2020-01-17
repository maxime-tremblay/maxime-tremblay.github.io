---
layout: post
title: Right Side Column Page and Validation Error Message Region
tags: [Interface, CSS]
---

If you ever used the "Right Side Column" page template, you might have noticed that the validation error message region is displayed under the right side region's expand/collapse trigger button.

{% include images.html name="Error_Message_Region.png" alt="Right Side Column Page Band Validation Error Message Region" class="center-block" width="500px" %}

As you can see above, the expand/collapse trigger button is on top of the close notification "X" button.

There are two ways to go in order to fix that, both using CSS only.

*The first method* is to add some right margin to the notification region.

```css
.js-rightExpanded .t-Body-content .t-Body-alert,
.js-rightCollapsed .t-Body-content .t-Body-alert {
    margin-right: 40px; /* Width of the right side region's trigger button */
}
```

It will then look like this:
{% include images.html name="Fix_2.png" alt="Right Side Column Page Band Validation Error Message Region" class="center-block" width="500px" %}

*The second method* is to reposition the notification region on top of the right side region's trigger button.

```css
.js-rightExpanded .t-Body-content .t-Body-alert,
.js-rightCollapsed .t-Body-content .t-Body-alert {
    position: relative; /* Need to position the div for the z-index to work */
    z-index: 500; /* z-index of right side column is 490 */
}
```

It will then look like this:
{% include images.html name="Fix_1.png" alt="Right Side Column Page Band Validation Error Message Region" class="center-block" width="500px" %}