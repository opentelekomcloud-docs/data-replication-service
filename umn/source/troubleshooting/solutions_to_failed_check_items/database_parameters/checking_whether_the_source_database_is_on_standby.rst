:original_name: drs_11_0056.html

.. _drs_11_0056:

Checking Whether the Source Database Is on Standby
==================================================

PostgreSQL Synchronization
--------------------------

.. table:: **Table 1** Checking whether the source database is on standby

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database is on standby                                                                                                                                                                                     |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | For a full+incremental synchronization task, the source database cannot be a standby database. Otherwise, incremental synchronization cannot be performed.                                                                    |
   |                                       |                                                                                                                                                                                                                               |
   |                                       | For a full synchronization task, the source database can be a standby database, but **hot_standby_feedback** must be set to **on**. Otherwise, the synchronization may fail.                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: In a real-time full+incremental synchronization task, the source database cannot be a standby database. Otherwise, incremental synchronization cannot be performed.                                            |
   |                                       |                                                                                                                                                                                                                               |
   |                                       | Handling suggestion: Configure the source database as the primary database.                                                                                                                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: For a full synchronization task, the source database **hot_standby_feedback** is set to **off**.                                                                                                               |
   |                                       |                                                                                                                                                                                                                               |
   |                                       | Handling suggestion: The source database is configured as the primary database, or **hot_standby_feedback** of the source database is set to **on**.                                                                          |
   |                                       |                                                                                                                                                                                                                               |
   |                                       | -  Change the source database to the primary database.                                                                                                                                                                        |
   |                                       | -  Alternatively, change the **hot_standby_feedback** value of the source database to **on** before starting full synchronization. After the full synchronization is complete, change the value of this parameter to **off**. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                                                      |
   |                                       |                                                                                                                                                                                                                               |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                                               |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
