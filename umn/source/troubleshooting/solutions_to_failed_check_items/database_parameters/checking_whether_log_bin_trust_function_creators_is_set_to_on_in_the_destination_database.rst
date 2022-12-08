:original_name: drs_11_0225.html

.. _drs_11_0225:

Checking Whether log_bin_trust_function_creators Is Set to On in the Destination Database
=========================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether log_bin_trust_function_creators is set to on in the destination database

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether **log_bin_trust_function_creators** is set to **on** in the destination database                                                                                                                                                                              |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | During the migration from RDS for MySQL to MySQL out of the cloud, the destination database does not support custom functions.                                                                                                                                        |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The destination database does not support custom functions.                                                                                                                                                                                            |
   |                                       |                                                                                                                                                                                                                                                                       |
   |                                       | Handling suggestions: In the **my.cnf** file of the destination database, check whether **log_bin_trust_function_creators=on** exists. If it does not exist, add **log_bin_trust_function_creators=on** and restart the database for the modification to take effect. |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
