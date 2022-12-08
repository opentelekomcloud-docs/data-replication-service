:original_name: drs_11_0005.html

.. _drs_11_0005:

Checking Whether the Source Database Version Is Supported
=========================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database version is supported

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database version is supported                                                                                                                                               |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the source database version is MySQL 5.5.x, MySQL 5.6.x, MySQL 8.0.x, and MySQL 5.7.x.                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database version is not supported.                                                                                                                                   |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Export data and then import it following the instructions provided in the "Migrating MySQL Data Using mysqldump" section in the *Relational Database Service User Guide*. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                                                                   |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.                                                                                              |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the source database fails to be connected.                                                                                                  |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Migration from MongoDB to DDS
-----------------------------

.. table:: **Table 2** Checking whether the source database version is supported

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database version is supported                                                                          |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the source database version is MongoDB 3.2.x, 3.4.x, or 4.0.x.                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database version is not supported.                                                              |
   |                                       |                                                                                                                           |
   |                                       | Handling suggestion: Check whether the source database version is MongoDB 3.2x, 3.4.x, and 4.0.x.                         |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the source database fails to be connected.                             |
   |                                       |                                                                                                                           |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                      |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The incremental data is obtained in changeStream mode but the source database version is earlier than 4.0. |
   |                                       |                                                                                                                           |
   |                                       | Handling suggestion: In changeStream mode, ensure that the source database version is 4.0 or later.                       |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                  |
   |                                       |                                                                                                                           |
   |                                       | Handling suggestion: Contact technical support.                                                                           |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------+
