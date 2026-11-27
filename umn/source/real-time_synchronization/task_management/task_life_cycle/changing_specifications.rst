:original_name: drs_11_0490.html

.. _drs_11_0490:

Changing Specifications
=======================

You can change the DRS task specifications based on your service requirements. After the specification change starts, the task enters the **Changing specifications** state and data synchronization is suspended. After the specification change is complete, the task is automatically resumed.

Constraints
-----------

-  DRS allows you to change the specifications of single-AZ synchronization tasks. Task specifications cannot be changed for dual-AZ tasks. The minimum specification that can be downgraded is medium.
-  DRS allows you to change the specifications of synchronization tasks only in the **Full**, **Full failed**, **Incremental**, or **Incremental failed** state.
-  After the task specifications are changed, the parameters you configured are set to the default parameters of the new specifications.
-  Before changing the task specifications, ensure that the current AZ supports the target specifications.
-  You are advised to change the task specifications during off-peak hours.
-  After the specification change starts, the task is suspended. The task is automatically resumed after the change is complete.
-  It takes about 30 minutes to change the task specifications.
-  Changing task specifications is a high-risk operation and may cause task change failures and task startup failures.

Procedure
---------

#. Log in to the management console.

#. Click |image1| in the upper left corner and select a region and project.

#. Choose **Databases** > **Data Replication Service**. The **Data Replication Service** page is displayed.

#. On the **Data Synchronization Management** page, select the target task and choose **More** > **Change Specifications** in the **Operation** column.

#. On the displayed page, select the desired specifications, perform a pre-check, and click **Next**.

#. Confirm specifications.

#. View the task specification change result.

   After the application is submitted, click **Back to Task List**. On the **Data Synchronization Management** page, the instance status is **Changing specifications**.

   After the task status changes from **Changing specifications** to another status, you can view the instance specifications on the **Basic Information** page to check whether the change is successful. Alternatively, you can view the change logs on the **Synchronization Logs** page to check whether the change is successful.

   -  **change specification start**: indicates that the specification change starts.
   -  **change specification success**: indicates that the specifications are changed.
   -  **change specification failed**: indicates that the specifications fail to be changed.

.. |image1| image:: /_static/images/en-us_image_0000002775303684.png
