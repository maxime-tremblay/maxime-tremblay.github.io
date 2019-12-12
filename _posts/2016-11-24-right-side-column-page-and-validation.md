---
layout: post
title: Right Side Column Page and Validation Error Message Region
tags: [Interface, CSS]
thumbnail: https://3.bp.blogspot.com/-Kxxv4S2gb-I/WDb_G29pqoI/AAAAAAAAASE/_PzxXnkNb9UqZIW56LJ-bG1iCXSgZE8cQCLcB/s72-c/Right%2BSide%2BColumn%2BPage%2Band%2BValidation%2BError%2BMessage%2BRegion.png
---

If you ever used the "Right Side Column" page template, you might have noticed that the validation error message region is displayed under the right side region's expand/collapse trigger button.

![Right Side Column Page Band Validation Error Message Region](https://3.bp.blogspot.com/-Kxxv4S2gb-I/WDb_G29pqoI/AAAAAAAAASE/_PzxXnkNb9UqZIW56LJ-bG1iCXSgZE8cQCLcB/s1600/Right%2BSide%2BColumn%2BPage%2Band%2BValidation%2BError%2BMessage%2BRegion.png "Right Side Column Page Band Validation Error Message Region"){:width="500px" class="img-responsive center-block"}

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
![Right Side Column Page Band Validation Error Message Region](https://3.bp.blogspot.com/-8_BCHfzSVg4/WDb_GzecWhI/AAAAAAAAASA/CQ6bEmsfEAEqyPeXeoIzmwJqgzhK97UlwCEw/s1600/Right%2BSide%2BColumn%2BPage%2Band%2BValidation%2BError%2BMessage%2BRegion%2B-%2BFix%2B2.png "Right Side Column Page Band Validation Error Message Region"){:width="500px" class="img-responsive center-block"}

*The second method* is to reposition the notification region on top of the right side region's trigger button.

```css
.js-rightExpanded .t-Body-content .t-Body-alert,
.js-rightCollapsed .t-Body-content .t-Body-alert {
    position: relative; /* Need to position the div for the z-index to work */
    z-index: 500; /* z-index of right side column is 490 */
}
```

It will then look like this:
![Right Side Column Page Band Validation Error Message Region](https://2.bp.blogspot.com/-0Wu1EUGa8OU/WDb_G0sA-XI/AAAAAAAAASI/APX_FP1wHLEW0A1isYvKRWdKVpMCuNpOACEw/s1600/Right%2BSide%2BColumn%2BPage%2Band%2BValidation%2BError%2BMessage%2BRegion-%2BFix%2B1.png "Right Side Column Page Band Validation Error Message Region"){:width="500px" class="img-responsive center-block"}