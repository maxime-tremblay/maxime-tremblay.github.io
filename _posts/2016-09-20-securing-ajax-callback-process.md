---
layout: post
title: Securing Ajax Callback Process
tags: [Security, Ajax, JavaScript]
thumbnail: https://2.bp.blogspot.com/-0LLh5Thhf6o/V-Ls04N_pII/AAAAAAAAAOk/crYvzKRDdyEq2tNMztz1cPovbJyOhtmIACLcB/s72-c/arguments-checksum.png
---

When navigating from a report page to the corresponding detail page, it's always a good practice to enable the parameters checksum to prevent users from tampering with the item values that are in the url.

To enable arguments checksum, you must first set the "Page Access Protection" attribute under the page attribute security section to "Arguments must have checksum" and then for each item that is going to be assigned from the url, you need to set the "Session State Protection" to one of the "Checksum Required" value (have a look at the item's help for more details about the different types of checksum).

![Arguments Checksum](https://2.bp.blogspot.com/-0LLh5Thhf6o/V-Ls04N_pII/AAAAAAAAAOk/crYvzKRDdyEq2tNMztz1cPovbJyOhtmIACLcB/s1600/arguments-checksum.png "Arguments Checksum"){:class="img-responsive"}

That way the user is not going to be able to change any value from the url.

I recently had to implement a similar concept using button in a report that were calling an AJAX Callback Process from a dynamic action.

Here's what my report's SQL Query looked like:
```sql
select '<button onclick="void(0);"'
           || ' data-data1="' || some_table_id || '"'
           || ' data-data2="' || some_value || '"'
           --|| ' data-data3="' || sys.dbms_crypto.hash(utl_raw.cast_to_raw(some_table_id || some_value || to_char(nvl(last_update_date, creation_date), :DATETIMEFORMAT)), 3) || '"' /* Where 3 -> SHA-1 from sys.dbms_crypto.hash_sh1 */
           || ' data-data3="' || apex_util.get_hash(apex_t_varchar2(some_table_id, some_value, to_char(nvl(last_update_date, creation_date), :DATETIMEFORMAT))) || '"'
           || ' class="t-Button t-Button--hot t-Button--small actionButton"'
           || ' type="button"><span class="t-Button-label">Some Action</span></button>'
       /* Rest of the query */
  from some_table
 where /* where clauses */
```

Where data1 and data2 are the values that are needed in the AJAX Callback Process and data3 is the checksum for the previous values.
To have a stronger checksum and to ensure that it is only used once, I added the record's last update date to it.
DATETIMEFORMAT is an application substitution string.

Note: in order to be able to use dbms_crypto, it needs to be granted to the current user (not required with the apex_util.get_hash function.
For more information on the Apex API, read this [GET_HASH](http://docs.oracle.com/cd/E59726_01/doc.50/e39149/apex_util.htm#AEAPI30207){:target="_blank"}.

The corresponding dynamic action to handle the button click was as follow:

**Dynamic Action:** Event: Click  
**jQuery Selector:** `.actionButton`
```javascript
var lSpinner$ = apex.util.showSpinner();
var lReportRegion$ = $(this.affectedElements);

apex.server.process("AJAX_PROCESS_NAME",
                    {x01: $(this.triggeringElement).data('data1'),
                     x02: $(this.triggeringElement).data('data2'),
                     x03: $(this.triggeringElement).data('data3')
                     },
                    {success: function( pData ) {
                        if (pData.success === true){
                            /* Show Sucess Message */
                            showSuccessMessage(pData.message);
                            
                            /* Refresh Region */
                            lReportRegion$.trigger('apexrefresh');
                        }
                        else{
                            /* Show Error Message */
                            showErrorMessage([pData.message]);
                        }
                        
                        lSpinner$.remove();
                      }
                     }
                    );
```

In the previous code, I'm using the affected element attribute to refresh my report region.

Here's the AJAX Callback Process:
```sql
declare
    l_some_table_id number;
    l_some_value    varchar2(50);
    l_checksum      varchar2(32767);
    --l_checksum      raw(32767); --sys.dbms_crypto.hash returns raw
    --l_hash_type     pls_integer := sys.dbms_crypto.hash_sh1;
    
    l_last_update   varchar2(100);
begin
    /* Retrieve parameters */
    l_some_table_id := to_number(apex_application.g_x01);
    l_some_value    := apex_application.g_x02;
    l_checksum      := apex_application.g_x03;
    
    select to_char(nvl(last_update_date, creation_date), :DATETIMEFORMAT)
      into l_last_update
      from some_table
     where some_table_id = l_some_table_id;
    
    /* Validate the checksum */
    --if l_checksum = sys.dbms_crypto.hash(utl_raw.cast_to_raw(l_some_table_id || l_some_value || l_last_update), l_hash_type) then
    if l_checksum = apex_util.get_hash(apex_t_varchar2(l_some_table_id, l_some_value, l_last_update)) then
        /* Do something */
        
        apex_json.open_object;
        apex_json.write('success', true);
        apex_json.write('message', 'Action Processed.');
        apex_json.close_object;
    else
        apex_json.open_object;
        apex_json.write('success', false);
        apex_json.write('message', 'Invalid Action.');
        apex_json.close_object;
    end if;
exception
    when no_data_found then
        apex_json.open_object;
        apex_json.write('success', false);
        apex_json.write('message', 'Invalid Action.');
        apex_json.close_object;
    when others then
        apex_json.open_object;
        apex_json.write('success', false);
        apex_json.write('message', 'Invalid Action.');
        apex_json.close_object;
end;
```

Basically what we do in the process is to recreate a checksum based on the parameters' values and to compare it with the checksum parameter and if they match we execute the code that needs to run. 

> **Note:** Edited above code to use the Apex API: apex_util.get_hash. Commented out everything related to dbms_crypto for reference purpose.