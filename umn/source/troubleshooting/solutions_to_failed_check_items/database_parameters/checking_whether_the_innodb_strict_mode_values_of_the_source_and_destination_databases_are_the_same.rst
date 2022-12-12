:original_name: drs_11_0060.html

.. _drs_11_0060:

Checking Whether the innodb_strict_mode Values of the Source and Destination Databases Are the Same
===================================================================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the innodb_strict_mode values of the source and destination databases are the same

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **innodb_strict_mode** values of the source and destination databases are the same                                                                                                                                                                 |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the **innodb_strict_mode** values of source and destination databases are the same. If they are inconsistent, the migration may fail.                                                                                                            |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | -  If you are migrating data to the cloud, perform the following operations:                                                                                                                                                                                   |
   |                                       |                                                                                                                                                                                                                                                                |
   |                                       |    Failure cause: The **innodb_strict_mode** values of the source and destination databases must be the same.                                                                                                                                                  |
   |                                       |                                                                                                                                                                                                                                                                |
   |                                       |    Handling suggestion: Create a parameter group for the destination database and change **innodb_strict_mode** to the same value as that of the source database. For details, see **Creating a Parameter Group** in *Relational Database Service User Guide*. |
   |                                       |                                                                                                                                                                                                                                                                |
   |                                       | -  If you are migrating data out of the cloud, perform the following operations:                                                                                                                                                                               |
   |                                       |                                                                                                                                                                                                                                                                |
   |                                       |    Failure cause: The **innodb_strict_mode** values of the source and destination databases must be the same.                                                                                                                                                  |
   |                                       |                                                                                                                                                                                                                                                                |
   |                                       |    Handling suggestion: Change **innodb_strict_mode** of the destination database to the same value as that of the source database.                                                                                                                            |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
