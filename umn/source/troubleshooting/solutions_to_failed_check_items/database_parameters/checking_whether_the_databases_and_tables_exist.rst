:original_name: drs_03_045.html

.. _drs_03_045:

Checking Whether the Databases and Tables Exist
===============================================

All Scenarios
-------------

.. table:: **Table 1** Checking whether the databases and tables exist

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the databases and tables exist                                                                                   |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | Description                           | There are databases and tables in the uploaded file that do not exist in the source database. The synchronization fails. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: Objects imported from files do not exist in the source database.                                          |
   |                                       |                                                                                                                          |
   |                                       | Handling suggestion: Remove these objects that do not exist and import the file again.                                   |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------+
