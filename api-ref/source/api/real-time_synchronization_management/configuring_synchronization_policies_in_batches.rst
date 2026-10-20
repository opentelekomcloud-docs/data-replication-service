:original_name: drs_03_0149.html

.. _drs_03_0149:

Configuring Synchronization Policies in Batches
===============================================

Function
--------

-  This API is used to configure synchronization policies in batches, including conflict policies, DROP DATASE filtering, and object synchronization scope.

Constraints
-----------

This API supports synchronization policies.

URI
---

POST /v3/{project_id}/jobs/batch-sync-policy

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

   +-----------+-----------+-----------------------------------------------------------------------+-------------------------------------------------------------------+
   | Parameter | Mandatory | Type                                                                  | Description                                                       |
   +===========+===========+=======================================================================+===================================================================+
   | jobs      | Yes       | Array of :ref:`Table 4 <drs_03_0149__request_limitspeedreq>`\ objects | List of requests for setting synchronization policies in batches. |
   +-----------+-----------+-----------------------------------------------------------------------+-------------------------------------------------------------------+

.. _drs_03_0149__request_limitspeedreq:

.. table:: **Table 4** SyncPolicyReq

   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                              |
   +===================+=================+=================+==========================================================================+
   | job_id            | Yes             | String          | Task ID.                                                                 |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | conflict_policy   | No              | String          | Conflict policy.                                                         |
   |                   |                 |                 |                                                                          |
   |                   |                 |                 | Values:                                                                  |
   |                   |                 |                 |                                                                          |
   |                   |                 |                 | -  **ignore**: Ignore the conflict.                                      |
   |                   |                 |                 | -  **overwrite**: Overwrite the existing data with the conflicting data. |
   |                   |                 |                 | -  **stop**: Report an error.                                            |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | filter_ddl_policy | No              | String          | DDL filtering policy.                                                    |
   |                   |                 |                 |                                                                          |
   |                   |                 |                 | Value: **drop_database**                                                 |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | ddl_trans         | No              | Boolean         | Whether to synchronize DDL during incremental synchronization.           |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | index_trans       | No              | Boolean         | Whether to synchronize indexes during incremental synchronization.       |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+
   | slot_name         | No              | String          | Replication slot name.                                                   |
   +-------------------+-----------------+-----------------+--------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 5** Response body parameters

   +-----------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | Parameter | Type                                                                        | Description                                                               |
   +===========+=============================================================================+===========================================================================+
   | count     | Integer                                                                     | Total number.                                                             |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------+
   | results   | Array of :ref:`ModifyJobResp <drs_03_0149__response_modifyjobresp>` objects | List of returned synchronization policies that are configured in batches. |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------------------------------------+

.. _drs_03_0149__response_modifyjobresp:

.. table:: **Table 6** SyncPolicyResp

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | id                    | String                | Task ID.                                                                                          |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | status                | String                | Status Values:                                                                                    |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **success**: The task is successful.                                                           |
   |                       |                       | -  **failed**: The task fails.                                                                    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_msg             | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

The following is an example of configuring synchronization task policies in batches:

.. code-block::

   https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-sync-policy

.. code-block::

   {
       "jobs": [{
       "conflict_policy": "ignore",
       "ddl_trans": true,
       "filter_ddl_policy": "drop_database",
       "index_trans": true,
       "job_id": "19557d51-1ee6-4507-97a6-8f69164jb201"
       }]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "id" : "19557d51-1ee6-4507-97a6-8f69164jb201",
       "status" : "success"
     } ],
     "count" : 1
   }

Status Code
-----------

=========== ===========
Status Code Description
=========== ===========
200         OK
400         Bad Request
=========== ===========

Error Code
----------

For details, see :ref:`Error Code <drs_05_0004>`.
