:original_name: drs_16_0001.html

.. _drs_16_0001:

How Do I Disable the Balancer?
==============================

Before using the DRS service to migrate collections between sharded clusters, you must disable the balancer of the collections to be migrated.

.. note::

   -  After the migration is complete, enable the balancer. The balancer is disabled during the migration, generating different numbers of chunks on each shard of the source database. After the balancer is enabled, chunks will be distributed between shards in the cluster, which may affect the performance of the source database.

Procedure
---------

#. Log in to a database through mongo shell.

#. Run the following command in the command window of the mongos node to switch to the config database:

   **use config**

#. Run the following commands to check whether the balancer can be disabled:

   .. code-block::

      while( sh.isBalancerRunning() ) {
                print("waiting...");
                sleep(1000);
      }

   -  If the command output is **waiting**, the balancer is migrating chunks. In this case, do not disable the balancer. Otherwise, data inconsistency may occur.


      .. figure:: /_static/images/en-us_image_0000001391694037.png
         :alt: **Figure 1** Viewing the command output

         **Figure 1** Viewing the command output

   -  If no command output is displayed, the balancer is not migrating any chunks. In this case, you can disable the balancer:

#. Disable the balancer.

   -  If you migrate the entire DB instance, run the following command to disable the balancer.

      .. code-block::

         sh.stopBalancer()

   -  If you need to disable the balancer of the sharded collections to be migrated, run the following command:

      .. code-block::

         sh.disableBalancing("database.collection")

      **database.collection** indicates the namespace of the collection to be migrated.
