:original_name: drs_16_1148.html

.. _drs_16_1148:

Why Does the Delay of DR Tasks Increase?
========================================

Causes for an Increase in RTO
-----------------------------

Recovery Time Objective (RTO) is duration of time within which transactions on the DRS instance are transmitted and replayed to the destination database during incremental synchronization. If the RTO value is large, transactions to be replayed on the DRS instance are stacked. The possible causes are as follows:

#. After a DR task is initialized, the incremental data generated from the time when the DR task is started to the current time needs to be replayed.
#. Batch operations are performed on service database tables that do not have primary keys. The DR instance is synchronizing tables that do not have primary keys and have a large amount of changed data. To ensure data consistency in tables without primary keys, all operations are recorded. As a result, the operation execution efficiency is lower than that in tables with primary keys. In addition, if the destination table has no index, the data update efficiency is lower.
#. If the DDL operation is performed on the service database, the DR instance can replay data only after the execution of the DDL operation is complete.
#. Frequently executed operations are performed on hot tables in the service database. The DR instance combines the transactions of the hot table and then replays the transactions, reducing frequent operations on the destination database.
#. The access to the DR database is abnormal. As a result, the incremental data cannot be replayed.

Handling Suggestion for an Increase in RTO
------------------------------------------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the **Basic Information** page, click the **Disaster Recovery Monitoring** tab to view the changes of RTO.

   -  If RTO decreases gradually or increases only in a short time, no action is required.

   -  If RTO keeps increasing, run the following statement in the DR database to check whether there are SQL statements that take a long time to execute or DDL statements that are being executed:

      .. code-block::

         show processlist

   -  If the DR database is abnormal, contact database O&M engineers.

Causes for an Increase in RPO
-----------------------------

Recovery Point Objective (RPO) refers to the time that passes from when a transaction in the service database is submitted and the time when the transaction is synchronized to the DRS instance during the incremental synchronization. If RPO is large, the latest changes made to the service database data have not been extracted to the DR instance. The possible causes are as follows:

#. The network between the service database and the DRS DR instance is unstable. Reading changes in logs from the service database is slow.
#. The service database cannot be accessed. As a result, incremental data cannot be extracted.

Handling Suggestion for an Increase in RPO
------------------------------------------

#. On the **Disaster Recovery Management** page, click the target DR task in the **Task Name/ID** column.
#. On the **Basic Information** page, click the **Disaster Recovery Monitoring** tab to view the changes of RPO.

   -  If RPO decreases gradually or increases only in a short time, no action is required.
   -  If the service database is abnormal, contact database O&M engineers.
