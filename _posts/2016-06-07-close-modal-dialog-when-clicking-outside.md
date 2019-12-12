---
layout: post
title: Close Modal Dialog When Clicking Outside
tags: [MODAL, APEX5, CLOSE]
thumbnail: https://2.bp.blogspot.com/-vjmVbCg3UyA/V1cdVfpjB1I/AAAAAAAAALk/vAGqlJkt75gsVydUtxRbMPtGaLDiWNIKQCKgB/s72-c/close_dialog_click_outside.gif
---

A couple weeks ago someone on apex.world slack asked a question regarding how to capture the cancel dialog event.

Juergen Schuster came up with a solution using the dialog's page attribute "Attributes" (under the Dialog section) to add/define the dialog with a custom close callback when initializing it.
![Dialog Attribute](https://4.bp.blogspot.com/-mUD55pMzs0c/V1cL2UGo1II/AAAAAAAAAKM/-7tHnY98hrEdJemZx2cl_NVxCyV1VS8tQCLcB/s1600/dialog_attribute.png "Dialog Attribute"){:width="420" class="img-responsive center-block"}

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
![Close Dialog Click Outside](https://2.bp.blogspot.com/-vjmVbCg3UyA/V1cdVfpjB1I/AAAAAAAAALk/vAGqlJkt75gsVydUtxRbMPtGaLDiWNIKQCKgB/s1600/close_dialog_click_outside.gif "Close Dialog Click Outside"){:class="img-responsive"}

You can have a look at my [Demo Application]({{ site.demo-app }}:1800){:target="_blank"}