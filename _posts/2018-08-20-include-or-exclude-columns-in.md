---
layout: post
title: Include or Exclude Columns in an Interactive Report Export
thumbnail: https://3.bp.blogspot.com/-0NcDGlcjJN8/W3dyJcUMwJI/AAAAAAAACNo/czwSOF88RzoIabx5kCJ6jyp_zcJci19xgCLcBGAs/s72-c/IR_download.png
---

You might have noticed that for the Classic Reports and the Interactive Grids there's an option to include or exclude a column in the report's export.

![Export / Printing Section](https://1.bp.blogspot.com/--dC18rR57p0/W3cj0STJD8I/AAAAAAAACNE/KuVoEclTvP0e6aZoSJpgb6yiS0H4x_zcACLcBGAs/s1600/include_in_export.png "Export / Printing Section"){:width="320px" class="img-responsive center-block"}

Unfortunately, that option is not available for the Interactive Reports.

In order to export a report, APEX submits the page using a request that is then used to generate the corresponding file. This can be verified by having a look at the network tab in DevTools:
![DevTools Requests](https://1.bp.blogspot.com/-bTb13qAgnS4/W3dqbC4r7zI/AAAAAAAACNU/p_6Dqs86YAIT2KQX1CNQupSb8qMj0c3lgCLcBGAs/s1600/IR_request.png "DevTools Requests"){:width="400px" class="img-responsive center-block"}

As we can see, a request is used to export the report, except for the Email option.

If we look at the request's details for the Email export:
![Email Request](https://3.bp.blogspot.com/-p7fzu17wGEo/W3dqbID0N-I/AAAAAAAACNQ/LuRMDeHuEwwzzQK3eWrpQ_bs7Dec6Nw9QCLcBGAs/s1600/IR_request_email.png "Email Request"){:width="400px" class="img-responsive center-block"}

We can see that it's making an AJAX call and that it sets the <i>p_widget_action</i> to "SEND_EMAIL" which is saved in the wwv_flow package as g_widget_action.

Using the above, we can remove a column from the export by adding a server-side condition that checks the request and the widget action as follow:

```sql
nvl(:request, 'EMPTY') not in ('CSV','XLS','PDF','RTF','HTMLD')
and nvl(wwv_flow.g_widget_action, 'EMPTY') <> 'SEND_EMAIL'
```

That condition will work if there is only one interactive report on the page. If there is more than one report, the requests will be different.

As we can see here:
![Multiple Reports Request](https://4.bp.blogspot.com/-U_8MwCFUv1s/W3dyqiPWzRI/AAAAAAAACNw/12z8P_KHGtQ8ywA1WurWK-urBNCaj-TRgCLcBGAs/s1600/IR_request_2.png "Multiple Reports Request"){:width="400px" class="img-responsive center-block"}

The requests are going to be using this pattern: `IR[R<region id>]_<export type>`

If we take that into consideration and include it into the previous condition, we will have this:

```sql
nvl(substr(:request, instr(:request, '_', -1) + 1), 'EMPTY') not in ('CSV','XLS','PDF','RTF','HTMLD')
and nvl(wwv_flow.g_widget_action, 'EMPTY') <> 'SEND_EMAIL'
```

In order to centralize the condition and avoid code being duplicated/replicated everywhere that we need to use this, it's best to create an authorization schema that we can use instead of using the server-side condition. 

Enjoy!