:original_name: drs_16_1157.html

.. _drs_16_1157:

Why Is the Delay High In Migration from MongoDB to DDS?
=======================================================

Involved Scenarios
------------------

-  Migration from MongoDB to DDS
-  Migration from DDS to MongoDB

Possible Causes
---------------

To ensure the performance of migration, synchronization, or disaster recovery, DRS performs concurrent replay at the collection level in the incremental phase. In the following special cases, DRS supports only single-thread write and does not support concurrent replay:

-  The collection index contains a unique key.
-  The value of **capped** of the collection attribute is **true**.

If the delay increases, check whether the problem is caused by the preceding reasons.
