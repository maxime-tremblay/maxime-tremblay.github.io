---
layout: post
title: Include or Exclude Columns in an Interactive Report Export
tags: [Interactive Report, Export]
---

You might have noticed that for the Classic Reports and the Interactive Grids there's an option to include or exclude a column in the report's export.

{% include images.html name="include_in_export.png" alt="Export / Printing Section" class="mx-auto" width="320px" %}

Unfortunately, that option is not available for the Interactive Reports.

In order to export a report, APEX submits the page using a request that is then used to generate the corresponding file. This can be verified by having a look at the network tab in DevTools:
{% include images.html name="IR_request.png" alt="DevTools Requests" class="mx-auto" width="400px" %}

As we can see, a request is used to export the report, except for the Email option.

If we look at the request's details for the Email export:
{% include images.html name="IR_request_email.png" alt="Email Request" class="mx-auto" width="400px" %}

We can see that it's making an AJAX call and that it sets the <i>p_widget_action</i> to "SEND_EMAIL" which is saved in the wwv_flow package as g_widget_action.

Using the above, we can remove a column from the export by adding a server-side condition that checks the request and the widget action as follow:

```sql
nvl(:request, 'EMPTY') not in ('CSV','XLS','PDF','RTF','HTMLD')
and nvl(wwv_flow.g_widget_action, 'EMPTY') <> 'SEND_EMAIL'
```

That condition will work if there is only one interactive report on the page. If there is more than one report, the requests will be different.

As we can see here:
{% include images.html name="IR_request_2.png" alt="Multiple Reports Request" class="mx-auto" width="400px" %}

The requests are going to be using this pattern: `IR[R<region id>]_<export type>`

If we take that into consideration and include it into the previous condition, we will have this:

```sql
nvl(substr(:request, instr(:request, '_', -1) + 1), 'EMPTY') not in ('CSV','XLS','PDF','RTF','HTMLD')
and nvl(wwv_flow.g_widget_action, 'EMPTY') <> 'SEND_EMAIL'
```

In order to centralize the condition and avoid code being duplicated/replicated everywhere that we need to use this, it's best to create an authorization schema that we can use instead of using the server-side condition. 

Enjoy!