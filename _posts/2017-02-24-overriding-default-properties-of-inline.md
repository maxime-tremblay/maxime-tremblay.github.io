---
layout: post
title: Overriding the Default Properties of Inline Dialogs
tags: [Inline Dialog, JavaScript]
---

When using inline modal, you can display them using the `openModal` JavaScript function.

That function is wrapping the jQuery UI Dialog Open method.
```javascript
/* **********************************************
     From Theme42.js
********************************************** */
window.openModal = function(pDialogId, pDialogTriggerId, pSetFocusId, pClear) {
        $("#" + pDialogId).dialog("open")
    }
```

What we can do to override the default properties is to set them either on page or right before calling the Open method.

Let's say we would like to have a smaller dialog (e.g. height of 200px)


**Option 1 - On page load**
```javascript
$('#INLINE_REGION_STATIC_ID').dialog('option', 'height', 200);
```

Then you can use
```javascript
openModal('INLINE_REGION_STATIC_ID');
```

or

```javascript
$('#INLINE_REGION_STATIC_ID').dialog('open');
```

**Option 2 - When openning the Dialog**
```javascript
$('#INLINE_REGION_STATIC_ID').dialog('option', 'height', 200).dialog('open')
```

For more information, you can have a look at the [Dialog Widget documentation](http://api.jqueryui.com/dialog/){:target="blank"}