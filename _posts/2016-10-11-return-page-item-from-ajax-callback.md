---
layout: post
title: Return Page Item From an AJAX Callback Process
tags: [Ajax, JavaScript]
---

Recently, I was working on a form that had multiple items retrieved when a select list item changed. The select list triggered a dynamic action that executed some PL/SQL code and returned item values.

It was looking like that:
{% include images.html name="da-plsql.png" alt="DA PL/SQL" class="center-block" width="450px" %}

At some point, the process became "too big" for the "Execute PL/SQL Code" action (it can only hold up to 4000 characters).

So, I decided to move everything to a page "AJAX Callback" process which can hold up to 32767 characters.

So I replaced the dynamic action "Execute PL/SQL Code" action with an "Execute JavaScript" action as follow:
```javascript
/* Show a processing image */
var lSpinner$ = apex.util.showSpinner();

apex.server.process("SOME_PROCESS",
                    {pageItems: "#P2300_LOV"
                     },
                    {success: function(pData) {
                        /* If the AJAX is successful set the value or the returned items */
                        if (pData.success === true){
                            /* Loop through the array and set the value of each item */
                            for (var i=0; i &lt; pData.items.length; i++){
                                apex.item(pData.items[i].id).setValue(pData.items[i].value);
                            }
                        }
                        
                        /* Remove the processing image */
                        lSpinner$.remove();
                      },
                     error: function(request, status, error) {
                        alert(request.responseText);
                         
                        /* Remove the processing image */
                        lSpinner$.remove();
                      }
                     }
                    );
````

And I created the AJAX Callback as follow:
```sql
declare
    /* Local variables */

    /* Utility function to output item's id and value */
    procedure output_json_item(p_item_name  in varchar2,
                               p_item_value in varchar2
                               )
    as
    begin
        apex_json.open_object;
        apex_json.write('id', p_item_name);
        apex_json.write('value', p_item_value, true); /* true so that null values are written as well */
        apex_json.close_object;
    end output_json_item;
begin
    /* ********************** *
     * PL/SQL Process Content *
     * ********************** */
    if :P2300_LOV = '1' then
        :P2300_ITEM1 := 1;
        :P2300_ITEM2 := 1;
        :P2300_ITEM3 := 1;
        :P2300_ITEM4 := 1;
    elsif :P2300_LOV = '2' then
        :P2300_ITEM1 := 2;
        :P2300_ITEM2 := 2;
        :P2300_ITEM3 := 2;
        :P2300_ITEM4 := 2;
    elsif :P2300_LOV = '3' then
        :P2300_ITEM1 := 3;
        :P2300_ITEM2 := 3;
        :P2300_ITEM3 := 3;
        :P2300_ITEM4 := 3;
    end if;
        
    apex_json.open_object;
    apex_json.write('success', true);
    
    apex_json.open_array('items');

    /* Call the utility procedure for every item you want to return */
    output_json_item('P2300_ITEM1', :P2300_ITEM1);
    output_json_item('P2300_ITEM2', :P2300_ITEM2);
    output_json_item('P2300_ITEM3', :P2300_ITEM3);
    output_json_item('P2300_ITEM4', :P2300_ITEM4);
    
    apex_json.close_array;
    
    apex_json.close_object;
exception
    when others then
        apex_json.open_object;
        apex_json.write('success', false);
        apex_json.write('message', sqlerrm);
        apex_json.close_object;
end;
```

The idea here is to have PL/SQL AJAX Callback execute and if it successfully completes, it will be returning the list of items along with their values as JSON on which we are going to loop through and set the items' value using the JavaScript item API.

You can have a look at my {% include demo.html label="Demo Application" page="2300" %}