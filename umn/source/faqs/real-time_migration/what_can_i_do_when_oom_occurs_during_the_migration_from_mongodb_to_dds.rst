:original_name: drs_15_0100.html

.. _drs_15_0100:

What Can I Do When OOM Occurs During the Migration from MongoDB to DDS?
=======================================================================

Scenarios
---------

Out of memory (OOM) occurs during the migration from MongoDB to DDS, causing migration failures.

Possible Cause
--------------

The possible causes are as follows:

-  If the mongod service of the source database is deployed on a single server, OOM occurs when the migration process consumes large amounts of memory through operations such as creating indexes and sorting queries.
-  If the mongod service is deployed on a server with other services and the **cacheSizeGB** value is not specified, OOM occurs when all available memory has been allocated to other services, so the WiredTiger engine does not have sufficient memory.

   .. note::

      By default, the memory used by the WiredTiger engine of mongod is calculated as follows: (Memory in GB - 1 GB) x 50% for version 3.2 or (Memory in GB - 1 GB) x 60% for version 3.4 and later.

Solution
--------

-  If the mongod service is deployed on a single server, do not perform any operations that consume large amounts of memory during the migration.
-  If the mongod service and other services are deployed on the same server, set the value of **cacheSizeGB** to the half of the minimal idle memory to ensure that memory used in peak hours will not be allocated to WiredTiger excessively.
