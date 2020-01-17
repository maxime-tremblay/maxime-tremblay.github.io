---
layout: post
title: Close Modal Dialog When Clicking Outside
tags: [Modal, JavaScript]
---

A couple weeks ago someone on apex.world slack asked a question regarding how to capture the cancel dialog event.

Juergen Schuster came up with a solution using the dialog's page attribute "Attributes" (under the Dialog section) to add/define the dialog with a custom close callback when initializing it.
{% include images.html name="dialog_attribute.png" alt="Dialog Attribute" class="center-block" width="420px" %}

Using the same logic we can use it to define a new open callback that will trigger the close dialog method when clicking outside the dialog.

Let's define the following JavaScript function on the parent page (if you're going to be using this in more than one place, I suggest you define it either on the page 0 or in a global javascript file)
```javascript
function closeDialogClickOutside(elem){
   $('.ui-widget-overlay').click(function(){
      $(elem).dialog('close');
   });
}
```

Then we simply have to set call the function when the dialog opens.
Which we can do by setting the Dialog's attribute "Attributes" to this: 
```javascript
open: function( event, ui ) { closeDialogClickOutside(this); }
```

Here's what you will get:
{% include images.html name="close_dialog_click_outside.gif" alt="Close Dialog Click Outside" %}

You can have a look at my {% include demo.html label="Demo Application" page="1800" %}