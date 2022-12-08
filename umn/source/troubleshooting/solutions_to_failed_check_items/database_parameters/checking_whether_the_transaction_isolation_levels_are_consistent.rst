:original_name: drs_11_0453.html

.. _drs_11_0453:

Checking Whether the Transaction Isolation Levels are Consistent
================================================================

MySQL
-----

.. table:: **Table 1** Checking whether the transaction isolation levels are consistent

   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Check Item                            | Whether the transaction isolation levels are consistent                                                                                                                        |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Description                           | Check whether the transaction isolation levels of the source and destination databases are the same.                                                                           |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Failure Cause and Handling Suggestion | If you are migrating data to the cloud, perform the following operations:                                                                                                      |
   |                                       |                                                                                                                                                                                |
   |                                       | **Failure cause**: The transaction isolation levels of the source and destination databases are different.                                                                     |
   |                                       |                                                                                                                                                                                |
   |                                       | **Handling suggestion**: Change the isolation level (**tx_isolation** or **transaction_isolation**) of the destination database to be the same as that of the source database. |
   +---------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
