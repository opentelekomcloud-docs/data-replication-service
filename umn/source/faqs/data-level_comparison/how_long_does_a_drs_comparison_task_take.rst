:original_name: drs_16_1162.html

.. _drs_16_1162:

How Long Does a DRS Comparison Task Take?
=========================================

-  Object comparison: Generally, the comparison results are returned within several minutes based on the query performance of the source database. If the amount of data is large, the comparison may take dozens of minutes.
-  Row comparison: The SELECT COUNT method is used. The query speed depends on the database performance.
-  Value comparison: If the database workload is not heavy and the network is normal, the comparison speed is about 5 MB/s.
