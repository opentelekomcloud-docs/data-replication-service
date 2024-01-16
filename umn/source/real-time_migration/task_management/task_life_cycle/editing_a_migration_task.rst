:original_name: drs_03_0002.html

.. _drs_03_0002:

Editing a Migration Task
========================

For a migration task that has been created but not started, DRS allows you to edit the configuration information of the task, including the task information, replication instance information, and migration information. For migration tasks in the following statuses, you can edit the tasks again after the replication instances are created:

-  Creating
-  Configuration

   .. note::

      For a started migration task, modifying the migration objects is not supported.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has been created.

Method 1
--------

#. In the task list on the **Online Migration Management** page, locate the target task and click **Edit** in the **Operation** column.

#. .. _drs_03_0002__li105671010104417:

   On the **Configure Source and Destination Databases** page, enter information about the source and destination databases and click **Next**.

#. On the **Set Task** page, select the accounts and objects to be migrated, and click **Next**.

   .. table:: **Table 1** Migration types and objects

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                    |
      +===================================+================================================================================================================================================================================================================================================================================================================================================================+
      | Flow Control                      | You can choose whether to control the flow.                                                                                                                                                                                                                                                                                                                    |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  **Yes**                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    You can customize the maximum migration speed.                                                                                                                                                                                                                                                                                                              |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    In addition, you can set the time range based on your service requirements. The traffic rate setting usually includes setting of a rate limiting time period and a traffic rate value. Flow can be controlled all day or during specific time ranges. The default value is **All day**. A maximum of three time ranges can be set, and they cannot overlap. |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    The flow rate must be set based on the service scenario and cannot exceed 9,999 MB/s.                                                                                                                                                                                                                                                                       |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  **No**                                                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    The migration speed is not limited and the outbound bandwidth of the source database is maximally used, which will increase the read burden on the source database. For example, if the outbound bandwidth of the source database is 100 MB/s and 80% bandwidth is used, the I/O consumption on the source database is 80 MB/s.                             |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    .. note::                                                                                                                                                                                                                                                                                                                                                   |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |       -  Flow control mode takes effect only during a full migration.                                                                                                                                                                                                                                                                                          |
      |                                   |       -  You can also change the flow control mode after creating a task. For details, see :ref:`Modifying the Flow Control Mode <drs_03_0046>`.                                                                                                                                                                                                               |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Migrate Account                   | During a database migration, accounts need to be migrated separately.                                                                                                                                                                                                                                                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | There are accounts that can be migrated completely, accounts whose permissions need to be reduced, and accounts that cannot be migrated. You can choose whether to migrate the accounts based on service requirements. If you select **Yes**, you can select the accounts to be migrated as required.                                                          |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  **Yes**                                                                                                                                                                                                                                                                                                                                                     |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    If you need to migrate accounts, see :ref:`Migrating Accounts <drs_09_0017>`.                                                                                                                                                                                                                                                                               |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  **No**                                                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    During migration, accounts, permissions, and passwords are not migrated.                                                                                                                                                                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Filter DROP DATABASE              | To reduce the risks involved in data migration, DDL operations can be filtered out. You can choose not to synchronize certain DDL operations.                                                                                                                                                                                                                  |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  If you select **Yes**, any database deletion operations performed on the source database are not migrated during data migration.                                                                                                                                                                                                                            |
      |                                   | -  If you select **No**, related operations are migrated to the destination database during data migration.                                                                                                                                                                                                                                                    |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Migrate Object                    | You can choose to migrate all objects, tables, or databases based on your service requirements.                                                                                                                                                                                                                                                                |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | -  **All**: All objects in the source database are migrated to the destination database. After the migration, the object names will remain the same as those in the source database and cannot be modified.                                                                                                                                                    |
      |                                   | -  **Tables**: The selected table-level objects will be migrated.                                                                                                                                                                                                                                                                                              |
      |                                   | -  **Databases**: The selected database-level objects will be migrated.                                                                                                                                                                                                                                                                                        |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | If the source database is changed, click |image1| in the upper right corner before selecting migration objects to ensure that the objects to be selected are from the changed source database.                                                                                                                                                                 |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                                   |                                                                                                                                                                                                                                                                                                                                                                |
      |                                   |    -  If you choose not to migrate all of the databases, the migration may fail because the objects, such as stored procedures and views, in the databases to be migrated may have dependencies on other objects that are not migrated. To prevent migration failure, migrate all of the databases.                                                            |
      |                                   |    -  If the object name contains spaces, the spaces before and after the object name are not displayed. If there are multiple spaces between the object name and the object name, only one space is displayed.                                                                                                                                                |
      |                                   |    -  The name of the selected migration object cannot contain spaces.                                                                                                                                                                                                                                                                                         |
      |                                   |    -  To quickly select the desired database objects, you can use the search function.                                                                                                                                                                                                                                                                         |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. On the **Check Task** page, check the migration task.

   -  If any check fails, review the cause and rectify the fault. After the fault is rectified, click **Check Again**.

      For details about how to handle check items that fail to pass the pre-check, see :ref:`Solutions to Failed Check Items <drs_11_0001>`.

   -  If the check is complete and the check success rate is 100%, click **Next**.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the **Confirm Task** page, specify **Start Time**, confirm that the configured information is correct, and click **Submit** to submit the task.

   .. note::

      -  Set **Start Time** to **Start upon task creation** or **Start at a specified time** based on site requirements.
      -  After a migration task is started, the performance of the source and destination databases may be affected. You are advised to start a migration task during off-peak hours.
      -  Under specific conditions, the destination database needs to be restarted once during the task startup, which may interrupt database services.

#. .. _drs_03_0002__li620112563620:

   After the task is submitted, view and manage it on the **Online Migration Management** page.

   -  You can view the task status. For more information about task status, see :ref:`Task Statuses <drs_03_0001>`.
   -  You can click |image2| in the upper-right corner to view the latest task status.

Method 2
--------

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the displayed page, click **edit this task** to go to the **Configure Source and Destination Databases** page.
#. Perform steps :ref:`2 <drs_03_0002__li105671010104417>` to :ref:`6 <drs_03_0002__li620112563620>`.

.. |image1| image:: /_static/images/en-us_image_0000001710470728.png
.. |image2| image:: /_static/images/en-us_image_0000001758429493.png
