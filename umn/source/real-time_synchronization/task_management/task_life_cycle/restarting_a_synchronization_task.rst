:original_name: drs_10_0412.html

.. _drs_10_0412:

Restarting a Synchronization Task
=================================

DRS allows you to restart a synchronization task after task parameters are changed in :ref:`Changing Task Parameters <drs_10_0410>`.

Constraints
-----------

-  Tasks in the **Full**, **Full synchronization failed**, **Incremental**, or **Incremental synchronization failed** state can be restarted.
-  Only the synchronization tasks of the following engines can be restarted:

   -  MySQL->MySQL
   -  MySQL -> GaussDB Distributed
   -  MySQL->TaurusDB
   -  MySQL->Kafka

Method 1
--------

#. In the task list on the **Data Synchronization Management** page, locate the target task and click **Restart** in the **Operation** column.
#. In the displayed **Restart Task** dialog box, click **Yes**.

Method 2
--------

#. On the **Data Synchronization Management** page, click the target synchronization task in the **Task Name/ID** column.
#. On the **Basic Information** page, click **Restart** in the upper right corner.
#. In the displayed **Restart Task** dialog box, click **Yes**.
