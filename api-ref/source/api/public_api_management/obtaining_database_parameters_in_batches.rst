:original_name: drs_03_0141.html

.. _drs_03_0141:

Obtaining Database Parameters in Batches
========================================

Function
--------

To ensure that service applications are not affected after the migration, DRS provides parameter comparison to help you compare parameters between the source and destination databases. This API is used to obtain database parameters of the source and destination databases.

Constraints
-----------

-  Only MySQL migration and MySQL DR support parameter comparison. This API can be invoked only when **job_direction** is set to **up** and the task status is **CONFIGURATION**. The parent task cannot call this API in the dual-active DR scenario.
-  The value of **innodb_buffer_pool_size** is set to not exceed 70% of the total memory of the destination database. If you set a larger value for this parameter, the destination database startup may fail. To adjust the value to suit your services, view `Parameters for Comparison <https://docs.otc.t-systems.com/usermanual/drs/drs_08_0001.html>`__.

URI
---

POST /v3/{project_id}/jobs/batch-get-params

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

   +-----------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type             | Description                                                                                                                                                                                             |
   +===========+===========+==================+=========================================================================================================================================================================================================+
   | jobs      | Yes       | Array of strings | Request body for querying tasks in batches.                                                                                                                                                             |
   +-----------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | refresh   | Yes       | String           | Whether to obtain database parameters again. **1** indicates yes, and **0** indicates no (obtaining parameters from the cache). Set this parameter to **1** when this API is called for the first time. |
   +-----------+-----------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 202**

.. table:: **Table 4** Response body parameters

   +-------------+-------------------------------------------------------------------------------------+-------------------------------------------------+
   | Parameter   | Type                                                                                | Description                                     |
   +=============+=====================================================================================+=================================================+
   | params_list | Array of :ref:`QueryDbParamsResp <drs_03_0141__response_querydbparamsresp>` objects | Response body for querying database parameters. |
   +-------------+-------------------------------------------------------------------------------------+-------------------------------------------------+
   | count       | Integer                                                                             | Total number.                                   |
   +-------------+-------------------------------------------------------------------------------------+-------------------------------------------------+

.. _drs_03_0141__response_querydbparamsresp:

.. table:: **Table 5** QueryDbParamsResp

   +-----------+---------------------------------------------------------------+----------------------------------+
   | Parameter | Type                                                          | Description                      |
   +===========+===============================================================+==================================+
   | params    | Array of :ref:`params <drs_03_0141__response_params>` objects | Data parameter information body. |
   +-----------+---------------------------------------------------------------+----------------------------------+

.. _drs_03_0141__response_params:

.. table:: **Table 6** params

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                       |
   +=======================+=======================+===================================================================================================+
   | compare_result        | String                | Parameter comparison result. Values:                                                              |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **true**                                                                                       |
   |                       |                       | -  **false**                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | data_type             | String                | Type                                                                                              |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | group                 | String                | Metric Type Values:                                                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **common**: common parameter.                                                                  |
   |                       |                       | -  **performance**: performance parameter.                                                        |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | key                   | String                | Parameter name                                                                                    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | need_restart          | String                | Whether the instance needs to be restarted. Values:                                               |
   |                       |                       |                                                                                                   |
   |                       |                       | -  **true**                                                                                       |
   |                       |                       | -  **false**                                                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | source_value          | String                | Source database parameter value.                                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | target_value          | String                | Parameter value of the destination database.                                                      |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | value_range           | String                | Value Range                                                                                       |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_code            | String                | Error code, which is optional and indicates the returned information about the failure status.    |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+
   | error_message         | String                | Error message, which is optional and indicates the returned information about the failure status. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------+

Example Request
---------------

Example of the request body for obtaining database parameters in batches:

.. code-block::

   https://{EndPoint}/drs/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-get-params

.. code-block::

   {
     "jobs" : [ "140b5236-88ad-43c8-811c-1268453jb101" ],
     "refresh": 1
   }

Example Response
----------------

**Status code: 202**

Accepted

.. code-block::

   {
     "count" : 1,
     "params_list" : [ {
       "params" : [ {
         "group" : "performance",
         "key" : "binlog_cache_size",
         "source_value" : "16384",
         "target_value" : "32768",
         "compare_result" : "false",
         "data_type" : "figure",
         "value_range" : "4096-16777216",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "binlog_stmt_cache_size",
         "source_value" : "32768",
         "target_value" : "32768",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "4096-16777216",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "bulk_insert_buffer_size",
         "source_value" : "8388608",
         "target_value" : "8388608",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "0-18446744073709551615",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "character_set_server",
         "source_value" : "utf8",
         "target_value" : "utf8",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "utf8|latin1|gbk|utf8mb4",
         "need_restart" : "true"
       }, {
         "group" : "common",
         "key" : "collation_server",
         "source_value" : "utf8_general_ci",
         "target_value" : "utf8_general_ci",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "latin1_german1_ci|latin1_swedish_ci|latin1_danish_ci|latin1_german2_ci|latin1_bin|latin1_general_ci|latin1_general_cs|latin1_spanish_ci|gbk_chinese_ci|gbk_bin|utf8_general_ci|utf8_bin|utf8_unicode_ci|utf8_icelandic_ci|utf8_latvian_ci|utf8_romanian_ci|utf8_slovenian_ci|utf8_polish_ci|utf8_estonian_ci|utf8_spanish_ci|utf8_swedish_ci|utf8_turkish_ci|utf8_czech_ci|utf8_danish_ci|utf8_lithuanian_ci|utf8_slovak_ci|utf8_spanish2_ci|utf8_roman_ci|utf8_persian_ci|utf8_esperanto_ci|utf8_hungarian_ci|utf8_sinhala_ci|utf8mb4_general_ci|utf8mb4_bin|utf8mb4_unicode_ci|utf8mb4_icelandic_ci|utf8mb4_latvian_ci|utf8mb4_romanian_ci|utf8mb4_slovenian_ci|utf8mb4_polish_ci|utf8mb4_estonian_ci|utf8mb4_spanish_ci|utf8mb4_swedish_ci|utf8mb4_turkish_ci|utf8mb4_czech_ci|utf8mb4_danish_ci|utf8mb4_lithuanian_ci|utf8mb4_slovak_ci|utf8mb4_spanish2_ci|utf8mb4_roman_ci|utf8mb4_persian_ci|utf8mb4_esperanto_ci|utf8mb4_hungarian_ci|utf8mb4_sinhala_ci",
         "need_restart" : "true"
       }, {
         "group" : "common",
         "key" : "connect_timeout",
         "source_value" : "10",
         "target_value" : "10",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "2-31536000",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "explicit_defaults_for_timestamp",
         "source_value" : "OFF",
         "target_value" : "OFF",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "ON|OFF",
         "need_restart" : "true"
       }, {
         "group" : "performance",
         "key" : "innodb_buffer_pool_size",
         "source_value" : "536870912",
         "target_value" : "536870912",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "5242880-2147483648",
         "need_restart" : "true"
       }, {
         "group" : "common",
         "key" : "innodb_flush_log_at_trx_commit",
         "source_value" : "1",
         "target_value" : "1",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "0|1|2",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "innodb_lock_wait_timeout",
         "source_value" : "50",
         "target_value" : "50",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "1-1073741824",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "key_buffer_size",
         "source_value" : "16777216",
         "target_value" : "16777216",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "8-9223372036854771712",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "long_query_time",
         "source_value" : "1.000000",
         "target_value" : "1.000000",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "0.03-3600",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "max_connections",
         "source_value" : "800",
         "target_value" : "800",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "1-100000",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "net_read_timeout",
         "source_value" : "30",
         "target_value" : "30",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "1-31536000",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "net_write_timeout",
         "source_value" : "60",
         "target_value" : "60",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "1-31536000",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "read_buffer_size",
         "source_value" : "262144",
         "target_value" : "262144",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "8192-2147479552",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "read_rnd_buffer_size",
         "source_value" : "524288",
         "target_value" : "524288",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "1-2147483647",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "sort_buffer_size",
         "source_value" : "262144",
         "target_value" : "262144",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "32768-18446744073709551615",
         "need_restart" : "false"
       }, {
         "group" : "performance",
         "key" : "sync_binlog",
         "source_value" : "1",
         "target_value" : "1",
         "compare_result" : "true",
         "data_type" : "figure",
         "value_range" : "0-4294967295",
         "need_restart" : "false"
       }, {
         "group" : "common",
         "key" : "tx_isolation",
         "source_value" : "REPEATABLE-READ",
         "target_value" : "REPEATABLE-READ",
         "compare_result" : "true",
         "data_type" : null,
         "value_range" : "READ-UNCOMMITTED|READ-COMMITTED|REPEATABLE-READ|SERIALIZABLE",
         "need_restart" : "false"
       } ]
     } ]
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
