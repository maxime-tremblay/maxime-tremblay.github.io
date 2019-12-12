---
layout: post
title: Copy Theme Roller Theme From One Application to Another
tags: [Universal Theme, Theme Roller]
thumbnail: https://3.bp.blogspot.com/-i0Zx6WGR1HE/VwPg2lXAJkI/AAAAAAAAAHs/j26syuVU4QgbM_iFkzhUy67ZF-DMrhKuw/s72-c/copy_universal_theme.gif
---

Here is how you can copy a theme roller custom theme from one application to the other.

From the application that has theme your source theme, open theme roller. Then open the developer tools and in the console run the following command
```javascript
apex.utr.config()
````

Copy that line to your clipboard.

Then in the destination application, open the theme roller and the developer tools.
Paste it into the console to load the configuration into Theme Roller.

Then you will only need to save this configuration as a new theme.

![Copy Universal Theme](https://3.bp.blogspot.com/-i0Zx6WGR1HE/VwPg2lXAJkI/AAAAAAAAAHs/j26syuVU4QgbM_iFkzhUy67ZF-DMrhKuw/s1600/copy_universal_theme.gif "Copy Universal Theme"){:class="img-responsive center-block"}