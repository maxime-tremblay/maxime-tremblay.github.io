---
layout: post
title: Datepicker Customization
tags: [Interface, Datepicker, JavaScript]
---

Back in 2010, the Oracle Application Express release 4.0 included the jQuery JavaScript library as well as the jQuery UI JavaScript library. With it came the new revision of the datepicker item based on the jQuery UI's widget as we have it today. Most of the widget's options are available to us as item attributes.
But, there might come a time when you get asked or need to change some option that is not available.

Maybe you need to change the first day of the week to Monday instead of Sunday, or need to disable some days, etc.

For a list of all available options and the utility functions, you should have a look at the [Datepicker Widget API Documentation](http://api.jqueryui.com/1.10/datepicker/){:target="_blank"}.

There are a couple of nice hidden features that you might not know existed.
Let's have a look at a couple of them.

Changing the first day of the week to Mondays:
```javascript
$('#P1000_DATE_3').datepicker("option", "firstDay", 1);
```

Disabling the selection of weekends using built-in utility function:
```javascript
$('#P1000_DATE_4').datepicker("option", "beforeShowDay", $.datepicker.noWeekends);
```

Disabling the selection of Mondays:
```javascript
function disableMondays(pDate){
    var lTooltipDate = "Tooltip for disabled dates";
    if (pDate.getDay() === 1) {
        return [false, 'disabledDayClass', lTooltipDate];
    }
    else {
        return [true, null, null];
    }
}

$('#P1000_DATE_5').datepicker("option", "beforeShowDay", function(date) {return disableMondays(date);});
```

However, if you change an option for a datepicker item, you'll notice that the icon trigger will look different.

{% include images.html name="Datepicker-APEX5.0.png" alt="Datepicker APEX5.0" class="center-block" width="400px" %}

{% include images.html name="Datepicker-APEX5.1.png" alt="Datepicker APEX5.1" class="center-block" width="400px" %}

So what's going on exactly?  
Let's have a look at the html.

Before changing an option:  
```html
<input type="text" class="datepicker apex-item-text apex-item-datepicker hasDatepicker" id="P1000_DATE_1" name="P1000_DATE_1" maxlength="" size="30" value="" autocomplete="off">
<button type="button" class="ui-datepicker-trigger a-Button a-Button--calendar">
<span class="a-Icon icon-calendar"></span>
    <span class="u-VisuallyHidden">Popup Calendar: Date<span></span></span>
</button>
```

After changing an option:  
```html
<input type="text" class="datepicker apex-item-text apex-item-datepicker hasDatepicker" id="P1000_DATE_1" name="P1000_DATE_1" maxlength="" size="30" value="" autocomplete="off">
<button type="button" class="ui-datepicker-trigger">
<span class="a-Icon icon-calendar"></span>
    <span class="u-VisuallyHidden">Popup Calendar: Date<span></span></span>
</button>
```

We can see that the button element is missing two APEX classes after an option is changed: `a-Button` and `a-Button--calendar`

So, to fix the issue with the button trigger we simply need to add the classes back.
That's also exactly what APEX is doing on page load for each datepicker item.
```javascript
(function() {
    apex.widget.datepicker("#P1000_DATE_1", {
        "buttonImageOnly": false,
        "buttonText": "\u003Cspan class=\u0022a-Icon icon-calendar\u0022\u003E\u003C\u002Fspan\u003E\u003Cspan class=\u0022u-VisuallyHidden\u0022\u003EPopup Calendar: Date\u003Cspan\u003E",
        "showTime": false,
        "defaultDate": new Date(2018, 1, 26, 20, 32, 47),
        "showOn": "button",
        "showOtherMonths": false,
        "changeMonth": false,
        "changeYear": false
    }, "dd-M-y", "en");

    apex.jQuery('#P1000_DATE_1').next('button').addClass('a-Button a-Button--calendar');
})();
```

Having a look again at our first example (changing the first day of the week to Mondays). We should use something like this:  
```javascript
$('#P1000_DATE_3').datepicker("option", "firstDay", 1).next('button').addClass('a-Button a-Button--calendar');
```

Now, what if you would like to change an option for every datepicker in your application.

Once a datepicker is initialized a "hasDatepicker" class is added to the element. So instead of using the item ID as the jQuery selector, we could use that class and have the code execute on page load.

```javascript
$('.hasDatepicker').datepicker("option", "firstDay", 1).next('button').addClass('a-Button a-Button--calendar');
```

If the previous code is not working as expected, it my be due to a timing issue. Since the code to customize the datepicker items is executed on page load and that the dapicker are initialized on page load also. The customizing code could be running before the actual initialization. To fix that you can add a short delay to it.

You can have a look at my {% include demo.html label="Demo Application" page="3200" %}

Enjoy! 