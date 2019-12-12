---
layout: post
title: APEX 5.2 Page Designer Style for APEX 5.1
tags: [Interface, Page Designer]
thumbnail: https://2.bp.blogspot.com/-H6YPUx2e7BA/Wpn9acUYDKI/AAAAAAAABr4/f-W6L295rrU8uVA7ozvHgLOZm3fKp0eygCLcBGAs/s72-c/APEX5.2EA1.png
---

Have you been playing, trying and testing stuff on the Early Adapter of APEX 5.2?
If you haven't, it's still available (as of writing this) for you to try at [apexea.oracle.com](https://apexea.oracle.com/){:target="_blank"}.

If you have, you probably noticed that the user interface of the page designer was refined and is looking better than ever.

APEX 5.2 Page Designer:
![APEX5.2EA1](https://2.bp.blogspot.com/-H6YPUx2e7BA/Wpn9acUYDKI/AAAAAAAABr4/f-W6L295rrU8uVA7ozvHgLOZm3fKp0eygCLcBGAs/s1600/APEX5.2EA1.png "APEX5.2EA1"){:width="570px" class="img-responsive center-block"}

APEX 5.1 Page Designer:
![APEX5.1-Standard](https://2.bp.blogspot.com/-nwcfrfZ0VF0/Wpn9aSiOCdI/AAAAAAAABsA/vtEHhoto3wA3-FpdvPyvy0muxgq6tz0ygCEwYBhgL/s1600/APEX5.1-Standard.png "APEX5.1-Standard"){:width="570px" class="img-responsive center-block"}

After a while, you'll get use to the new look of the page designer and going back to 5.1 might feel weird.

Wouldn't it be nice if we could have the same look and feel on APEX 5.1.

We can actually achieve that and it's not that difficult.

The following is relying on CSS only, no JavaScript required. So there's no risk of breaking the page designer or any of its functionalities.

So how can we do it?

There's a super useful extension I used: [Stylish](https://userstyles.org/){:target="_blank"}
[Stylish](https://userstyles.org/){:target="_blank"}  
It's available on [Chrome](https://chrome.google.com/webstore/detail/.../fjnbnpbmkenffdnngjfgmeleoegfcffe){:target="_blank"}, [Firefox](https://addons.mozilla.org/en-US/firefox/addon/stylish/){:target="_blank"} and [Opera](https://addons.opera.com/en/extensions/details/stylish/){:target="_blank"}.

What it does is inject CSS for whatever website your tell it to.

How to set everything up:  
**Step 1.** Install the extension

**Step 2.** Create a new style

**Step 3.** Copy and paste the following code

```css
/* ------------------------------------------------------------------------------------------------------------------- */
/* APEX 18.1 Page Designer Style for APEX 5.1                                                                          */
/* Version: 1.1 (2018-03-16)                                                                                           */
/* Author:  Maxime Tremblay                                                                                            */
/*                                                                                                                     */
/* https://max-tremblay.blogspot.ca/2018/03/apex-52-page-designer-style-for-apex-51.html                               */
/*                                                                                                                     */
/* To be used with the Stylish Addon: https://userstyles.org/                                                          */
/*  - Chrome:  https://chrome.google.com/webstore/detail/stylish-custom-themes-for/fjnbnpbmkenffdnngjfgmeleoegfcffe    */
/*  - Firefox: https://addons.mozilla.org/en-US/firefox/addon/stylish/                                                 */
/*  - Opera:   https://addons.opera.com/en-gb/extensions/details/stylish/                                              */
/*                                                                                                                     */
/* Use with regexp URL: https?://(?:(?!apexea.oracle.com).)*f\?p=4000:4500.*                                           */
/* or any other URL you wish                                                                                           */
/*                                                                                                                     */
/* Using Gist: https://gist.github.com/maxime-tremblay/59c46c9f441801b6de0c88f72d0d63d9                                */
/* Served using: https://rawgit.com/                                                                                   */
/*                                                                                                                     */
/* ------------------------------------------------------------------------------------------------------------------- */

/* You can use the rawgit URL or copy everything from the Gist */
@import url('https://rawgit.com/maxime-tremblay/59c46c9f441801b6de0c88f72d0d63d9/raw/aa9877dad692317aa676b63911b6366631ee772d/APEX18.1-Page_Designer_for_APEX5.1.css');
```

**Step 4.** Define what website it should be applied to.

Since I'm working with APEX 5.1 everywhere, I'm using the regular expression `https?://(?:(?!apexea.oracle.com).)*f\?p=4000:4500.*` to apply it everywhere except apexea.oracle.com.

Here's the end result:

![APEX5.1-Custom](https://3.bp.blogspot.com/-GdAAogHARe8/Wpn9aV0ELiI/AAAAAAAABsI/gl6n0MAfujYY0xfgzkzzn9NhT5xjwgG-QCPcBGAYYCw/s1600/APEX5.1-Custom.png "APEX5.1-Custom"){:width="570px" class="img-responsive center-block"}

Of course not everything is the exact same. Everything that relies on new CSS classes or anything new will obviously not be replicated.

Here's a list of small differences
- Never element are not strikethrough
- Elements with unsaved changes don't have the left border highlight
- The property editor header is looking differently (buttons removed in 5.2 and search filter moved).

I've been using this for a couple of weeks now and I have to say that I really love it.

Enjoy!