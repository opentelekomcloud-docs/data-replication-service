:original_name: drs_03_0130.html

.. _drs_03_0130:

Setting Flow Control for Tasks
==============================

Function
--------

This API is used to enable or disable flow control for tasks. By default, the migration speed is not limited after a task is created.

-  You can customize the maximum migration speed.
-  If the migration speed is not limited, the outbound bandwidth of the source database is maximally used, which causes read consumption on the source database accordingly. For example, if the outbound bandwidth of the source database is 100 MB/s and 80% bandwidth is used, the I/O consumption on the source database is 80 MB/s.

Constraints
-----------

-  You can set the time range based on your service requirements. Flow can be controlled all day or during specific time ranges. The default value is **All day**.
-  A maximum of three time ranges can be set, and they cannot overlap.
-  The start time cannot be the same as the end time.
-  If the start time is 16:00 and the end time is 15:59, the bandwidth is limited for the whole day.
-  If **speed_limit** is set to **[]**, the speed is not limited.
-  The minute in the start time is ignored. The end time must be ended with 59. For example, 03:59 is equivalent to 04:00 (UTC) and the hour is a two-digit number.
-  In the dual-active DR scenario, the parent task cannot call the API.
-  This API cannot be used when the task mode is **INCR_TRANS**.

URI
---

PUT /v3/{project_id}/jobs/batch-limit-speed

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

   +--------------+-----------+----------------------------------------------------------------------------+--------------------+
   | Parameter    | Mandatory | Type                                                                       | Description        |
   +==============+===========+============================================================================+====================+
   | speed_limits | Yes       | Array of :ref:`LimitSpeedReq <drs_03_0130__request_limitspeedreq>` objects | Speed limit in DR. |
   +--------------+-----------+----------------------------------------------------------------------------+--------------------+

.. _drs_03_0130__request_limitspeedreq:

.. table:: **Table 4** LimitSpeedReq

   +-------------+-----------+------------------------------------------------------------------------------+-------------------------------------------+
   | Parameter   | Mandatory | Type                                                                         | Description                               |
   +=============+===========+==============================================================================+===========================================+
   | job_id      | Yes       | String                                                                       | Task ID.                                  |
   +-------------+-----------+------------------------------------------------------------------------------+-------------------------------------------+
   | speed_limit | Yes       | Array of :ref:`SpeedLimitInfo <drs_03_0130__request_speedlimitinfo>` objects | Request body of flow control information. |
   +-------------+-----------+------------------------------------------------------------------------------+-------------------------------------------+

.. _drs_03_0130__request_speedlimitinfo:

.. table:: **Table 5** SpeedLimitInfo

   +-----------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type    | Description                                                                                                                                                    |
   +===========+===========+=========+================================================================================================================================================================+
   | begin     | Yes       | String  | Start time (UTC) of flow control. The start time is an integer in hh:mm format and the minutes part is ignored. **hh** indicates the hour, for example, 01:00. |
   +-----------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end       | Yes       | String  | End time (UTC) in the format of hh:mm, for example, 15:59. The value must end with 59.                                                                         |
   +-----------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | speed     | Yes       | String  | Speed. The value ranges from 1 to 9,999, in MB/s.                                                                                                              |
   +-----------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_utc    | No        | Boolean | Whether the UTC time is used.                                                                                                                                  |
   +-----------+-----------+---------+----------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 6** Response body parameters

   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | Parameter | Type                                                                        | Description                                 |
   +===========+=============================================================================+=============================================+
   | count     | Integer                                                                     | Total number.                               |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+
   | results   | Array of :ref:`ModifyJobResp <drs_03_0130__response_modifyjobresp>` objects | List of tasks that are modified in batches. |
   +-----------+-----------------------------------------------------------------------------+---------------------------------------------+

.. _drs_03_0130__response_modifyjobresp:

.. table:: **Table 7** ModifyJobResp

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

Example of setting flow control for DR tasks in batches:

.. code-block::

   https://{Endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-limit-speed

.. code-block::

   {
     "speed_limits" : [ {
       "job_id" : "7d0504f1-aba3-435f-914f-936b861jb502",
       "speed_limit" : [ {
         "begin" : "16:00",
         "end" : "15:59",
         "speed" : "15"
       } ]
     } ]
   }

Example Response
----------------

**Status code: 200**

OK

.. code-block::

   {
     "results" : [ {
       "id" : "efa2bd29-8780-494f-a2ee-188b003ejb11",
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
