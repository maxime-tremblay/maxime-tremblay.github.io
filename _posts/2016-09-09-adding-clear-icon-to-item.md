---
layout: post
title: Adding a Clear Icon to an Item
tags: [Interface, Button, JavaScript, CSS]
---

Here's how to add a clear icon to an item (similar to the calendar icon of the datepicker item).
Since the datepicker's icon has the same look and feel as what we want, let's reuse the same CSS and html.

Let's inspect the html code of the datepicker's icon:

```html
<button class="ui-datepicker-trigger a-Button a-Button--calendar" type="button">
    <span class="a-Icon icon-calendar"></span>
    <span class="u-VisuallyHidden">Popup Calendar: Date Picker</span>
</button>
```  


 - ui-datepicker-trigger: class used to handle the click event
   - Let's rename that to 'clearItem-trigger'
 - a-Button: standard look and feel of buttons
   - Let's reuse it as we want the same look and feel
 - a-Button--calendar: additional css for the calendar icon
   - Let's rename that to 'a-Button--clearInput'
 - icon-calendar: image of the calendar</li>
   - Let's replace it with a clear icon: 'icon-remove'

We can then retrieve and adapt the CSS for the above classes from the Core.min.css.
We will then have the following CSS:

```css
.t-Form-inputContainer .a-Button--clearInput{
    margin-left: -.1rem;
    order: 3; /* Apex 5.1: Set the correct order */
}

.t-Form--large .a-Button.a-Button--clearInput,
.t-Form-fieldContainer--large .a-Button.a-Button--clearInput {
    padding: .8rem 1.2rem
}

.t-Form--xlarge .a-Button.a-Button--clearInput,
.t-Form-fieldContainer--xlarge .a-Button.a-Button--clearInput {
    padding: 1.4rem 1.2rem
}

.t-Form--login .a-Button.a-Button--clearInput {
    padding: 1rem 1.2rem
}
```

That's for the visual aspect of the icon.
Let's now add the following JavaScript code that will add the remove icon and that will handle the click event.

JavaScript code on page page load:

```javascript
$('.clearInput').each(function(){
    var lTriggerHtml = '<button class="clearInput-trigger a-Button a-Button--clearInput" data-item_id="' + $(this).attr('id') + '" type="button">'
                     +     '<span class="a-Icon icon-remove"></span>'
                     +     '<span class="u-VisuallyHidden">Clear Item\'s Value</span>'
                     + '</button>';
    $(this).after(lTriggerHtml);
});

$('.clearInput-trigger').click(function(){
    $('#' + $(this).data('item_id')).val('');
});
```

The first part will add the clear button after each element that has the 'clearInput' class.
The second part is used to handle the click event.

Now you simply have to add the 'clearInput' class (under the item's Advanced properties) to each item you want the clear button to be added.

One thing to note is that the above code will not trigger the item's change event.
If you would also like to trigger the change event, we could add an additionnal CSS class to the item like 'clearInput--change' and update the second part of the JavaScript code to:

We need to add the two following classes:

```javascript
$('.clearInput-trigger').click(function(){
    var triggeringElement = $('#' + $(this).data('item_id'));
    
    triggeringElement.val('');
    
    if (triggeringElement.hasClass('clearInput--change')){
        triggeringElement.change();
    }
});
```

We also need to update the JavaScript Code that adds the button so that it assigns the corresponding CSS class to the button.

```javascript
$('.clearInput').each(function(){
    var lClearInputClass = $(this).hasClass('clearInput--inside') ? 'a-Button--clearInputInside': 'a-Button--clearInput';
    var lTriggerHtml = '<button class="clearInput-trigger a-Button ' + lClearInputClass + '" data-item_id="' + $(this).attr('id') + '" type="button">'
                     +     '<span class="a-Icon icon-remove"></span>'
                     +     '<span class="u-VisuallyHidden">Clear Item\'s Value</span>'
                     + '</button>';
    
    $(this).after(lTriggerHtml);
});
```

Now supposed that you would like to have the icon be inside the element.
You need to have the element has right padding (equal to the width of the icon, 32px in our case) and you need to move the icon left by the same amount.

```css
.clearInput--inside{
    padding-right: 32px !important;
}

.t-Form-inputContainer .a-Button--clearInputInside{
    margin-left: -32px;
}
```

Simply have to set the 'clearInput clearInput--inside' class (under the item's Advanced properties) to each item you want the clear button to be added inside.

Final JavaScript:

```javascript
$('.clearInput').each(function(){
    var lClearInputClass = $(this).hasClass('clearInput--inside') ? 'a-Button--clearInputInside': 'a-Button--clearInput';
    var lTriggerHtml = '<button class="clearInput-trigger a-Button ' + lClearInputClass + '" data-item_id="' + $(this).attr('id') + '" type="button">'
                     +     '<span class="a-Icon icon-remove"></span>'
                     +     '<span class="u-VisuallyHidden">Clear Item\'s Value</span>'
                     + '</button>';
    
    $(this).after(lTriggerHtml);
});
 
$('.clearInput-trigger').click(function(){
    var triggeringElement = $('#' + $(this).data('item_id'));
     
    triggeringElement.val('');
     
    if (triggeringElement.hasClass('clearInput--change')){
        triggeringElement.change();
    }
});
```

Final CSS:

```css
.clearInput--inside{
    padding-right: 32px !important;
}

.t-Form-inputContainer .a-Button--clearInputInside{
    margin-left: -32px;
}

.t-Form-inputContainer .a-Button--clearInput{
    margin-left: -.1rem;
    order: 3; /* Apex 5.1: Set the correct order */
}
 
.t-Form--large .a-Button.a-Button--clearInput,
.t-Form-fieldContainer--large .a-Button.a-Button--clearInput {
    padding: .8rem 1.2rem
}
 
.t-Form--xlarge .a-Button.a-Button--clearInput,
.t-Form-fieldContainer--xlarge .a-Button.a-Button--clearInput {
    padding: 1.4rem 1.2rem
}
 
.t-Form--login .a-Button.a-Button--clearInput {
    padding: 1rem 1.2rem
}
```

Here's the end result:
{% include images.html name="input_clear_icon.gif" alt="Input Clear Icon" %}

You can have a look at my {% include demo.html label="Demo Application" page="2100" %}