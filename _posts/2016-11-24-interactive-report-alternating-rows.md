---
layout: post
title: Interactive Report Alternating Rows
tags: [INTERACTIVE, Report, IR, COLOR, ROW, ALTERNATE, ALTERNATING, APEX5]
thumbnail: https://3.bp.blogspot.com/-TI_bO7RzwTo/WDccZrprIkI/AAAAAAAAATc/0deMFpc0XxET6_PpV55-V7E_rl1W1iYegCLcB/s72-c/Alternating%2BRows%2B2.png
---

For classic reports there is a region attribute template option to have the rows have alternating row color.

![Alternating Rows Classic](https://2.bp.blogspot.com/-io52mkse_hs/WDcQvQZ_pdI/AAAAAAAAASk/MwCrgoDOgm4RHtaB7VNTUuu-pM5NhChmwCLcB/s1600/Alternating%2BRows%2B-%2BClassic.png "Alternating Rows Classic"){:width="400px" class="img-responsive center-block"}

That template option is not part of the interactive report template options.

![Alternating Rows Classic](https://2.bp.blogspot.com/--lVCmNgJGSs/WDcRBLaLjgI/AAAAAAAAASo/NejdkK2Tb3YGoY9ZB3l6ecV8ZrENtx8xwCLcB/s1600/Alternating%2BRows%2B-%2BInteractive.png "Alternating Rows Classic"){:width="400px" class="img-responsive center-block"}

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
![Alternating Rows](https://3.bp.blogspot.com/-JXfKXR3z_pY/WDcWyxASa3I/AAAAAAAAATA/K1fasAaCunIYByX7v4WQXFOkxiyzuvwEgCLcB/s1600/Alternating%2BRows.png "Alternating Rows"){:width="500px" class="img-responsive center-block"}

The classic report is using <span style="background-color: #fcfcfc; border-color: #000; display: inline-block; height: 15px; width: 15px;"> </span> #fcfcfc (very light gray) for the odd rows and nothing for the even rows.

```css
.customAlternatingRow .a-IRR-table tr:nth-child(odd) td {
    background-color: #fcfcfc;
}
```

Which would look like this:
![Alternating Rows 2](https://3.bp.blogspot.com/-TI_bO7RzwTo/WDccZrprIkI/AAAAAAAAATc/0deMFpc0XxET6_PpV55-V7E_rl1W1iYegCLcB/s1600/Alternating%2BRows%2B2.png "Alternating Rows 2"){:width="500px" class="img-responsive center-block"}

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

You can have a look at my [Demo Application]({{ site.demo-app }}:2900){:target="_blank"}