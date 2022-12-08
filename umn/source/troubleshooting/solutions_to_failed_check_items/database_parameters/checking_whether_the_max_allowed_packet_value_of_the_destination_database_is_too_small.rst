:original_name: drs_15_0017.html

.. _drs_15_0017:

Checking Whether the max_allowed_packet Value of the Destination Database Is too Small
======================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the max_allowed_packet value of the destination database is too small

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the max_allowed_packet value of the destination database is too small                                                                                                                  |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | A large amount of data cannot be written to the destination database during the migration because the max_allowed_packet value is smaller than 100 MB. As a result, the full migration failed. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **max_allowed_packet** value of the destination database is too small, which may cause data fails to be written during the migration.                                       |
   |                                       |                                                                                                                                                                                                |
   |                                       | Handling suggestions: Set the **max_allowed_packet** value greater than 100 MB                                                                                                                 |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
