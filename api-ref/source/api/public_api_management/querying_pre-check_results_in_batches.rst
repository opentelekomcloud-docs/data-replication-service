:original_name: drs_03_0111.html

.. _drs_03_0111:

Querying Pre-check Results in Batches
=====================================

Function
--------

This API is used to query the pre-check results of tasks in batches.

Constraints
-----------

-  This API can be called only when the task status is **CONFIGURATION** and the pre-check API is invoked.

URI
---

POST /v3/{project_id}/jobs/batch-precheck-result

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

   +-----------+-----------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type             | Description                                                                                                                                          |
   +===========+===========+==================+======================================================================================================================================================+
   | jobs      | Yes       | Array of strings | Request for querying pre-check results in batches. The value cannot be empty. The values must comply with the UUID rule. The task ID must be unique. |
   +-----------+-----------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +-----------+-------------------------------------------------------------------------------------+--------------------------------------------------------------+
   | Parameter | Type                                                                                | Description                                                  |
   +===========+=====================================================================================+==============================================================+
   | results   | Array of :ref:`QueryPreCheckResp <drs_03_0111__response_queryprecheckresp>` objects | Response body set for querying pre-check results in batches. |
   +-----------+-------------------------------------------------------------------------------------+--------------------------------------------------------------+
   | count     | Integer                                                                             | Total number of records.                                     |
   +-----------+-------------------------------------------------------------------------------------+--------------------------------------------------------------+

.. _drs_03_0111__response_queryprecheckresp:

.. table:: **Table 5** QueryPreCheckResp

   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                         | Description                                                                                                                                           |
   +=======================+==============================================================================+=======================================================================================================================================================+
   | precheck_id           | String                                                                       | ID of the task for querying the pre-check result.                                                                                                     |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | result                | Boolean                                                                      | Whether the pre-check items are passed. **true**: indicates that the pre-check is passed. The task can be started only after the pre-check is passed. |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | process               | String                                                                       | Pre-check progress, in percentage.                                                                                                                    |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | total_passed_rate     | String                                                                       | Percentage of passed pre-checks.                                                                                                                      |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rds_instance_id       | String                                                                       | RDS DB instance ID.                                                                                                                                   |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_direction         | String                                                                       | Task direction. Values:                                                                                                                               |
   |                       |                                                                              |                                                                                                                                                       |
   |                       |                                                                              | -  **up**: to-the-cloud scenarios and DR scenarios where the current cloud is the standby.                                                            |
   |                       |                                                                              | -  **down**: out-of-cloud scenarios and DR scenarios where the current cloud is the active.                                                           |
   |                       |                                                                              | -  **non-dbs**: self-built databases.                                                                                                                 |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | precheck_result       | Array of :ref:`PrecheckResult <drs_03_0111__response_precheckresult>` object | Pre-check results.                                                                                                                                    |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | error_msg             | String                                                                       | Error message, which is optional and indicates the returned information about the failure status.                                                     |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+
   | error_code            | String                                                                       | Error code, which is optional and indicates the returned information about the failure status.                                                        |
   +-----------------------+------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _drs_03_0111__response_precheckresult:

.. table:: **Table 6** PrecheckResult

   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | Parameter             | Type                                                                                      | Description                        |
   +=======================+===========================================================================================+====================================+
   | item                  | String                                                                                    | Check item.                        |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | result                | String                                                                                    | Check results. Values:             |
   |                       |                                                                                           |                                    |
   |                       |                                                                                           | -  **PASSED**                      |
   |                       |                                                                                           | -  **ALARM**                       |
   |                       |                                                                                           | -  **FAILED**                      |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | failed_reason         | String                                                                                    | Failure cause.                     |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | data                  | String                                                                                    | Encrypted data.                    |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | raw_error_msg         | String                                                                                    | Row error message.                 |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | group                 | String                                                                                    | Check item group.                  |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+
   | failed_sub_jobs       | Array of :ref:`PrecheckFailSubJobVO <drs_03_0111__response_precheckfailsubjobvo>` objects | Information about failed subtasks. |
   +-----------------------+-------------------------------------------------------------------------------------------+------------------------------------+

.. _drs_03_0111__response_precheckfailsubjobvo:

.. table:: **Table 7** PrecheckFailSubJobVO

   +--------------+--------+-----------------------------------------------------------+
   | Parameter    | Type   | Description                                               |
   +==============+========+===========================================================+
   | id           | String | ID of the subtask that fails to pass the pre-check.       |
   +--------------+--------+-----------------------------------------------------------+
   | name         | String | The name of the subtask that fails to pass the pre-check. |
   +--------------+--------+-----------------------------------------------------------+
   | check_result | String | Check results.                                            |
   +--------------+--------+-----------------------------------------------------------+

Example Request
---------------

-  Query the pre-check results of the DDS database real-time migration.

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-precheck-result

   .. code-block::

      {
        "jobs" : [ "a281f62f-4631-45d6-a2d3-679a9f4jb105" ]
      }

-  Query the pre-check results of the MySQL database real-time migration.

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-precheck-result

   .. code-block::

      {
        "jobs" : [ "140b5236-88ad-43c8-811c-1268453jb101" ]
      }

Example Response
----------------

**Status code: 200**

OK

-  Example response for querying the pre-check result during real-time MySQL migration:

   .. code-block::

      {
        "count" : 1,
        "results" : [ {
          "result" : true,
          "process" : "100%",
          "precheck_id" : "140b5236-88ad-43c8-811c-1268453jb101",
          "total_passed_rate" : "100%",
          "rds_instance_id" : "e05a3679efe241d8b5dee80b17c1a863in01",
          "job_direction" : "up",
          "precheck_result" : [ {
            "item" : "dstDbDiskSize",
            "result" : "PASSED",
            "data" : "{\"diskSizeTimes\":\"1.5\",\"dstVolumeSize\":\"37660000000\",\"srcIndexSize\":0,\"size\":\"0\",\"srcIndexAmount\":0}",
            "group" : "db_disk_size"
          }, {
            "item" : "checkIncreSrcDbExistedInDstDb",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbCharacterSetConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbClockConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbCollationServerConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbIsolationLevelConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbParamConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dbServerUuidConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dstMaxAllowedPacketCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "hasForeignKeyOnUnselectedTable",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "innodbStrictModeConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "isUserRequireSslLink",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "sqlModeConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "sqlModeNoEngine",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcBinlogFormatCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcBinlogRowImageCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbBinlogExpireLogsDays",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbBinlogIsOff",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbExistUnsupportEngineTable",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbIndexKeyLength",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbNameContainsUnsupportedSymbols",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbServerIdCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDstTableNameCaseSensitiveCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcHasNoPkTableWhenTgtHasInvisiblePk",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcRoutinesWithoutPrivilegeCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcTableNameContainsNonAscii",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcTriggerAndEventCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcViewNameContainsNonAscii",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srclogSlaveUpdatesCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "userRequirementIsEnoughForDefiner",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "userSelectObjectsCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dstStatusCheck",
            "result" : "PASSED",
            "data" : "",
            "group" : "db_target_status",
            "failed_reason" : ""
          }, {
            "item" : "dstDbPrivilegesIsEnough",
            "result" : "PASSED",
            "group" : "db_user_privilege"
          }, {
            "item" : "srcDbPrivilegesIsEnoughForIncre",
            "result" : "PASSED",
            "group" : "db_user_privilege"
          }, {
            "item" : "dbVersionMeetRequirement",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "dstDbVersionSupport",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "srcDbVersionSupport",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "dstDbConnection",
            "result" : "PASSED",
            "group" : "network"
          }, {
            "item" : "srcDbConnection",
            "result" : "PASSED",
            "group" : "network"
          } ]
        } ]
      }

-  Example response for querying the pre-check result during real-time DDS migration:

   .. code-block::

      {
        "count" : 1,
        "results" : [ {
          "result" : true,
          "process" : "100%",
          "precheck_id" : "a281f62f-4631-45d6-a2d3-679a9f4jb105",
          "total_passed_rate" : "100%",
          "rds_instance_id" : "3cadd5a0ef724f55ac7fa5bcb5f4fc5fin02",
          "job_direction" : "up",
          "precheck_result" : [ {
            "item" : "dstDbDiskSize",
            "result" : "PASSED",
            "data" : "{'size': '5263360', 'dstVolumeSize':'19089431762', 'diskSizeTimes':'1.5'}",
            "group" : "db_disk_size"
          }, {
            "item" : "srcAndDstCappedCollConsistency",
            "result" : "PASSED",
            "group" : "db_object_conflict_check"
          }, {
            "item" : "srcCollAlreadyExistedInDstColl",
            "result" : "PASSED",
            "group" : "db_object_conflict_check"
          }, {
            "item" : "srcViewAlreadyExistedInDstView",
            "result" : "PASSED",
            "group" : "db_object_conflict_check"
          }, {
            "item" : "rolesDependentCheck",
            "result" : "PASSED",
            "group" : "db_object_dependency_check"
          }, {
            "item" : "usersDependentCheck",
            "result" : "PASSED",
            "group" : "db_object_dependency_check"
          }, {
            "item" : "srcCollHasTtlIndex",
            "result" : "ALARM",
            "data" : "{\"srcHasTtlIndexColls\":\"fastunit.ttlsuoyin\"}",
            "group" : "db_params",
            "failed_reason" : "SRC_HAS_TTL_INDEXES"
          }, {
            "item" : "dbSslConsistency",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dstChunkNumCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "mongoTypeFitTransferMode",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcCollIndexNumCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcCollNameContainsUnsupportedSymbols",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbInstanceIsEmpty",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcDbNameContainsUnsupportedSymbols",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "srcIdIndexCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "userSelectObjectsCheck",
            "result" : "PASSED",
            "group" : "db_params"
          }, {
            "item" : "dstStatusCheck",
            "result" : "PASSED",
            "data" : "",
            "group" : "db_target_status",
            "failed_reason" : ""
          }, {
            "item" : "dstDbPrivilegesIsEnough",
            "result" : "PASSED",
            "group" : "db_user_privilege"
          }, {
            "item" : "srcDbPrivilegesIsEnough",
            "result" : "PASSED",
            "group" : "db_user_privilege"
          }, {
            "item" : "dbVersionMeetRequirement",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "dstDbVersionSupport",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "srcDbVersionSupport",
            "result" : "PASSED",
            "group" : "db_version"
          }, {
            "item" : "dstDbConnection",
            "result" : "PASSED",
            "group" : "network"
          }, {
            "item" : "srcDbConnection",
            "result" : "PASSED",
            "group" : "network"
          }, {
            "item" : "srcShardKeyConfiguration",
            "result" : "ALARM",
            "data" : "{\"notConfigShardIndexColls\":\"ycsb.usertable,mgo.mycollection7,mgo.mycollection9,mgo.mycollection5,mgo.mycollection4,mgo.mycollection3,mgo.mycollection,mgo.mycollection8,mgo.mycollection2,mgo.mycollection6,testdb3.testuk,testdb3.coll2,testdb3.coll6,testdb3.coll1,testdb3.Coll1,testdb3.testuk2,testdb3.coll5,testdb3.coll4,testdb1.coll6,testdb1.coll1,testdb1.testuk2,testdb1.coll2,testdb1.testuk,testdb1.coll5,testdb1.coll4,testdb1.Coll1,Testdb5.coll1,Testdb5.collx,Testdb5.Coll1,fastunit.gudingjihe,fastunit.geohaystack,fastunit.coll,fastunit.weiyisuoyin,fastunit.testSpecial\\\\u4E2D\\\\u6587~!@#%^&*()_+=-[]{};:?,`,fastunit.log,fastunit.twoD,fastunit.lianhesuoyin,fastunit.xishusuoyin,fastunit.quanwensuoyin,fastunit.ttlsuoyin,fastunit.putongsuoyin,fastunit.collcount,fastunit.shuzusuoyin,fastunit.twodsphere,fastunit.qiantaowendangsuoyin,fastunit.indexpartial\"}",
            "group" : "src_info_check",
            "failed_reason" : "SRC_INSTANCE_TYPE_IS_REPLICA_SET"
          }, {
            "item" : "checkBalanceStatus",
            "result" : "PASSED",
            "group" : "src_info_check"
          }, {
            "item" : "srcMongoInstanceType",
            "result" : "PASSED",
            "group" : "src_info_check"
          } ]
        } ]
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
