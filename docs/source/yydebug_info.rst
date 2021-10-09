YYDebug Info
============

.. py:function:: yydebug_get_script_code(script_name_or_id)

   Takes in the name or ID number of a GML script and returns its GML code.
   
       * **Returns:** *string*
       
       * **Parameters:**
       
           * **script_name_or_id** (*string*, *number*) -

               The name or ID number of the GML script asset, function, or method.

               .. note::
                  When using script names, you can use either the name of the script asset/function directly,
                  or use the formatting provided by the ``debug_get_callstack`` built-in function.

               .. note::
                  The idea of passing in the name of a method may seem confusing, since they (unlike functions/scripts)
                  do not have a canonical name tied to a specific asset. However, you can still obtain the name of any
                  method stored in a variable. Simply call ``script_get_name(method_variable)``
                  (You will get something like ``"anon_2D37DFFB_819"``) and pass the returned value into this function .
                  This function will give you the GML code associated with the method's parent GML script.
                  
