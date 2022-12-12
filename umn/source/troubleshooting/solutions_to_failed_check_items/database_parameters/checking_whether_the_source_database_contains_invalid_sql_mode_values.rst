:original_name: drs_11_0049.html

.. _drs_11_0049:

Checking Whether the Source Database Contains Invalid sql_mode Values
=====================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the source database contains invalid sql_mode values

   +---------------------------------------+----------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database contains invalid **sql_mode** values                                   |
   +---------------------------------------+----------------------------------------------------------------------------------------------------+
   | Description                           | If the source database contains invalid **sql_mode** values, the migration will fail.              |
   +---------------------------------------+----------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **sql_mode** value of the source database cannot be **no_engine_substitution**. |
   |                                       |                                                                                                    |
   |                                       | Handling suggestion: Change **sql_mode** of the source database to a proper value.                 |
   +---------------------------------------+----------------------------------------------------------------------------------------------------+
