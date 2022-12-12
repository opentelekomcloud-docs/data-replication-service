:original_name: drs_03_0100.html

.. _drs_03_0100:

Resetting a Migration Task
==========================

During the migration, if a migration task fails due to uncertain causes, the background will resume the task several times. However, the task may fail to be recovered in some scenarios. To continue the migration, DRS allows you to reset the task.

You can reset failed migration tasks in any of the following statuses:

-  Migration failure status

Prerequisites
-------------

-  You have logged in to the DRS console.
-  A migration task has failed.

Method 1
--------

#. In the task list on the **Online Migration Management** page, locate the target task and click **Reset** in the **Operation** column.

#. .. _drs_03_0100__li1764125135215:

   In the displayed dialog box, check the migration task again.

#. .. _drs_03_0100__li1436312473210:

   After the check is complete and the check success rate is 100%, click **Start** to submit the migration task again.

Method 2
--------

#. On the **Data Migration Management** page, click the target task name in the **Task Name/ID** column.
#. On the displayed page, click the **Migration Progress** tab, and click **Reset** in the upper left corner.
#. Perform :ref:`2 <drs_03_0100__li1764125135215>` to :ref:`3 <drs_03_0100__li1436312473210>` from method 1.
