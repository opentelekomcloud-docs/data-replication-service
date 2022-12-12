:original_name: drs_11_0107.html

.. _drs_11_0107:

Checking Whether the SSL Certificate of the Destination Database Exists
=======================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the SSL certificate of the destination database exists

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the SSL certificate of the destination database exists                                                                                                                                                                                                          |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the SSL certificate type of the destination database is correct during migration. Otherwise, the migration fails.                                                                                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The SSL certificate of the destination database does not exist.                                                                                                                                                                                          |
   |                                       |                                                                                                                                                                                                                                                                         |
   |                                       | Handing suggestion: On the **Configure Source and Destination Databases** page, enable SSL connection for the destination database and upload an encryption certificate that contains only one beginning tag **BEGIN CERTIFICATE** and one end tag **END CERTIFICATE**. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The SSL certificate type of the destination database is not supported.                                                                                                                                                                                   |
   |                                       |                                                                                                                                                                                                                                                                         |
   |                                       | Handing suggestion: On the **Configure Source and Destination Databases** page, enable SSL connection for the destination database and upload an encryption certificate that contains only one beginning tag **BEGIN CERTIFICATE** and one end tag **END CERTIFICATE**. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
