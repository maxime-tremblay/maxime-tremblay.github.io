---
layout: post
title: Copy Theme Roller Theme From One Application to Another
tags: [Universal Theme, Theme Roller]
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

{% include images.html name="copy_universal_theme.gif" alt="Copy Universal Theme" class="mx-auto" %}