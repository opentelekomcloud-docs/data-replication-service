:original_name: drs_10_0401.html

.. _drs_10_0401:

Modifying the Flow Control Mode
===============================

You can choose whether to control the flow. DRS allows you to change the flow control mode after a task is created. Currently, only the following real-time migration types support this function:

-  To the cloud

   -  MySQL->MySQL
   -  MySQL -> GaussDB(for MySQL) primary/standby
   -  Oracle->PostgreSQL
   -  PostgreSQL->PostgreSQL

-  Out of the cloud

   -  MySQL->MySQL

-  Self-built databases -> Self-built databases

   -  MySQL->MySQL

.. note::

   -  The flow control mode takes effect only in the full synchronization phase.
   -  After the traffic rate is modified in the incremental migration phase, the modification takes effect when the task enters the full migration phase again. For example, if the traffic rate is modified and a synchronization object is added to the task, the modification takes effect in the full synchronization phase of the task.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A synchronization task has been created.

Method 1
--------

#. In the **Synchronization Information** area on the **Basic Information** tab, click **Modify** next to the **Flow Control** field.
#. In the displayed dialog box, modify the settings.

Method 2
--------

#. In the task list on the **Data Synchronization Management** page, locate the target task and choose **More** > **Speed** or **Speed** in the **Operation** column.
#. In the displayed dialog box, modify the settings.
