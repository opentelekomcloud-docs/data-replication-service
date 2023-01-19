:original_name: drs_03_0128.html

.. _drs_03_0128:

Task Creation Example
=====================

This section describes how to create a real-time migration task by calling an API.

Involved APIs
-------------

-  API for obtaining tokens from IAM

   Obtain a token and add **X-Auth-Token** to the request header of API calls.

-  API used to create a real-time migration task.

Procedure
---------

#. Obtain the token by referring to :ref:`Authentication <drs_01_0005>`.

#. Obtain the DRS endpoints.

   -  Before calling this API, obtain the required `region and endpoint <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.

#. Obtain the project ID of a user in a region. For details, see :ref:`Obtaining a Project ID <drs_api_0106>`.

#. Send POST https://{*DRS endpoint*}/v3/{projectId}/jobs.

#. Add **X-Auth-Token** to the request header. The value is user token.

#. Add the **Content-Type** key to the request header. The value of **Content-Type** is **application/json**.

#. Specify the following parameters in the request body:

   .. note::

      For details about the API used for creating DB instances, see :ref:`Creating Tasks in Batches <drs_03_0104>`.

   .. code-block::

      {
          "bind_eip": true,//Check whether an EIP has been bound to the replication instance in the public network scenario.
          "db_use_type": "migration",//The usage type. The value can be migration (real-time migration), sync (real-time synchronization), or cloudDataGuard (real-time DR). This parameter is mandatory.
          ""description": "",//Task description
          "engine_type": "mysql",//The engine type. The value can be mysql, mongodb, or cloudDataGuard-mysql.
          "is_target_readonly": true,//Specifies whether the destination instance is readable only.
          "job_direction": "up",//Task direction. The value can be up or down.
          "name": "DRS-2057",//Task name. This parameter is mandatory.
          "net_type": "eip",// Network type. This parameter is mandatory and the value can be vpn, vpc, or eip.
          "node_type": "high",//Specification type. This parameter is mandatory.
          "source_Endpoint": {//Information body of the source database. This parameter is mandatory.
              "db_type": "mysql",//The database type. The value can be mysql, mongodb, or gaussdbv5. This parameter is mandatory.
          },
          "target_Endpoint": {//Information body of the destination database
              "db_type": "mysql",//Database type. This parameter is mandatory.
          "inst_id": "63e0699063494a8a93798f38abf3247ein01",// RDS instance ID. This parameter is mandatory when the database is an RDS DB instance.
              "region": "eu-de" // The region where the RDS DB instance is located. This parameter is mandatory when the database is an RDS DB instance.
          },
          "task_type": "FULL_INCR_TRANS" //Task mode. The value can be FULL_TRANS or FULL_INCR_TRANS.
      }

   If the request fails, an error code and error information are returned. For details, see section :ref:`Error Code <drs_05_0004>`.
