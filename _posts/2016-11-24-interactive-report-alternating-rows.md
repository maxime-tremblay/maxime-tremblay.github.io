---
layout: post
title: Interactive Report Alternating Rows
tags: [Interface, Interactive Report, CSS]
---

For classic reports there is a region attribute template option to have the rows have alternating row color.

{% include images.html name="Alternating_Rows_-_Classic.png" alt="Alternating Rows Classic" class="center-block" width="400px" %}

That template option is not part of the interactive report template options.

{% include images.html name="Alternating_Rows_-_Interactive.png" alt="Alternating Rows Classic" class="center-block" width="400px" %}

We can achieve the same effect in an interactive using once again some CSS.

```css
.customAlternatingRow .a-IRR-table tr:nth-child(odd) td {
    background-color: yellow;
}

.customAlternatingRow .a-IRR-table tr:nth-child(even) td {
    background-color: yellowgreen;
}
```

The only thing left to do is to add the "customAlternatingRow" class to your region (under Appearance, CSS Classes) or at the page level.

It will then look like this:
{% include images.html name="Alternating_Rows.png" alt="Alternating Rows" class="center-block" width="500px" %}

The classic report is using <span style="background-color: #fcfcfc; border-color: #000; display: inline-block; height: 15px; width: 15px;"> </span> #fcfcfc (very light gray) for the odd rows and nothing for the even rows.

```css
.customAlternatingRow .a-IRR-table tr:nth-child(odd) td {
    background-color: #fcfcfc;
}
```

Which would look like this:
{% include images.html name="Alternating_Rows_2.png" alt="Alternating Rows 2" class="center-block" width="500px" %}

If you would like to also change the highlighted/hovered row color, you can use the following CSS:

```css
.customRowHighlight .a-IRR-table tr:hover td {
    background-color: #f9f9f9;
}
```  

<span></span>

> **Note:**
> If you would like this to be applied on all interactive reports in your application, simply remove the `.customAlternatingRow` and/or `.customRowHighlight` from the CSS.

Browser Support of the :nth-child() Selector (from [w3school](http://www.w3schools.com/cssref/sel_nth-child.asp){:target="_blank"})

| Selector     | Chrome |  IE | Firefox | Safari | Opera |
|--------------|:------:|:---:|:-------:|:------:|:-----:|
| :nth-child() |   4.0  | 9.0 |   3.5   |   3.2  |  9.6  |

You can have a look at my {% include demo.html label="Demo Application" page="2900" %}