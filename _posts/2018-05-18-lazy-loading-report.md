---
layout: post
title: Lazy Loading Report
tags: [Performance, Interactive Report]
---

I was recently asked to have a look at an APEX page that took some time to load. That particular page was accessed using the navigation menu. Since the load time was longer than usual, users were often clicking multiple times on it while waiting.

As usual, I turned debug mode on and had a look at the result. It turned out to be the underlying query of the page's report that was slow.

We were able to fine-tune the query to make everything load faster. But it still took a couple of seconds to render.

What I did was to make the report lazy load the data, similar to what the Interactive Grid can do.

The idea is the following:
 - Create a hidden item on the page
 - Create a computation using the "After Regions" point to set the item to 'Y'
 - In the report, add a where clause that checks if the item's value is equal to 'Y'
 - Create a dynamic action on page load that refreshes the report

What this is doing is that when the report is being rendered for the first time, the calculation has not been executed and the item is still null so that the report will show nothing.
Then, the calculation will be executed and the dynamic actions will refresh the report showing the expected results.

Don't get me wrong here, the overall process is still going to take the exact same time.
If the page is taking 10 seconds to load, it will still take 10 seconds for the page to fully load.
But, the user experience is going to be a lot better because now the page will load instantaneously, then the report will take some time to load while displaying the processing icon.

Here's what the query would look like
```sql
select /* your columns */
  from /* your tables */
 where 1 = 1 
   and nvl(:P1_IS_LOADED, 'N') = 'Y'
```

If you also need to be able to download the report, you'll need to add another condition so that it can work:
```sql
select /* your columns */
  from /* your tables */
 where 1 = 1 
   and ( /* Standard Page Load */
         nvl(:P1_IS_LOADED, 'N') = 'Y'
         
         /* Report Download */
         or substr(:request, instr(:request, '_', -1) + 1) in ('CSV','XLS','PDF','RTF','HTMLD')
         
         /* Report Email */
         or wwv_flow.g_widget_action = 'SEND_EMAIL'
         )
```

For more information about the above condition, you can have a look [here]({% post_url 2018-08-20-include-or-exclude-columns-in %}){:target="_blank"}.

Here's what the end result looks like compared to the standard behaviour:

{% include images.html name="Lazy_Load_Report.gif" alt="Lazy Load Report" class="mx-auto" %}

You can have a look at my {% include demo.html label="Demo Application" page="3500" %}

Enjoy!