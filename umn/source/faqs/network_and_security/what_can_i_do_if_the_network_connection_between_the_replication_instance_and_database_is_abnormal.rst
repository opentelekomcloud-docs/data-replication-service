:original_name: drs_02_0100.html

.. _drs_02_0100:

What Can I Do If the Network Connection Between the Replication Instance and Database Is Abnormal?
==================================================================================================

Before data migration, ensure that network preparations and security rule settings are complete. If the connection is abnormal, check whether the network configuration is correct.

This section uses the migration from MySQL to RDS MySQL as an example to describe three migration scenarios: cross-cloud real-time migration, on-premises database migration, and real-time migration of self-built ECS databases.

Cross-Cloud Real-Time Migration
-------------------------------

#. Network settings

   Enable public accessibility for the source database.

   -  Source database network settings:

      Enable public accessibility for the source database.

      For details, see related documents provided by Alibaba Cloud.

   -  Destination database network settings:

      By default, the destination database and the DRS replication instance are in the same VPC and can communicate with each other. No further configuration is required.

#. Security rules

   -  Source database security group settings:

      Add the EIP of the replication instance to the whitelist of the source MySQL DB instance to allow the access from the EIP.

      Before configuring the whitelist for the source database, obtain the EIP of the DRS replication instance. You can find the EIP on the **Configure Source and Destination Databases** page after creating the replication instance on the DRS console.

      You can also add 0.0.0.0/0 to the source database whitelist to allow any IP address to access the source database but you must ensure that the above does not pose a risk to your services.

      After the migration is complete, you can delete the configuration from the whitelist.

   -  Destination database security group settings:

      -  By default, the destination database and the DRS replication instance are in the same VPC and can communicate with each other. DRS can directly write data to the destination database.
      -  Configure the security group of the VPC where the destination database is located to ensure that the IP addresses and listening ports of the DRS instance are allowed to access the on-premises database.

Real-Time Migration of On-Premises Databases
--------------------------------------------

#. Network settings

   -  Source database network settings:

      You can migrate on-premises MySQL databases to the RDS MySQL databases on the current cloud through a VPN or public network. Enable public accessibility or establish a VPN for the on-premises MySQL databases based on the site requirements. You are advised to migrate data through a public network, which is more convenient and cost-effective.

   -  Destination database network settings:

      -  If the source database attempts to access the destination database through a VPN, ensure that the VPN service is enabled and the source database can communicate with the destination RDS MySQL database.
      -  If the source database attempts to access the destination database through a public network, you do not need to configure the destination RDS MySQL database.

#. Security rules

   a. Source database security group settings:

      -  If the migration is performed over a public network, add the EIP of the DRS replication instance to the network whitelist of the source MySQL database to enable the source MySQL database to communicate with the current cloud. Before setting the network whitelist, obtain the EIP of the replication instance.

         The IP address on the **Configure Source and Destination Databases** page is the EIP of the replication instance.

      -  If the migration is performed over a VPN network, add the private IP address of the DRS migration instance to the network whitelist of the source MySQL database to enable the source MySQL database to communicate with the current cloud. The IP address on the **Configure Source and Destination Databases** page is the private IP address of the replication instance.

      After the migration is complete, you can delete the rules.

   b. Destination database security group settings:

      -  By default, the destination database and the DRS replication instance are in the same VPC and can communicate with each other. DRS can directly write data to the destination database.
      -  Configure the security group of the VPC where the destination database is located to ensure that the IP addresses and listening ports of the DRS instance are allowed to access the on-premises database.

Real-Time Migration of Self-Built Databases on the ECS
------------------------------------------------------

#. Network settings

   -  The source and destination databases must be in the same region.
   -  The source and destination databases can be either in the same VPC or different VPCs.

      -  If the source and destination databases are in the same VPC, the networks are interconnected by default.
      -  If the source and destination databases are in different VPCs, the subnets of the source and destination databases are required to be in different CIDR blocks. You need to create a VPC peering connection between the two VPCs.

#. Security rules

   -  In the same VPC, the network is connected by default. You do not need to set a security group.
   -  In different VPCs, establish a VPC peering connection between the two VPCs. You do not need to set a security group.

Checking iptables Settings
--------------------------

If the source database is a self-built database on an ECS and cannot be connected after the preceding operations are performed, check the iptables settings. If the DRS frequently initiates connection requests and fails, the HOSTGUARD service adds the requested IP address to the blacklist.

#. Log in to the ECS.

#. Run the following command to check whether any DENY-related project contains the IP address of the DRS instance. The project name is **IN_HIDS_MYSQLD_DENY_DROP**.

   **iptables --list**

#. If yes, run the following command to query the iptables inbound rule list and obtain the rule ID (line-numbers):

   **iptables -L INPUT --line-numbers**

#. Run the following command to delete the inbound rules that deny the IP address of the DRS instance: (Note: Delete the rules from the end to the beginning. Otherwise, line-numbers will be updated and you need to query again.)

   **iptables -D** *Project_name* *Rule_ID*

#. Delete the iptables rules and test the connection again.
