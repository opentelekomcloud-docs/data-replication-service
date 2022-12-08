:original_name: drs_01_0104.html

.. _drs_01_0104:

When Can I Stop a Migration Task?
=================================

You can refer to the following methods to check whether the task can be stopped. Before stopping the task, ensure that:

#. At least one complete data comparison is performed during off-peak hours.
#. Service cutover is completed.

   a. Interrupt services first. If the workload is not heavy, you may do not need to interrupt the services.

   b. Run the following statement on the source database (MySQL is used as an example) and check whether there are statements executed by new sessions within 1 to 5 minutes. If not, the service is stopped.

      .. code-block:: text

         show processlist;

      .. note::

         The process list queried by the preceding statement includes the connection of the DRS replication instance. If no additional session executes SQL statements, the service has been stopped.

   c. When the real-time synchronization delay is 0s and remains stable for a period, you can perform a data-level comparison between the source and destination databases. For details about the time required, refer to the comparison results of the previous comparison.

      -  If there is enough time, compare all objects.
      -  If there is not enough time, use the data-level comparison to compare the tables that are frequently used and that contain key business data or inconsistent data.

   d. Determine a proper time to cut the services over to the destination database. Then, services can be used externally again.

#. Stopping a task only deletes the replication instance, and the migration task is still in the task list. You can choose whether to delete the task.
