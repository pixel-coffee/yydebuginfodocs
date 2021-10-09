YYDebug Info
============

yydebug_get_script_code
^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: yydebug_get_script_code(script_name_or_id)

    Takes in the name or ID number of a GML script and returns its GML code. If the script is not found, this will return ``undefined``.
   
        * **Returns:** (*string* **or** *undefined*)
        
        * **Parameters:**
        
            * **script_name_or_id** (*string*, *method* **or** *integer*) -

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
                  
    **Examples**
    
    Using function ID/name:
    
    .. code-block:: javascript
        :linenos:
   
        // scr_move_player.gml
        function scr_move_player(x, y) {
            self.x = x;
            self.y = y;
        }
    
    .. code-block:: javascript
        :linenos:
        
        // Step event
        show_message(yydebug_get_script_code(scr_move_player));
        show_message(yydebug_get_script_code("scr_move_player"));
        show_message(yydebug_get_script_code(script_get_name(scr_move_player)));
        // The 3 lines above will print the contents of scr_move_player.gml
    
    Using method name:
    
    .. code-block:: javascript
        :linenos:
   
        // scr_move_player.gml
        global.scr_move_player = function(x, y) {
            self.x = x;
            self.y = y;
        }
    
    .. code-block:: javascript
        :linenos:
        
        // Step event
        show_message(yydebug_get_script_code(global.scr_move_player)); // Works
        show_message(yydebug_get_script_code(script_get_name(global.scr_move_player))); // Works
        show_message(yydebug_get_script_code("scr_move_player")); // Returns undefined

yydebug_get_script_line
^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: yydebug_get_script_line(script_name_or_id, line_number)

   Takes in a GML script name/ID number + a line number and returns the corresponding line of GML code. If the script is not found or the line number is out of range, this will return ``undefined``.
   
       * **Returns:** (*string* **or** *undefined*)
       
       * **Parameters:**
       
           * **script_name_or_id** (*string*, *method* **or** *integer*) -

               The name or ID number of the GML script asset, function, or method.
       
           * **line_number** (*number*) -

               The desired line number of the script.
                  
    **Examples**
    
    .. code-block:: javascript
        :linenos:
        
        // scr_move_player.gml
        function scr_move_player(x, y) {
            self.x = x;
            self.y = y;
        }
    
    .. code-block:: javascript
        :linenos:
        
        // Step event
        show_message(yydebug_get_script_line(scr_move_player, 3)); // Prints "    self.x = x;"
        
yydebug_get_script_lines
^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: yydebug_get_script_lines(script_name_or_id)

   Similar to ``yydebug_get_script_code``, this will take in the name or ID number of a GML script. But instead of returning its GML code as a single string, it will return its GML code as an array of lines. If the script is not found, this will return ``undefined``.
   
       * **Returns:** (*array* [ *string* ] **or** *undefined*)
       
       * **Parameters:**
       
           * **script_name_or_id** (*string*, *method* **or** *integer*) -

               The name or ID number of the GML script asset, function, or method.
                  
    **Examples**
    
    .. code-block:: javascript
        :linenos:
        
        // scr_move_player.gml
        function scr_move_player(x, y) {
            self.x = x;
            self.y = y;
        }
    
    .. code-block:: javascript
        :linenos:
        
        // Step event
        show_message(yydebug_get_script_lines(scr_move_player));
        // Result:
        // [
        //     "// scr_move_player.gml",
        //     "function scr_move_player(x, y) {",
        //     "    self.x = x;",
        //     "    self.y = y;",
        //     "}"
        // ]
        
yydebug_get_script_line_count
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. py:function:: yydebug_get_script_line_count(script_name_or_id)

   Takes in the name or ID number of a GML script and returns the line count of its GML code. If the script is not found, this will return ``undefined``.
   
       * **Returns:** (*integer number* **or** *undefined*)
       
       * **Parameters:**
       
           * **script_name_or_id** (*string*, *method* **or** *integer*) -

               The name or ID number of the GML script asset, function, or method.
                  
    **Examples**
    
    .. code-block:: javascript
        :linenos:
        
        // scr_move_player.gml
        function scr_move_player(x, y) {
            self.x = x;
            self.y = y;
        }
    
    .. code-block:: javascript
        :linenos:
        
        // Step event
        show_message(yydebug_get_script_line_count(scr_move_player)); // Prints 5
        
yydebug_callstack
^^^^^^^^^^^^^^^^^

.. py:function:: yydebug_callstack(depth=undefined, offset=0)

   Similar to the built-in ``debug_get_callstack()`` function, this will return a callstack to the user, but with the following improvements:
   
   1. In addition to the GML script name and line number, it will return the line string itself for each function in the callstack.
   
   2. The GML script name and line number are separated into different struct members.
   
   3. Unlike ``debug_get_callstack()``, there is no unneeded trailing ``0`` at the end of the array.
   
       * **Returns:** (*array* [ *struct* ])
       
           Struct properties:

               * **scriptName** (*string*)

                    The name of the GML script, function or method.

               * **lineNumber** (*integer number*)

                    The current line number of execution of the script on the callstack.

               * **lineInfo** (*string*)

                    The line of GML code that is present on the line number of execution.

            .. warning::
                This function relies on the built-in ``debug_get_callstack()`` function.
                As of writing this, Game Maker Studio has a bug where ``debug_get_callstack()`` will sometimes report a line number of ``-1``
                for anonymous methods. Because of this, the structs returned by ``yydebug_callstack`` for those methods will report
                having **lineNumber** == ``-1`` and **lineInfo** == ``undefined``. Until YYG fixes this bug, there is no way around this.

            .. note::
                The array is ordered such that the current script of execution appears at the beginning, with its callers toward the end.
                So if you have a method ``a`` which calls ``b`` which calls ``c``, the order of the array would be ``c`` ``b`` ``a``.
       
       * **Parameters:**
       
           * **depth** (*integer*) [Optional] -

               The maximum depth of the callstack (AKA which index to cut off the returned array at).
               If ``undefined`` or not supplied, the full callstack will be returned.
       
           * **offset** (*integer*) [Optional] -

                The starting offset of the returned callstack array. This is used if want to ignore the first few elements of the callstack array.
                So if you supply an offset of ``1``, for example, the first element of the returned array will be the *caller* of the current script of execution.
                If ``2``, it will return its caller's caller, and so on.

                ``0`` by default.
                  
    **Examples**
    
    .. code-block:: javascript
        :linenos:
        
        // Room1 creation code
        var player = instance_create_depth(0, 0, 0, obj_player);
        with (player) scr_move_player(100, 200);
        
    .. code-block:: javascript
        :linenos:
        
        // scr_move_player.gml
        function scr_move_player(x, y) {
            scr_move_player_x(x);
            scr_move_player_y(y);
        }
        function scr_move_player_x(x) {
            self.x = x;
            show_message(yydebug_callstack());
            // The above prints:
            // [
            //     {
            //         scriptName : "gml_Script_scr_move_player_x",
            //         lineNumber : 8,
            //         lineInfo : "    show_message(yydebug_callstack());"
            //     },
            //     {
            //         scriptName : "gml_Script_scr_move_player",
            //         lineNumber : 3,
            //         lineInfo : "    scr_move_player_x(x);"
            //     },
            //     {
            //         scriptName : "gml_Room_Room1_Create",
            //         lineNumber : 3,
            //         lineInfo : "with (player) scr_move_player(100, 200);"
            //     }
            // ]
            show_message(yydebug_callstack(2)); // Limit depth to 2
            // The above prints:
            // [
            //     {
            //         scriptName : "gml_Script_scr_move_player_x",
            //         lineNumber : 27,
            //         lineInfo : "    show_message(yydebug_callstack(2)); // Limit depth to 2"
            //     },
            //     {
            //         scriptName : "gml_Script_scr_move_player",
            //         lineNumber : 3,
            //         lineInfo : "    scr_move_player_x(x);"
            //     }
            // ]
        }
        function scr_move_player_y(y) {
            self.y = y;
            show_message(yydebug_callstack(undefined, 1)); // Max depth, offset of 1
            // The above prints:
            // [
            //     {
            //         scriptName : "gml_Script_scr_move_player",
            //         lineNumber : 3,
            //         lineInfo : "    scr_move_player_x(x);"
            //     },
            //     {
            //         scriptName : "gml_Room_Room1_Create",
            //         lineNumber : 3,
            //         lineInfo : "with (player) scr_move_player(100, 200);"
            //     }
            // ]
        }
