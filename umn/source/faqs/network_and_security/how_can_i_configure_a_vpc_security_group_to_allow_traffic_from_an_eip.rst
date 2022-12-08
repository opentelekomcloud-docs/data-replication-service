:original_name: drs_01_0112.html

.. _drs_01_0112:

How Can I Configure a VPC Security Group to Allow Traffic from an EIP?
======================================================================

By default, a VPC on the current cloud is isolated from external networks for security reasons. You cannot use an EIP outside a VPC (for example, an EIP of another cloud database or an on-premise database) to access DB instances inside the VPC. However, the replication instance or destination database in a VPC needs to connect to an external EIP to migrate data.

Therefore, you need to add an outbound rule to a security group to allow access from specific external EIPs and ports outside the VPC. The outbound rule allows the replication instance EIP to access the destination database EIP.
