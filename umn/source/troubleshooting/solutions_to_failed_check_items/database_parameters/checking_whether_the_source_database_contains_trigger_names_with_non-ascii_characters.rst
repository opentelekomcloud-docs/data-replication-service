:original_name: drs_11_0073.html

.. _drs_11_0073:

Checking Whether the Source Database Contains Trigger Names with Non-ASCII Characters
=====================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains trigger names with non-ASCII characters

   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database contains trigger names with non-ASCII characters                                                                                          |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | If the source database contains non-ASCII characters, the migration will fail.                                                                                        |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The source database cannot contain view names with non-ASCII characters.                                                                        |
   |                                              |                                                                                                                                                                       |
   |                                              | Handling suggestion: To solve this problem, perform the following steps:                                                                                              |
   |                                              |                                                                                                                                                                       |
   |                                              | Method 1:                                                                                                                                                             |
   |                                              |                                                                                                                                                                       |
   |                                              | Click **Previous** to return to the **Select Migration Type** page. Select a customized object and do not select the trigger name that contains non-ASCII characters. |
   |                                              |                                                                                                                                                                       |
   |                                              | Method 2: Change the trigger name.                                                                                                                                    |
   +----------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
