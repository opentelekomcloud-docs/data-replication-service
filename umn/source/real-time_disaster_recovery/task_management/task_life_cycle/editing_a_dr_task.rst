:original_name: drs_03_0026.html

.. _drs_03_0026:

Editing a DR Task
=================

For a DR task that has been created but not started, DRS allows you to edit the configuration information of the task, including the source and destination database details. For DR tasks in the following statuses, you can edit and submit the tasks again.

-  Creating
-  Configuration

Prerequisites
-------------

You have logged in to the DRS console.

Method 1
--------

#. In the task list on the **Disaster Recovery Management** page, locate the target task and click **Edit** in the **Operation** column.

#. .. _drs_03_0026__li105671010104417:

   On the **Configure Source and Destination Databases** page, enter information about the service and DR databases and click **Next**.

#. On the **Check Task** page, check the DR task.

   -  If any check fails, review the failure cause and rectify the fault. After the fault is rectified, click **Check Again**.

   -  If the check is complete and the check success rate is 100%, go to the **Compare Parameter** page.

      .. note::

         You can proceed to the next step only when all checks are successful. If there are any items that require confirmation, view and confirm the details first before proceeding to the next step.

#. On the displayed page, specify **Start Time** and DR instance details. Then, click **Submit**.

   .. table:: **Table 1** Task and recipient description

      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                          |
      +===================================+======================================================================================================================================================+
      | Start Time                        | Set **Start Time** to **Start upon task creation** or **Start at a specified time** based on site requirements.                                      |
      |                                   |                                                                                                                                                      |
      |                                   | .. note::                                                                                                                                            |
      |                                   |                                                                                                                                                      |
      |                                   |    Starting a DR task may slightly affect the performance of the service and DR databases. You are advised to start a DR task during off-peak hours. |
      +-----------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

#. .. _drs_03_0026__li34303618172657:

   After the DR task is submitted, view and manage it on the **Disaster Recovery Management** page.

   -  You can view the task status. For more information about task status, see :ref:`Task Statuses <drs_02_0025>`.
   -  You can click |image1| in the upper-right corner to view the latest task status.

Method 2
--------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the displayed page, click **edit this task** to go to the **Configure Source and Destination Databases** page.
#. Perform :ref:`2 <drs_03_0026__li105671010104417>` through :ref:`5 <drs_03_0026__li34303618172657>` in method 1.

.. |image1| image:: /_static/images/en-us_image_0000001341414072.png
