:original_name: drs_16_0123.html

.. _drs_16_0123:

What Can I Do When Scheduled Task Failed to Start Leaving Message "can not get agency token"
============================================================================================

When you use a subaccount to use scheduled task startup function, the **account entrustment** function must be used. Otherwise, the scheduled task fails to be started, leaving message "can not get agency token".

Solution
--------

Two solutions are provided as follows:

-  Method 1: Use your primary account to create a task and select **Start at a specified time** for **Start Time**.
-  Method 2: Use the primary account to add the Security Administrator permission to the user group to which the subaccount belongs. Then, create a task again, and select **Start at a specified time** for **Start Time**.
-  Method 3: Create a task again and select **Start upon task creation** for **Start Time**.
