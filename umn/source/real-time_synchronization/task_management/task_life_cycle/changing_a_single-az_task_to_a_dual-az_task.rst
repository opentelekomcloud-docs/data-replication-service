:original_name: drs_06_0010.html

.. _drs_06_0010:

Changing a Single-AZ Task to a Dual-AZ Task
===========================================

DRS allows you to change a single-AZ task to a dual-AZ task, improving task reliability while remaining the original task.

Constraints
-----------

-  A dual-AZ task cannot be changed to a single-AZ task.
-  Only tasks in the **Incremental** or **Incremental failed** state can be changed.
-  Only synchronization tasks from GaussDB Centralized to Kafka can be changed.

Procedure
---------

#. Log in to the management console.
#. Click |image1| in the upper left corner and select a region and project.
#. Choose **Databases** > **Data Replication Service**. The **Data Replication Service** page is displayed.
#. On the **Data Synchronization Management** page, select the target task and choose **More** > **Change to Primary/Standby** in the **Operation** column.
#. On the displayed page, select the standby AZ. If the task is over a public network, you need to specify the EIP of the standby task and click **OK**.
#. After submitting the change, click **Back to Task List**. On the **Data Synchronization Management** page, the task status is **Changing to primary/standby**. After the task is changed, you can see that the parent task contains one primary and one standby subtask. The standby subtask and the parent task are in the **Configuration** state.
#. Click **Edit** in the **Operation** column of the parent task. On the displayed page, test the connections to the source and destination databases. If the connections are normal, click **Next**.
#. On the **Confirm Task** page, click **Start Task**. If the task is billed on a yearly/monthly basis, click **Pay and Start** to go to the payment page.

.. |image1| image:: /_static/images/en-us_image_0000001918683154.png
