:original_name: drs_16_1151.html

.. _drs_16_1151:

Why Do I Use the SCAN IP Address to Connect to an Oracle RAC Cluster?
=====================================================================

If the source Oracle database is an RAC cluster, you are advised to use SCAN IP+SERVICE_NAMES to create a task because SCAN IP has stronger fault tolerance, better load balancing capability, and faster synchronization.

-  If the SCAN IP address is used, ensure that the SCAN IP address can communicate with all virtual IP addresses of the source database. Otherwise, the connection test cannot be passed.
-  If SCAN IP is not used, the virtual IP address of a node can be used. If other nodes are abnormal, the synchronization process is not affected.

For details about the SCAN IP address, see the `documents <https://docs.oracle.com/en/database/oracle/oracle-database/12.2/rilin/about-scan-vip-addresses.html>`__ on the Oracle official website.
