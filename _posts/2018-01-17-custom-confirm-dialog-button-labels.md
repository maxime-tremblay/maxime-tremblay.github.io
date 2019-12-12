---
layout: post
title: Custom Confirm Dialog Button Labels
tags: [Inline Dialog, Label, JavaScript]
thumbnail: https://1.bp.blogspot.com/-eBVyM7xfSJM/WlEszXvEomI/AAAAAAAABik/8iA_OODNABApVy_AyJYHEG27Vu2mSYbRwCLcBGAs/s72-c/confirm.png
---

Some time ago, someone on the apex.world Slack channel asked a question about the APEX confirm dialog. The question was if it was possible to change the labels of the confirm dialog buttons from "Cancel/Ok" to "No/Yes".

If we look at the [JavaScript APIs](https://docs.oracle.com/database/apex-5.1/AEAPI/JavaScript-APIs.htm#AEAPI266){:target="_blank"} documentation, we can see that there are three different ways that we can display a confirmation dialog:

- apex.confirm
- apex.page.confirm
- apex.message.confirm

> **Note**  
> The confirm function from the page namespace is different from the one in the confirm namespace. They both render the same confirmation dialog though.
> 
> **apex.confirm:** Alias for the apex.page.confirm function.
> 
> **apex.page.confirm:** Displays a confirmation dialog showing a message (pMessage) and OK and Cancel buttons. Depending on the user's choice, submits the page setting the request value to pRequest, or does not submit the page.
> 
> **apex.message.confirm:** Displays a confirmation dialog showing a message (pMessage), and OK and Cancel buttons. The callback function passed as the pCallback parameter is called when the dialog is closed, and passes true if OK is pressed and false otherwise.

The following JavaScript code:
```javascript
apex.message.confirm( "Are you sure?", function( okPressed ) {
    console.log(okPressed ? 'Ok' : 'Cancel');
});
```

Would display this dialog:

![Confirm Dialog](https://1.bp.blogspot.com/-eBVyM7xfSJM/WlEszXvEomI/AAAAAAAABik/8iA_OODNABApVy_AyJYHEG27Vu2mSYbRwCLcBGAs/s1600/confirm.png "Confirm Dialog"){:width="400px" class="img-responsive center-block"}

Now, back to the original question. What if we would like to change those button labels.

If we have a look at the JavaScript code of the apex.message.confirm function, we can see that the labels are based on some apex.lang messages (APEX.DIALOG.OK and APEX.DIALOG.CANCEL) and that there is no built-in way to change the labels.

But...

What we can do is change the values (using the JavaScript API of the [apex.lang](https://docs.oracle.com/en/database/oracle/application-express/19.2/aexjs/apex.lang.html){:target="_blank"} namespace) of the two messages and then call the confirm function. We should also revert the changes to the messages after that so that everything remains as it was initially.

Ok, so let's create a wrapper function on apex.message.confirm (the same also works for apex.page.confirm)  and add two parameters for the button labels.

The function could look like this:
```javascript
function customConfirm( pMessage, pCallback, pOkLabel, pCancelLabel ){
    var l_original_messages = {"APEX.DIALOG.OK":     apex.lang.getMessage("APEX.DIALOG.OK"),
                               "APEX.DIALOG.CANCEL": apex.lang.getMessage("APEX.DIALOG.CANCEL")};

    //change the button labels messages
    apex.lang.addMessages({"APEX.DIALOG.OK":     pOkLabel});
    apex.lang.addMessages({"APEX.DIALOG.CANCEL": pCancelLabel});

    //show the confirm dialog
    apex.message.confirm(pMessage, pCallback);
    
    //the timeout is required since APEX 19.2 due to a change in the apex.message.confirm
    setTimeout(function () {
    //changes the button labels messages back to their original values
    apex.lang.addMessages({"APEX.DIALOG.OK":     l_original_messages["APEX.DIALOG.OK"]});
    apex.lang.addMessages({"APEX.DIALOG.CANCEL": l_original_messages["APEX.DIALOG.CANCEL"]});
    }, 0);
}
```

Then, calling our function:
```javascript
customConfirm( "Are you sure?", function( okPressed ) {
    console.log(okPressed ? 'Ok' : 'Cancel');
}, "Yes", "No");
```

Would result in this:
![Custom Confirm](https://1.bp.blogspot.com/-73eOhk-0WTI/WlLk6qf2kkI/AAAAAAAABjE/krBSlYLa8-kdqSDkUnyMEG2JLoo1tZVmQCPcBGAYYCw/s1600/custom_confirm.png "Custom Confirm"){:width="400px" class="img-responsive center-block"}

or anything you want, like this:
![Custom Confirm](https://1.bp.blogspot.com/-HWbZ81cjSbY/WlO9NO8YG0I/AAAAAAAABjc/YnGgqJ09tFsvNlKuz0LNh6v9IMuLdCX-ACPcBGAYYCw/s1600/custom_confirm2.png "Custom Confirm"){:width="400px" class="img-responsive center-block"}

You can have a look at it in action in my [Demo Application]({{ site.demo-app }}:1700){:target="_blank"}

Enjoy!