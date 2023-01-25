:original_name: drs_16_0002.html

.. _drs_16_0002:

How Do I Set Global binlog_format=ROW to Take Effect Immediately?
=================================================================

During migration for MySQL databases, the source database binlog must be in the ROW format. Otherwise, the task fails. After **binlog_format=ROW** at the global level is set in the source database, all the previous service threads need to be stopped because these threads still connect the binlog in the non-ROW format.

Procedure
---------

#. Log in to the source database using the MySQL official client or other tools.

#. Run the following command for setting global parameters in the source database.

   .. code-block:: text

      set global binlog_format = ROW;

#. Run the following command on the source database and check whether the preceding operation is successful:

   .. code-block:: text

      select @@global.binlog_format;

#. You can use either of the following methods to ensure that the modified binlog format of the source database takes effect immediately:

   **Method 1**

   a. Select a non-service period to disconnect all service connections on the current database.

      #. Run the following command to query all service threads (excluding all binlog dump threads and current threads) in the current database:

         .. code-block:: text

            show processlist;

      #. Stop all the service threads queried in the previous step.

      .. note::

         Do not create or start a migration task before the preceding operations are complete. Otherwise, data may be inconsistent.

   b. To prevent the binlog format of the source database from becoming invalid due to database restart, add or modify the **binlog_format** parameter in the startup configuration file (**my.ini** or **my.cnf**) of the source database and save the modification.

      .. code-block:: text

         binlog_format=ROW

   **Method 2**

   a. To prevent the binlog format of the source database from becoming invalid due to database restart, add or modify the **binlog_format** parameter in the startup configuration file (**my.ini** or **my.cnf**) of the source database and save the modification.

      .. code-block:: text

         binlog_format=ROW

   b. Ensure that the **binlog_format** parameter is successfully added or modified. Then, restart the source database at a non-service period.
