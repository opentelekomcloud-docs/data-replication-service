:original_name: drs_03_0046.html

.. _drs_03_0046:

Modifying the Flow Control Mode
===============================

You can choose whether to control the flow. DRS allows you to change the flow control mode after a task is created. Currently, only the following real-time migration types support this function:

-  To the cloud

   -  MySQL->MySQL
   -  MongoDB->DDS

-  From of the cloud

   -  MySQL->MySQL
   -  DDS->MongoDB

.. note::

   -  Flow control mode takes effect only during a full migration.
   -  After the traffic rate is modified in the incremental migration phase, the modification takes effect when the task enters the full migration phase again.

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has been created.

Method 1
--------

#. In the **Migration Information** area on the **Basic Information** tab, click **Modify** next to the **Flow Control** field.
#. In the displayed dialog box, modify the settings.

Method 2
--------

#. In the task list on the **Online Migration Management** page, locate the target task and choose **More** > **Speed** or **Speed** in the **Operation** column.
#. In the displayed dialog box, modify the settings.
