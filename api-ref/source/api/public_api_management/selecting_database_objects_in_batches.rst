:original_name: drs_03_0109.html

.. _drs_03_0109:

Selecting Database Objects in Batches
=====================================

Function
--------

This API is used to select the databases or tables to be migrated.

Constraints
-----------

-  Only real-time migration and real-time synchronization support object selection.
-  After a task is created, the task status is **CONFIGURATION**. The task can be invoked only after the test of connections to the source and destination databases is successful and the API for modifying the task is invoked.

URI
---

PUT /v3/{project_id}/jobs/batch-select-objects

.. table:: **Table 1** Path parameters

   ========== ========= ====== ==================================
   Parameter  Mandatory Type   Description
   ========== ========= ====== ==================================
   project_id Yes       String Project ID of a tenant in a region
   ========== ========= ====== ==================================

Request Parameters
------------------

.. table:: **Table 2** Request header parameters

   +-----------------+-----------------+-----------------+--------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                |
   +=================+=================+=================+============================================+
   | Content-Type    | Yes             | String          | The content type.                          |
   |                 |                 |                 |                                            |
   |                 |                 |                 | The default value is **application/json**. |
   +-----------------+-----------------+-----------------+--------------------------------------------+
   | X-Auth-Token    | Yes             | String          | User token obtained from IAM.              |
   +-----------------+-----------------+-----------------+--------------------------------------------+
   | X-Language      | No              | String          | Request language type                      |
   |                 |                 |                 |                                            |
   |                 |                 |                 | Default value: **en-us**                   |
   |                 |                 |                 |                                            |
   |                 |                 |                 | Values:                                    |
   |                 |                 |                 |                                            |
   |                 |                 |                 | -  **en-us**                               |
   |                 |                 |                 | -  **zh-cn**                               |
   +-----------------+-----------------+-----------------+--------------------------------------------+

.. table:: **Table 3** Request body parameters

   +-----------+-----------+------------------------------------------------------------------------------------------------+----------------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                                           | Description                                                    |
   +===========+===========+================================================================================================+================================================================+
   | jobs      | Yes       | Array of :ref:`UpdateDatabaseObjectReq <drs_03_0109__request_updatedatabaseobjectreq>` objects | Request task ID list for updating database objects in batches. |
   +-----------+-----------+------------------------------------------------------------------------------------------------+----------------------------------------------------------------+

.. _drs_03_0109__request_updatedatabaseobjectreq:

.. table:: **Table 4** UpdateDatabaseObjectReq

   +-----------------+-----------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type                                                                     | Description                                                                                          |
   +=================+=================+==========================================================================+======================================================================================================+
   | job_id          | Yes             | String                                                                   | Task ID.                                                                                             |
   +-----------------+-----------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | selected        | No              | Boolean                                                                  | Whether to select an object. If this parameter is not set, the default value is **No**.              |
   |                 |                 |                                                                          |                                                                                                      |
   |                 |                 |                                                                          | **Yes**: Customize the objects to be migrated.                                                       |
   |                 |                 |                                                                          |                                                                                                      |
   |                 |                 |                                                                          | **No**: Migrate all VMs.                                                                             |
   +-----------------+-----------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | sync_database   | No              | Boolean                                                                  | Whether to perform database-level synchronization.                                                   |
   +-----------------+-----------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+
   | job             | No              | Array of :ref:`DatabaseInfo <drs_03_0109__request_databaseinfo>` objects | Data object selection information. This parameter is mandatory when **selected** is set to **true**. |
   +-----------------+-----------------+--------------------------------------------------------------------------+------------------------------------------------------------------------------------------------------+

.. _drs_03_0109__request_databaseinfo:

.. table:: **Table 5** DatabaseInfo

   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                         |
   +===================+=================+=================+=====================================================================================================================================================================================================================================================================================================================+
   | id                | No              | String          | When **object_type** is set to **database**, this parameter indicates the database name. If **object_type** is set to **table** or **view**, set the field value by referring to the example.                                                                                                                       |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | parent_id         | No              | String          | Database name. This parameter is mandatory when **object_type** is set to **table** or **view**.                                                                                                                                                                                                                    |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | object_type       | No              | String          | Type. Values:                                                                                                                                                                                                                                                                                                       |
   |                   |                 |                 |                                                                                                                                                                                                                                                                                                                     |
   |                   |                 |                 | -  **database**                                                                                                                                                                                                                                                                                                     |
   |                   |                 |                 | -  **table**                                                                                                                                                                                                                                                                                                        |
   |                   |                 |                 | -  **schema**                                                                                                                                                                                                                                                                                                       |
   |                   |                 |                 | -  **view**                                                                                                                                                                                                                                                                                                         |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | object_name       | No              | String          | Database object name, database name, table name, and view name.                                                                                                                                                                                                                                                     |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | select            | No              | String          | Whether to migrate the database objects. **true** indicates that the database objects will be migrated. **false** indicates that the database objects will not be migrated. **partial** indicates some tables in the database will be migrated. If this parameter is not specified, the default value is **false**. |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | object_alias_name | No              | String          | Alias, which is the new mapped name.                                                                                                                                                                                                                                                                                |
   +-------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 6** Response body parameters

   +------------+---------------------------------------------------------------------------------------+-------------------------------------------------+
   | Parameter  | Type                                                                                  | Description                                     |
   +============+=======================================================================================+=================================================+
   | all_counts | Long                                                                                  | Total number.                                   |
   +------------+---------------------------------------------------------------------------------------+-------------------------------------------------+
   | results    | Array of :ref:`DatabaseObjectResp <drs_03_0109__response_databaseobjectresp>` objects | Response list for selecting objects in batches. |
   +------------+---------------------------------------------------------------------------------------+-------------------------------------------------+

.. _drs_03_0109__response_databaseobjectresp:

.. table:: **Table 7** DatabaseObjectResp

   +------------+---------+---------------------------------------------------------------------------------------------------+
   | Parameter  | Type    | Description                                                                                       |
   +============+=========+===================================================================================================+
   | job_id     | String  | Task ID.                                                                                          |
   +------------+---------+---------------------------------------------------------------------------------------------------+
   | status     | Boolean | The status that indicates that objects are selected.                                              |
   +------------+---------+---------------------------------------------------------------------------------------------------+
   | error_code | String  | Error code, which is optional and indicates the returned information about the failure status.    |
   +------------+---------+---------------------------------------------------------------------------------------------------+
   | error_msg  | String  | Error message, which is optional and indicates the returned information about the failure status. |
   +------------+---------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

-  Object selection example:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-select-objects

   .. code-block::

      {
        "jobs" : [ {
          "job" : [ {
            "id" : "fastunit",
            "parent_id" : null,
            "object_name" : "fastunit",
            "object_type" : "database",
            "select" : "partial",
            "object_alias_name" : null
          }, {
            "id" : "fastunit-*-*-coll",
            "parent_id" : "fastunit",
            "object_name" : "coll",
            "object_type" : "table",
            "select" : "true",
            "object_alias_name" : null
          }, {
            "id" : "ycy1",
            "parent_id" : null,
            "object_name" : "ycy1",
            "object_type" : "database",
            "select" : "partial",
            "object_alias_name" : null
          }, {
            "id" : "ycy1-*-*-coll",
            "parent_id" : "ycy1",
            "object_name" : "coll",
            "object_type" : "table",
            "select" : "true",
            "object_alias_name" : null
          }, {
            "id" : "ycy1-*-*-collcount",
            "parent_id" : "ycy1",
            "object_name" : "collcount",
            "object_type" : "table",
            "select" : "true",
            "object_alias_name" : null
          } ],
          "job_id" : "57fd2692-0ebe-4714-9b59-fe7aa65djb15",
          "selected" : true
        } ]
      }

-  Example of full migration:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-select-objects

   .. code-block::

      {
        "jobs" : [ {
          "job" : [ ],
          "job_id" : "e59f5eef-2bcc-4461-b9ac-10aded44jb15",
          "selected" : false
        } ]
      }

Example Response
----------------

**Status code: 202**

Accepted

.. code-block::

   {
       "all_counts": 1,
       "results": [{
           "job_id": "4d700f6f-9a17-47e0-a7d6-1bc2155jb101",
           "status": true
       }]
   }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
202         Accepted
400         Bad Request
=========== ===========

Error Code
----------

For details, see :ref:`Error Code <drs_05_0004>`.
