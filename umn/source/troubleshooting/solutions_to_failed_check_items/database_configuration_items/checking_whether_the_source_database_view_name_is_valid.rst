:original_name: drs_11_0072.html

.. _drs_11_0072:

Checking Whether the Source Database View Name Is Valid
=======================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains view names with non-ASCII characters

   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the source database contains view names with non-ASCII characters                                                                                            |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | If the source database contains non-ASCII characters, the migration will fail.                                                                                       |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Failure cause: The source database view names contain unsupported characters, non-ASCII characters, or the following characters: ></\\                               |
   |                                              |                                                                                                                                                                      |
   |                                              | Handling suggestion: To solve this problem, perform the following steps:                                                                                             |
   |                                              |                                                                                                                                                                      |
   |                                              | Method 1:                                                                                                                                                            |
   |                                              |                                                                                                                                                                      |
   |                                              | Click **Previous** to return to the **Select Migration Type** page. Select a customized object and do not select the view name that contains unsupported characters. |
   |                                              |                                                                                                                                                                      |
   |                                              | Method 2: Change the view name.                                                                                                                                      |
   +----------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
