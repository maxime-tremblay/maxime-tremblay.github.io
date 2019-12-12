---
layout: post
title: Switch and Radio as Pill Custom Colors
tags: []
thumbnail: https://3.bp.blogspot.com/-cD2_R9KvNoI/Wn-7-bZgXxI/AAAAAAAABp4/92MsI_MX_0YK1guUrdrmsozBLZudClXsACLcBGAs/s72-c/custom_color.png
---

There are two easy ways to have Toggle-like items in your applications.

One way is by using the Switch item type that will like this:
![Switch Item](https://2.bp.blogspot.com/-ucz5DsIUWEI/Wn-p3kbxwaI/AAAAAAAABog/657M3JLSRJoBT6p7io9UeyFHMtHWAbFqACLcBGAs/s1600/switch_item.png "Switch Item"){:width="320px" class="img-responsive center-block"}

If your switch items are displayed as select lists rather than as toggle items, you will need to go in your application's Shared Components, then in the Components Settings and edit the Switch item to change the Display Style attribute to Switch.

Another way is by using a Radio item. You'll need to change some attributes so that the item is displayed as a toggle.

First, you'll need to change the Number of Columns attributes to at least the amount of values you have. I like to use 999 so that if a new value is added to the list, I won't have to change the attribute again.

![Radio as Pill](https://4.bp.blogspot.com/-wczH25ygal0/Wn-pKGLxxpI/AAAAAAAABoY/EP2cbYiDMDoVLWNE-OT8hXlEU_csEHnhgCEwYBhgL/s1600/radio_as_pill_1.png "Radio as Pill"){:width="320px" class="img-responsive center-block"}

Then you'll need to change the Template Options so that the Radio Group Display is set to "Display as Pill Button".

![Radio as Pill](https://4.bp.blogspot.com/-YyWXN1Mh1Sw/Wn-pKPpGNFI/AAAAAAAABoU/WN2XGNX7AWgJxr3-XNUxyTSub74KpKFtACEwYBhgL/s1600/radio_as_pill_2.png "Radio as Pill"){:width="320px" class="img-responsive center-block"}

You will get a radio item that looks like this:
![Radio Item](https://2.bp.blogspot.com/-ray_3jIP20M/Wn-p3v5rXuI/AAAAAAAABok/l1LuxoVZ5eMB5Md0fWhyK2mB7o9yrwtaACLcBGAs/s1600/radio_Item.png "Radio Item"){:width="320px" class="img-responsive center-block"}

Now, let's customize their colors.

# Custom On/Off Colors
Let's define this CSS
```css
/* Custom On/Off Color - No Color */
.t-Form-fieldContainer--radioButtonGroup .customOnOffColor.apex-item-radio input:checked + label,
.customOnOffColor.apex-button-group input:checked+label {
    background-color: #EF9A9A;
}

/* Custom On/Off Color - Yes Color */
.t-Form-fieldContainer--radioButtonGroup .customOnOffColor.apex-item-radio input[value=Y]:checked + label,
.customOnOffColor.apex-button-group input[value=Y]:checked+label {
    background-color:#A5D6A7
}
```

In order to have the items use custom colors, we only need to set the CSS Classes to "customOnOffColor".

The yes value will be green and any other value will be red, like this:
![Custom On/Off Colors](https://2.bp.blogspot.com/--syb9E6YqYw/Wn-7-fuE8zI/AAAAAAAABqA/rX_WfnDZmSAMdrzM11aMsaPFlwwly1QOACLcBGAs/s1600/custom_on_off_colors.png "Custom On/Off Colors"){:width="320px" class="img-responsive center-block"}

# Custom On Color
Let's define this CSS 
```css
/* Custom On Color */
.t-Form-fieldContainer--radioButtonGroup .customOnColor.apex-item-radio input:checked + label,
.customOnColor.apex-button-group input:checked+label {
    background-color: #B3E5FC;
}
```

In order to have the items use custom color, we only need to set the CSS Classes to "customOnColor".

The selected value will be blue, like this:
![Custom On Color](https://2.bp.blogspot.com/-ENtmuHOxURc/Wn-7-fesohI/AAAAAAAABp8/jYL5pBa1Zdsu2S9VL_27cIYhWx1f9jX7ACLcBGAs/s1600/custom_on_colors.png "Custom On Color"){:width="320px" class="img-responsive center-block"}

For both the custom On/Off and On only colors, if you'd like to apply it for all items (Switch and Radio as Pill), you can simply remove the classes names from the above CSS.

You can have a look at it in action in my [Demo Application]({{ site.demo-app }}:2800){:target="_blank"}

Enjoy!