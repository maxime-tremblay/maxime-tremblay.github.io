---
layout: post
title: Using Font APEX in APEX 5.0
tags: [Icons, Font APEX]
---

{% include images.html name="FontApex.png" alt="Font APEX" class="mx-auto" width="320px" %}

APEX 5.1 introduced Font APEX, a new icon library designed to complement Universal Theme and to replace Font Awesome. The same "fa" prefix for the icons was kept so that it's easier to move from Font Awesome to this entirely new icon library.

Font APEX comes with a number of customizations built-in, enabling us to easily control the size, animation, rotation, and even add modifiers on top of icons. You can try customizing your icons using the Icon Builder in the [Universal Theme Sample Application](https://apex.oracle.com/fontapex){:target="_blank"}.

What if you are still on APEX 5.0 and would like to use it?

Don't worry you are able to do so.
Here's how you can do it.

First, let's get the Font APEX library files.
You can get them from the [APEX 5.1 installation](http://www.oracle.com/technetwork/developer-tools/apex/downloads/index.html){:target="_blank"} file under the `images\libraries\font-apex` folder (or from [here]({{"font-apex_(v1.0).zip" | prepend: postsAssetPrefix}}))

Then you will need to import these files in your application (let's do it using the Static Application Files for the sake of simplicity, but you could also import them in the Static Workspace Files or copy them on your web server).

> **Note:** zipping the font-apex folder will enable us to upload only that zipped file instead of every single file from the folder using the zip file will also keep the folder structure.


{% include images.html name="upload_files.png" alt="Upload Files" class="mx-auto" width="550px" %}

You will end up with the following files:
{% include images.html name="upload_files_2.png" alt="Upload Files" class="mx-auto" width="550px" %}

Then, let's remove the Font Awesome and include the Font APEX.
{% include images.html name="include_files.png" alt="Include Files" class="mx-auto" width="550px" %}

> **Notes:**  
> Step 4 removes the Font Awesome reference.  
> Step 5 uses the Font APEX CSS file reference from above step. Notice that the .min was replaced by #MIN#  
> 
> **From help text:**  
> If you provide a minified version of your file you can use the substitution string #MIN# to include .min or #MIN_DIRECTORY# to include minified/ in your file URL for a regular page view and an empty string if the page is viewed in debug mode.

At this point, if you try to run your application, you should be able to see most of the Font APEX icons.

There are some tweaks we still need to do so that everything is displayed nicely.
First, there is still a class that uses the "font-family: font-awesome;", which is used by the expand/collapse navigation menu button.

The other thing we need to change is the height of the icons.
Font Awesome uses 14x14 icons whereas Font APEX uses 16x16 icons. Some icons might not be displayed correctly. The expand/collapse navigation menu button is also one of those.

Here's the CSS that is required to fix these.

```css
.t-Icon[class*=' fa-'],.t-Icon[class^=fa-]{
    font-family: font-apex!important;
    font-size: initial;
}

.t-TreeNav .a-TreeView-node--topLevel&gt;.a-TreeView-content .fa{
    font-size: initial;
}
```

Enjoy Font APEX in your APEX 5.0 applications! 

> **Edit 1:** The Custom Prefix Class attribute needs to be set to "fa"

> **Edit 2:** Scott Wesley has a nice followup to this: [http://www.grassroots-oracle.com/2017/03/font-apex-between-versions.html](http://www.grassroots-oracle.com/2017/03/font-apex-between-versions.html){:target="_blank"}