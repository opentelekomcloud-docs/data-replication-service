:original_name: drs_11_0014.html

.. _drs_11_0014:

Checking Whether the Source Database Binlog Is Enabled
======================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database binlog is enabled

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database binlog is enabled                                                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether binlog is enabled for the source database.                                                                                              |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: This item cannot be checked because the source database fails to be connected.                                                         |
   |                                       |                                                                                                                                                       |
   |                                       | Handling suggestion: Check whether the source database is connected.                                                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Insufficient user permissions                                                                                                          |
   |                                       |                                                                                                                                                       |
   |                                       | Handling suggestion: Check whether the database user permissions meet the migration requirements.                                                     |
   |                                       |                                                                                                                                                       |
   |                                       | .. note::                                                                                                                                             |
   |                                       |                                                                                                                                                       |
   |                                       |    For details about the required MySQL permissions and authorized operations, see :ref:`Which MySQL Permissions Are Required for DRS? <drs_04_0034>` |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                              |
   |                                       |                                                                                                                                                       |
   |                                       | Handling suggestion: Contact technical support.                                                                                                       |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The binlog function is disabled on the source database.                                                                                |
   |                                       |                                                                                                                                                       |
   |                                       | Handling suggestion:                                                                                                                                  |
   |                                       |                                                                                                                                                       |
   |                                       | -  If the source is an on-premises database, perform the following operations to enable binlog.                                                       |
   |                                       |                                                                                                                                                       |
   |                                       |    #. Run the following command to check whether binlog is enabled:                                                                                   |
   |                                       |                                                                                                                                                       |
   |                                       |       .. code:: text                                                                                                                                  |
   |                                       |                                                                                                                                                       |
   |                                       |          show variables like "log_bin"\G;                                                                                                             |
   |                                       |                                                                                                                                                       |
   |                                       |       |image1|                                                                                                                                        |
   |                                       |                                                                                                                                                       |
   |                                       |    #. If binlog is disabled, add **log-bin = mysql-bin** followed by **[mysqld]** in the MySQL configuration file **my.cnf** or **my.ini**.           |
   |                                       |                                                                                                                                                       |
   |                                       |       |image2|                                                                                                                                        |
   |                                       |                                                                                                                                                       |
   |                                       |    #. Restart the database.                                                                                                                           |
   |                                       |                                                                                                                                                       |
   |                                       |       |image3|                                                                                                                                        |
   |                                       |                                                                                                                                                       |
   |                                       | -  If the source is an RDS instance, enable binlog by referring to the RDS official documentation.                                                    |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. |image1| image:: /_static/images/en-us_image_0000001341254208.png
.. |image2| image:: /_static/images/en-us_image_0000001391534441.png
.. |image3| image:: /_static/images/en-us_image_0000001391773989.jpg
