:original_name: drs_precheck.html

.. _drs_precheck:

Checking Whether the Source Database Is Connected
=================================================

MySQL Migration
---------------

.. table:: **Table 1** Checking whether the source database is connected

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database is connected                                                                           |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the source database. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The connection fails.                                                                               |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in Real-Time Migration.                 |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Incorrect username or password                                                                      |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Check whether the input username and password for the connection test are correct.            |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database account does not allow remote connections.                                             |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion:                                                                                               |
   |                                       |                                                                                                                    |
   |                                       | Run the following command to create a user that allows remote connections. After the migration, delete this user.  |
   |                                       |                                                                                                                    |
   |                                       | .. code:: text                                                                                                     |
   |                                       |                                                                                                                    |
   |                                       |    CREATE USER 'Account' @ '%' IDENTIFIED BY 'Password'                                                            |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The SSL CA root certificate is invalid.                                                             |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Upload a valid SSL CA certificate.                                                            |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: No SSL CA root certificate exists.                                                                  |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Contact technical support.                                                                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database is unavailable.                                                                        |
   |                                       |                                                                                                                    |
   |                                       | Handling suggestion: Contact technical support.                                                                    |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------+

PostgreSQL Synchronization
--------------------------

.. table:: **Table 2** Checking whether the source database is connected

   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database is connected                                                                                                                                                  |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the source database.                                                                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The IP address is inaccessible.                                                                                                                                            |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in Real-Time Migration.                                                                                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The connection fails.                                                                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in Real-Time Migration.                                                                                        |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database account does not allow remote connections.                                                                                                                    |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion:                                                                                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | Configure the remote connection permission for the user in the **pg_hba.conf** file.                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | Open **pg_hba.conf**, add the following, and restart the database for the modification to take effect:                                                                                    |
   |                                       |                                                                                                                                                                                           |
   |                                       | .. code:: text                                                                                                                                                                            |
   |                                       |                                                                                                                                                                                           |
   |                                       |    host all xxx(dbuser) 0.0.0.0/0 password                                                                                                                                                |
   |                                       |                                                                                                                                                                                           |
   |                                       | After the migration is complete, delete this record and restart the database again.                                                                                                       |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Failed to connect to the database.                                                                                                                                         |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion:                                                                                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | The **listen_addresses** parameter value or port number in the **postgres.conf** file is incorrect.                                                                                       |
   |                                       |                                                                                                                                                                                           |
   |                                       | In the **postgres.conf** file, set the **listen_addresses** value to **'*'** or set the port number to the correct value. Then, restart the database for the modification to take effect. |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: Incorrect username or password                                                                                                                                             |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion: Check whether the input username and password for the connection test are correct.                                                                                   |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The user does not have the login permission.                                                                                                                               |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion:                                                                                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | Run the following command to grant the login permission to the user:                                                                                                                      |
   |                                       |                                                                                                                                                                                           |
   |                                       | **alter role** *xxx(dbuser)* **login**                                                                                                                                                    |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The postgres database does not exist in the source database.                                                                                                               |
   |                                       |                                                                                                                                                                                           |
   |                                       | Handling suggestion: Create a postgres database.                                                                                                                                          |
   +---------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Migration from MongoDB to DDS
-----------------------------

.. table:: **Table 3** Checking whether the source database is connected

   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the source database is connected                                                                                                                                                                  |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check the connectivity and accuracy of the IP address, port number, username, and password of the source database.                                                                                        |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | Failure cause: The connection fails.                                                                                                                                                                      |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Configure the network by referring to "Network Types" in Real-Time Migration.                                                                                                        |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The username, password, or authentication database of the source database is incorrect.                                                                                                    |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Check that the input username, password, and authentication database for the connection test are correct.                                                                            |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The database is unavailable.                                                                                                                                                               |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                           |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: An internal error occurs.                                                                                                                                                                  |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                           |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: SSL connection parameters are not configured.                                                                                                                                              |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Contact technical support.                                                                                                                                                           |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                       | Failure cause: The source database cannot connect to the port of the replication instance.                                                                                                                |
   |                                       |                                                                                                                                                                                                           |
   |                                       | Handling suggestion: Modify the firewall, security group, or ACL configurations of the source and destination databases to enable the source database to connect to the port of the replication instance. |
   +---------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
