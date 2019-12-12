---
layout: post
title: Handling Dialog Cancel Event
tags: [Modal, Event, JavaScript]
---

If you ever had to handle a modal dialog close to trigger some action on the parent page, you probably used a dynamic action using the "Dialog Closed" event.

When closing a modal dialog there are two ways to do it.
 1. Close
    - Using an after submit process of type "Close Dialog";
    - Using a dynamic action with a "Close Dialog" action;
    - Branching to a page that has a "Normal" page mode.
 2. Cancel
    - Using a dynamic action with a "Cancel Dialog" action;
    - Clicking on the top right "X" icon/button.

When using a branch to close the modal dialog, the modal dialog will close then it's parent will branch to the specified page.

Except when using the branch method, when you close the modal dialog, APEX will trigger a "Dialog Close" event. Then, on the parent page, you will be able to handle it using a dynamic action "Dialog Closed" event.
The thing is that the cancel methods will not trigger any event on the parent page. So, by default, you won't be able to handle the dialog close when it was cancelled.

One way to have both the close and cancel method trigger an even on the parent page would be to override the dialog close event (APEX is using [jQuery UI Dialog](http://api.jqueryui.com/dialog/){:target="_blank"}).

So what we will do is this.

You will need to define the following JavaScript function (either on the parent pages, on page 0 or in your JavaScript global library file)
```javascript
function customEvent(event, data){
    apex.event.trigger(document, event, data);
}
```

Then, under the modal dialog page attributes, in the dialog section, set the "Attributes" to:
```javascript
close: function() { customEvent('customDialogClose', {modalPageId: 'MODAL_CLOSE_FIXED'});}
```

What this will do is that it will trigger (on the parent page) the event "customDialogClose".
The second parameter is a data attribute that could be used to differentiate modals between each other. It can can be useful if you are calling more than one on the parent page or if you want to send data back to the parent page.

Finally, in your parent page you can define a custom dynamic action as follow: 
```texte
Event: Custom
Custom Event: customDialogClose
Selection Type: JavaScript Expression
JavaScript Expression: document
```

One thing to note is that the default close event will still be triggered when using the close method.

You can have a look at my [Demo Application]({{ site.demo-app }}:2500){:target="_blank"}