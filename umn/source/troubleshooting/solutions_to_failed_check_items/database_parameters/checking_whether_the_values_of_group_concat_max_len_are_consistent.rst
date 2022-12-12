:original_name: drs_11_0469.html

.. _drs_11_0469:

Checking Whether the Values of group_concat_max_len Are Consistent
==================================================================

MySQL Migration, Synchronization, and Disaster Recovery
-------------------------------------------------------

.. table:: **Table 1** group_concat_max_len consistency check

   +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | The **group_concat_max_len** value in the destination database is inconsistent with that in the source database.                                                                                 |
   +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | If the values of **group_concat_max_len** in the source and destination databases are different, the queried fields may be truncated. Change the parameter values to the same.                   |
   +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: If the values of group_concat_max_len in the source and destination databases are different, the queried fields may be truncated. Change the parameter values to the same. |
   |                                              |                                                                                                                                                                                                  |
   |                                              | Handling suggestion: Change the parameter values to the same.                                                                                                                                    |
   +----------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
