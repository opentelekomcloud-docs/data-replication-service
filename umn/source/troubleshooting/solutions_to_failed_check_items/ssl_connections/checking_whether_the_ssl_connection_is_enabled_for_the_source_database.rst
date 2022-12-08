:original_name: drs_11_0042.html

.. _drs_11_0042:

Checking Whether the SSL Connection Is Enabled for the Source Database
======================================================================

PostgreSQL
----------

.. table:: **Table 1** Checking whether the SSL connection is enabled for the source database

   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the SSL connection is enabled for the source database                                                                                                                                                                                     |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the SSL connection is enabled for the source database.                                                                                                                                                                              |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The source database SSL connection is disabled.                                                                                                                                                                                    |
   |                                       |                                                                                                                                                                                                                                                   |
   |                                       | Handling suggestion: In the **postgresql.conf** file, set **ssl_ca_file** to the directory of an SSL root CA certificate and set **ssl** to **on** to enable the SSL connection. Then, restart the database for the modifications to take effect. |
   +---------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
