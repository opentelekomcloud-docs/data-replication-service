:original_name: drs_11_0006.html

.. _drs_11_0006:

Checking Whether the Destination Database Version Is Supported
==============================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the destination database version is supported

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database version is supported                                                                                                                                          |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database version is MySQL 5.6.x, or MySQL 5.7.x.                                                                                                                 |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination database version is not supported.                                                                                                                              |
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
   |                                       | Failure cause: This item cannot be checked because the destination database fails to be connected.                                                                                             |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestion: Check whether the destination database is connected.                                                                                                                      |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

MongoDB to DDS Migration
------------------------

.. table:: **Table 2** Checking whether the destination database version is supported

   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database version is supported                                                  |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the destination database version is MongoDB 3.4.x, 4.0.x, or 4.2.x.                      |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination database version is not supported.                                      |
   |                                       |                                                                                                        |
   |                                       | Handling suggestion: Check whether the destination database version is MongoDB 3.4.x, 4.0.x, or 4.2.x. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: This item cannot be checked because the destination database fails to be connected.     |
   |                                       |                                                                                                        |
   |                                       | Handling suggestion: Check whether the destination database is connected.                              |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                               |
   |                                       |                                                                                                        |
   |                                       | Handling suggestion: Contact technical support.                                                        |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------+
