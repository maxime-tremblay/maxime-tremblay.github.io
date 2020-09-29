---
layout: post
title: APEX Items the Application Builder Style
tags: [Interface, Items, CSS]
---

The APEX application builder has the items look and feel different compared to what you get in a regular application.

{% include images.html name="Page_Designer.png" alt="Page Designer" class="mx-auto" width="400px" %}

You might think that they are looking good and that you would like to display them the same way in your application.

Here's the CSS you can use to do just that: 
```css
/* Removes borders from items */
.t-Form-inputContainer input[type="text"],
.t-Form-inputContainer input.text_field,
.t-Form-inputContainer input.password,
.t-Form-inputContainer input.datepicker,
.t-Form-inputContainer span.display_only,
.t-Form-inputContainer input.popup_lov,
.t-Form-inputContainer select,
.u-TF-item--text,
.u-TF-item--datepicker,
.u-TF-item--select,
.a-IRR-selectList[size="1"],
.t-Form-inputContainer select.selectlist[size="1"],
.t-Form-inputContainer select.yes_no,
.u-TF-item--select {
   background-color: transparent;
   border-top-color: transparent;
   border-left-color: transparent;
   border-right-color: transparent;
}

/* Removes decoration of the popup lov button */
.a-Button.a-Button--popupLOV {
    background-color: transparent;
    box-shadow: none;
}
.a-Button.a-Button--popupLOV:hover {
    background-color: #f8f8f8;
    box-shadow: 0 0 0 1px rgba(0, 0, 0, 0.125) inset;
}

/* Removes borders when displaying inline error  */
.t-Form-inputContainer input[type="text"].apex-page-item-error,
.t-Form-inputContainer input.text_field.apex-page-item-error,
.t-Form-inputContainer input.password.apex-page-item-error,
.t-Form-inputContainer input.datepicker.apex-page-item-error,
.t-Form-inputContainer span.display_only.apex-page-item-error,
.t-Form-inputContainer input.popup_lov.apex-page-item-error,
.t-Form-inputContainer select.apex-page-item-error,
.u-TF-item--text.apex-page-item-error,
.u-TF-item--textarea.apex-page-item-error,
.u-TF-item--datepicker.apex-page-item-error,
.u-TF-item--select.apex-page-item-error{
   border-top-color: transparent;
   border-left-color: transparent;
   border-right-color: transparent;
}

/* Removes borders when displaying inline error (required with valid state) */
.t-Form-inputContainer input[type="text"].apex-page-item-error:required:valid,
.t-Form-inputContainer input.text_field.apex-page-item-error:required:valid,
.t-Form-inputContainer input.password.apex-page-item-error:required:valid,
.t-Form-inputContainer input.datepicker.apex-page-item-error:required:valid,
.t-Form-inputContainer span.display_only.apex-page-item-error:required:valid,
.t-Form-inputContainer input.popup_lov.apex-page-item-error:required:valid,
.t-Form-inputContainer select.apex-page-item-error:required:valid,
.u-TF-item--text.apex-page-item-error:required:valid,
.u-TF-item--textarea.apex-page-item-error:required:valid,
.u-TF-item--datepicker.apex-page-item-error:required:valid,
.u-TF-item--select.apex-page-item-error:required:valid {
    border-top-color: transparent;
    border-right-color: transparent;
    border-left-color: transparent;
}

/* Fix the select list error border color */
.t-Form-inputContainer select.apex-page-item-error{
    border-color: #eb6562;
}
```

Basically, the CSS will hide the top, left and right border of the items, while keeping the bottom border as well as the border's defined color. When the item is focused, all borders will be displayed as usual.

You'll end up with something like this:
{% include images.html name="APEX_Items_Builder_Style.gif" alt="APEX Items Builder Style" class="mx-auto"%}

You can have a look at my {% include demo.html label="Demo Application" page="3300" %}

Have fun!