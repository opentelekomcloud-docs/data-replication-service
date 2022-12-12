:original_name: drs_11_0024.html

.. _drs_11_0024:

Checking Whether the COLLATION_SERVER Values of the Source and Destination Databases Are the Same
=================================================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the COLLATION_SERVER values of the source and destination databases are the same

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the **COLLATION_SERVER** values of the source and destination databases are the same                       |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Description                           | The migration fails because the **COLLATION_SERVER** values of the source and destination databases are different. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The **COLLATION_SERVER** values of the source and destination databases must be the same.           |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Change **COLLATION_SERVER** of the source and destination databases to the same value.        |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
