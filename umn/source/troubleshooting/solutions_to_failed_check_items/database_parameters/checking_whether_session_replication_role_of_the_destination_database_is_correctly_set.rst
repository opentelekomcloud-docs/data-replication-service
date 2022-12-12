:original_name: drs_03_1130.html

.. _drs_03_1130:

Checking Whether session_replication_role of the Destination Database Is correctly Set
======================================================================================

PostgreSQL Synchronization
--------------------------

.. table:: **Table 1** Checking whether the session_replication_role value of the destination database is correctly set

   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                                   | Whether the **session_replication_role** value of the destination database is correctly set.                                                                                                                                                                                                                                          |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                                  | The **session_replication_role** parameter of the destination database is not set to **replica**. Data synchronization may fail when the synchronized table has associated foreign key constraints or triggers.                                                                                                                       |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Item to Be Confirmed and Handling Suggestion | Item to be confirmed: The **session_replication_role** parameter of the destination database is not set to **replica**.                                                                                                                                                                                                               |
   |                                              |                                                                                                                                                                                                                                                                                                                                       |
   |                                              | Handling suggestion: Before starting the synchronization task, set **session_replication_role** of the destination database to **replica**. After the synchronization is complete, change the value of this parameter to **origin**. If the destination database is an RDS instance, you can modify the parameter on the RDS console. |
   +----------------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
