:original_name: drs_11_0228.html

.. _drs_11_0228:

Checking Whether the sql_mode Value in the Destination Database Is Not NO_ENGINE_SUBSTITUTION
=============================================================================================

MySQL Migration and Synchronization
-----------------------------------

.. table:: **Table 1** Checking whether the sql_mode value in the destination database is not NO_ENGINE_SUBSTITUTION

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the sql_mode value in the destination database is not NO_ENGINE_SUBSTITUTION                                                                                                                      |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | MyISAM tables are included in the migration objects. The sql_mode value in the destination database cannot be NO_ENGINE_SUBSTITUTION.                                                                     |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **sql_mode** value in the destination database is **NO_ENGINE_SUBSTITUTION**.                                                                                                          |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: In the destination database, set **SQL_MODE** to a value other than NO_ENGINE_SUBSTITUTION. For details, see "Modifying Parameters" in the *Relational Database Service User Guide*. |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
