:original_name: drs_11_0002.html

.. _drs_11_0002:

Checking Whether the Destination Database Is Connected
======================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the destination database is connected

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database is connected                                                                           |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the destination database. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The connection fails.                                                                                    |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in section Real-Time Migration.              |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Incorrect username or password                                                                           |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Check whether the input username and password for the connection test are correct.                 |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database account does not allow remote connections.                                                  |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion:                                                                                                    |
   |                                       |                                                                                                                         |
   |                                       | Run the following command to create a user that allows remote connections. After the migration, delete this user.       |
   |                                       |                                                                                                                         |
   |                                       | .. code:: text                                                                                                          |
   |                                       |                                                                                                                         |
   |                                       |    CREATE USER 'Account' @ '%' IDENTIFIED BY 'Password'                                                                 |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database is unavailable.                                                                             |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Contact technical support.                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+

PostgreSQL Synchronization
--------------------------

.. table:: **Table 2** Checking whether the destination database is connected

   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database is connected                                                                                                                                                        |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the destination database.                                                                              |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The IP address is inaccessible.                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in section Real-Time Migration.                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The connection fails.                                                                                                                                                                 |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in section Real-Time Migration.                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database account does not allow remote connections.                                                                                                                               |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion:                                                                                                                                                                                 |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Grant the remote connection permission for the user in the **pg_hba.conf** file because the replication instance and user are not configured in the **pg_hba.conf** configuration file.              |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Add the following to the **pg_hba.conf** configuration file. After the migration is complete, delete this record and restart the database for the modification to take effect.                       |
   |                                       |                                                                                                                                                                                                      |
   |                                       | .. code:: text                                                                                                                                                                                       |
   |                                       |                                                                                                                                                                                                      |
   |                                       |    host all xxx(dbuser) 0.0.0.0/0 password                                                                                                                                                           |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Failed to connect to the database. The failure may be caused by the incorrect **listen_addresses** parameter value or port number in **postgres.conf**.                               |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion: In the **postgres.conf** file, set **listen_addresses** to "``*``" or set the port number to the correct value. Then, restart the database for the modification to take effect. |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Incorrect username or password                                                                                                                                                        |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion: Check whether the input username and password for the connection test are correct.                                                                                              |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The user does not have the login permission.                                                                                                                                          |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion:                                                                                                                                                                                 |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Run the following command to grant the login permission to the user:                                                                                                                                 |
   |                                       |                                                                                                                                                                                                      |
   |                                       | **alter role** *xxx(dbuser)* **login**                                                                                                                                                               |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The postgres database does not exist in the source database.                                                                                                                          |
   |                                       |                                                                                                                                                                                                      |
   |                                       | Handling suggestion: Create a postgres database.                                                                                                                                                     |
   +---------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

MongoDB Migration
-----------------

.. table:: **Table 3** Checking whether the destination database is connected

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the destination database is connected                                                                           |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the destination database. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The connection fails.                                                                                    |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in section Real-Time Migration.              |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Incorrect username or password                                                                           |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Check whether the input username and password for the connection test are correct.                 |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database is unavailable.                                                                             |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Contact technical support.                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Contact technical support.                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: SSL connection parameters are not configured.                                                            |
   |                                       |                                                                                                                         |
   |                                       | Handling suggestion: Contact technical support.                                                                         |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------+
