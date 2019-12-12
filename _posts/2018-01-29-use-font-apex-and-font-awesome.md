---
layout: post
title: Use Font APEX and Font Awesome Simultaneously
tags: [FONT AWESOME, ICONS, APEX5, FONT APEX]
thumbnail: https://2.bp.blogspot.com/-KUTIw5qWAnA/Wm9pmQK60uI/AAAAAAAABmY/4BlXI-f8P-kAXFSabBEButVHXcaLtSioQCLcBGAs/s72-c/Icons.png
---

APEX 5.0 gave us the ability to include the Font Awesome library in our applications. In APEX 5.1, Font APEX was added the the list of icon library.

Taken from the Universal Theme Sample Application:

> Font APEX is an all new icon library designed to complement Universal Theme. It was designed as a replacement for Font Awesome, the web's leading icon library, and therefore contains almost all of the Font Awesome icons, re-drawn on a 16x16 grid as line-icons, to match the aesthetic we wanted. We wanted to make it a seamless switch to go from Font Awesome to Font APEX, and therefore use the same "fa" prefix for the icons, making it easier than ever to move to entirely new icon library.

To include either Font Awesome or Font APEX in our application, we need to go under the application's Shared Components, then under Themes, select the theme and under the Icons section, we can select the library that we want to include.

What if we would, for some reason, like to include the two libraries and use some icons from one and some icons from the other.

Unfortunately, the library attribute only enables us to select one of them.

On top of that, since the two libraries are using the same "fa" prefix, we can't simply include both files.

On the other hand, Font Awesome includes the LESS and Sass files so that we can customize and build the library ourselves.


# What we'll do
The idea is to include the Font APEX library using the built-in attributes. We'll then need to customize Font Awesome so that it uses a different prefix, build it and include that custom version into our application.

# Building our customized Font Awesome
First, we'll need to head over to [http://fontawesome.io/](http://fontawesome.io/){:target="_blank"} and download the library.  
Once extracted, we get 4 folders:
- css
- fonts
- less 
- scss

Looking at either the LESS or Sass folder we'll see the different files required to build the library. You can choose whichever one you're most familiar with.

For what we're trying to achieve, we can focus specifically on the "variables" and the "font-awesome" files.

The variables file allows us to replace the "fa-css-prefix" variable.
By default, it's set to "fa", but let's change it to something different like "fawe".

Then, we can build the customized version of the library using the "font-awesome" file.

You can build LESS and Sass files with most text editors. There are also many desktop applications that are able to compile LESS and Sass.

Once our customized Font Awesome is built, we need to upload it to our application (either in the Static Files or on your Web Server).

# Using Font APEX and Font Awesome
First, we'll need to include our custom Font Awesome library. We can add it under the Shared Components by going into the User Interface Attributes and then selecting the Desktop interface. Under the Cascading Style Sheets Section, we can add the references to our file. 

Something like this:
```html
#APP_IMAGES#font-awesome/4.7.0/css/custom-font-awesome#MIN#.css
```

Using Font APEX will be just as usual. Use the corresponding "fa" class as seen on [https://apex.oracle.com/fontapex](https://apex.oracle.com/fontapex){:target="_blank"}

```html
<i class="fa fa-cog" aria-hidden="true"></i>
<i class="fa fa-trash-o" aria-hidden="true"></i>
<i class="fa fa-bars" aria-hidden="true"></i>
<i class="fa fa-envelope-o" aria-hidden="true"></i>
<i class="fa fa-key" aria-hidden="true"></i>
<i class="fa fa-shopping-cart" aria-hidden="true"></i>
<i class="fa fa-battery-half" aria-hidden="true"></i>
```

In order to use our customized Font Awesome, we will need to use our custom class prefix. In our case: "fawe".  
```html
<i class="fawe fawe-cog" aria-hidden="true"></i>
<i class="fawe fawe-trash-o" aria-hidden="true"></i>
<i class="fawe fawe-bars" aria-hidden="true"></i>
<i class="fawe fawe-envelope-o" aria-hidden="true"></i>
<i class="fawe fawe-key" aria-hidden="true"></i>
<i class="fawe fawe-shopping-cart" aria-hidden="true"></i>
<i class="fawe fawe-battery-half" aria-hidden="true"></i>
```

You'll then be able to use both at the same time, like this:
![Icons](https://2.bp.blogspot.com/-KUTIw5qWAnA/Wm9pmQK60uI/AAAAAAAABmY/4BlXI-f8P-kAXFSabBEButVHXcaLtSioQCLcBGAs/s1600/Icons.png "Icons"){:class="img-responsive center-block"}

You can have a look at it in action in my [Demo Application]({{ site.demo-app }}:2000){:target="_blank"}

You can also get the custom Font Awesome library: [here](https://drive.google.com/file/d/10b9jedIyqSNzOKdvF7HR3xFRkE85zG7a){:target="_blank"}

Enjoy!