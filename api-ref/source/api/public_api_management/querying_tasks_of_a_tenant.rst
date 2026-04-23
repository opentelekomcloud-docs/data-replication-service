:original_name: drs_03_0138.html

.. _drs_03_0138:

Querying Tasks of a Tenant
==========================

Function
--------

This API is used to query tenant tasks by engine type, network type, task status, task name, or task ID.

URI
---

POST /v3/{project_id}/jobs

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

   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type                                                                   | Description                                                                                                                                                                          |
   +=======================+=================+========================================================================+======================================================================================================================================================================================+
   | cur_page              | Yes             | Integer                                                                | Current page. Set the value to **0** to obtain all items.                                                                                                                            |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | Default value: **1**                                                                                                                                                                 |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | per_page              | Yes             | Integer                                                                | Number of records on each page.                                                                                                                                                      |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | -  Default value: **10**                                                                                                                                                             |
   |                       |                 |                                                                        | -  Minimum value: **0**                                                                                                                                                              |
   |                       |                 |                                                                        | -  Maximum value: **100**                                                                                                                                                            |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | db_use_type           | Yes             | String                                                                 | Scenario. The value can be **migration** (real-time migration), **sync** (real-time synchronization), or **cloudDataGuard** (real-time disaster recovery).                           |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | Values:                                                                                                                                                                              |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | -  **migration**                                                                                                                                                                     |
   |                       |                 |                                                                        | -  **sync**                                                                                                                                                                          |
   |                       |                 |                                                                        | -  **cloudDataGuard**                                                                                                                                                                |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | engine_type           | No              | String                                                                 | Engine type of a DRS task.                                                                                                                                                           |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | Default value: **mysql**                                                                                                                                                             |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | Values:                                                                                                                                                                              |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | -  **mysql**: used for migration and synchronization from MySQL to MySQL                                                                                                             |
   |                       |                 |                                                                        | -  **mongodb**: used for migration from MongoDB to DDS                                                                                                                               |
   |                       |                 |                                                                        | -  **cloudDataGuard-mysql**: used for DR from MySQL to MySQL                                                                                                                         |
   |                       |                 |                                                                        | -  **mysql-to-taurus**: used for synchronization from MySQL to TaurusDB Cluster                                                                                                      |
   |                       |                 |                                                                        | -  **postgresql**: used for synchronization from PostgreSQL to PostgreSQL                                                                                                            |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | enterprise_project_id | No              | String                                                                 | Enterprise project. If no value is specified, this parameter is set to **null**. This parameter cannot be left blank. When enterprise project is enabled, this parameter can be set. |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name                  | No              | String                                                                 | Name or ID.                                                                                                                                                                          |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | net_type              | No              | String                                                                 | Network type. Values:                                                                                                                                                                |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | -  **vpn**                                                                                                                                                                           |
   |                       |                 |                                                                        | -  **vpc**                                                                                                                                                                           |
   |                       |                 |                                                                        | -  **eip**                                                                                                                                                                           |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | service_name          | No              | String                                                                 | Service name.                                                                                                                                                                        |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                | No              | String                                                                 | Status. Values:                                                                                                                                                                      |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CREATING**: The task is being created.                                                                                                                                             |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CREATE_FAILED**: The task fails to be created.                                                                                                                                     |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CONFIGURATION**: The task is being configured.                                                                                                                                     |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **STARTJOBING**: The task is being started.                                                                                                                                          |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **WAITING_FOR_START**: The task is waiting to be started.                                                                                                                            |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **START_JOB_FAILED**: The task failed to be started.                                                                                                                                 |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **FULL_TRANSFER_STARTED**: Full migration is in progress, and the DR scenario is initialized.                                                                                        |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **FULL_TRANSFER_FAILED**: Full migration failed. Initialization failed in the DR scenario.                                                                                           |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **FULL_TRANSFER_COMPLETE**: Full migration is complete, and the initialization is complete in the DR scenario.                                                                       |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **INCRE_TRANSFER_STARTED**: Incremental migration is being performed, and the DR task is in progress.                                                                                |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **INCRE_TRANSFER_FAILED**: Incremental migration fails and a DR exception occurs.                                                                                                    |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **RELEASE_RESOURCE_STARTED**: The task is being stopped.                                                                                                                             |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **RELEASE_RESOURCE_FAILED**: The task failed to be stopped.                                                                                                                          |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **RELEASE_RESOURCE_COMPLETE**: The task is stopped.                                                                                                                                  |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHANGE_JOB_STARTED**: The task is being changed.                                                                                                                                   |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHANGE_JOB_FAILED**: The task failed to be changed.                                                                                                                                |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHILD_TRANSFER_STARTING**: The subtask is being started.                                                                                                                           |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHILD_TRANSFER_STARTED**: The subtask is being migrated.                                                                                                                           |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHILD_TRANSFER_COMPLETE**: The subtask migration is complete.                                                                                                                      |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **CHILD_TRANSFER_FAILED**: The subtask failed to be migrated.                                                                                                                        |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **RELEASE_CHILD_TRANSFER_STARTED**: The subtask is being stopped.                                                                                                                    |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | **RELEASE_CHILD_TRANSFER_COMPLETE**: The subtask is complete.                                                                                                                        |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | Values:                                                                                                                                                                              |
   |                       |                 |                                                                        |                                                                                                                                                                                      |
   |                       |                 |                                                                        | -  **CREATING**                                                                                                                                                                      |
   |                       |                 |                                                                        | -  **CREATE_FAILED**                                                                                                                                                                 |
   |                       |                 |                                                                        | -  **CONFIGURATION**                                                                                                                                                                 |
   |                       |                 |                                                                        | -  **STARTJOBING**                                                                                                                                                                   |
   |                       |                 |                                                                        | -  **WAITING_FOR_START**                                                                                                                                                             |
   |                       |                 |                                                                        | -  **START_JOB_FAILED**                                                                                                                                                              |
   |                       |                 |                                                                        | -  **FULL_TRANSFER_STARTED**                                                                                                                                                         |
   |                       |                 |                                                                        | -  **FULL_TRANSFER_FAILED**                                                                                                                                                          |
   |                       |                 |                                                                        | -  **FULL_TRANSFER_COMPLETE**                                                                                                                                                        |
   |                       |                 |                                                                        | -  **INCRE_TRANSFER_STARTED**                                                                                                                                                        |
   |                       |                 |                                                                        | -  **INCRE_TRANSFER_FAILED**                                                                                                                                                         |
   |                       |                 |                                                                        | -  **RELEASE_RESOURCE_STARTED**                                                                                                                                                      |
   |                       |                 |                                                                        | -  **RELEASE_RESOURCE_FAILED**                                                                                                                                                       |
   |                       |                 |                                                                        | -  **RELEASE_RESOURCE_COMPLETE**                                                                                                                                                     |
   |                       |                 |                                                                        | -  **CHANGE_JOB_STARTED**                                                                                                                                                            |
   |                       |                 |                                                                        | -  **CHANGE_JOB_FAILED**                                                                                                                                                             |
   |                       |                 |                                                                        | -  **CHILD_TRANSFER_STARTING**                                                                                                                                                       |
   |                       |                 |                                                                        | -  **CHILD_TRANSFER_STARTED**                                                                                                                                                        |
   |                       |                 |                                                                        | -  **CHILD_TRANSFER_COMPLETE**                                                                                                                                                       |
   |                       |                 |                                                                        | -  **CHILD_TRANSFER_FAILED**                                                                                                                                                         |
   |                       |                 |                                                                        | -  **RELEASE_CHILD_TRANSFER_STARTED**                                                                                                                                                |
   |                       |                 |                                                                        | -  **RELEASE_CHILD_TRANSFER_COMPLETE**                                                                                                                                               |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tags                  | No              | Array of :ref:`ResourceTag <drs_03_0104__request_resourcetag>` objects | Tags.                                                                                                                                                                                |
   +-----------------------+-----------------+------------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 4** Response body parameters

   +--------------+-----------------------------------------------------------------+-----------------------+
   | Parameter    | Type                                                            | Description           |
   +==============+=================================================================+=======================+
   | total_record | Integer                                                         | Total number of tasks |
   +--------------+-----------------------------------------------------------------+-----------------------+
   | jobs         | Array of :ref:`JobInfo <drs_03_0138__response_jobinfo>` objects | Task details.         |
   +--------------+-----------------------------------------------------------------+-----------------------+

.. _drs_03_0138__response_jobinfo:

.. table:: **Table 5** JobInfo

   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                                                                            | Description                                                                                                       |
   +=======================+=================================================================================+===================================================================================================================+
   | id                    | String                                                                          | Task ID.                                                                                                          |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | name                  | String                                                                          | Task name.                                                                                                        |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | status                | String                                                                          | Task status. Values:                                                                                              |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **CREATING**: The task is being created.                                                                       |
   |                       |                                                                                 | -  **CREATE_FAILED**: The task fails to be created.                                                               |
   |                       |                                                                                 | -  **CONFIGURATION**: The task is being configured.                                                               |
   |                       |                                                                                 | -  **STARTJOBING**: The task is being started.                                                                    |
   |                       |                                                                                 | -  **WAITING_FOR_START**: The task is waiting to be started.                                                      |
   |                       |                                                                                 | -  **START_JOB_FAILED**: The task fails to be started.                                                            |
   |                       |                                                                                 | -  **FULL_TRANSFER_STARTED**: Full migration is in progress, and the DR scenario is initialized.                  |
   |                       |                                                                                 | -  **FULL_TRANSFER_FAILED**: Full migration failed. Initialization failed in the DR scenario.                     |
   |                       |                                                                                 | -  **FULL_TRANSFER_COMPLETE**: Full migration is complete, and the initialization is complete in the DR scenario. |
   |                       |                                                                                 | -  **INCRE_TRANSFER_STARTED**: Incremental migration is being performed, and the DR task is in progress.          |
   |                       |                                                                                 | -  **INCRE_TRANSFER_FAILED**: Incremental migration fails and a DR exception occurs.                              |
   |                       |                                                                                 | -  **RELEASE_RESOURCE_STARTED**: The task is being stopped.                                                       |
   |                       |                                                                                 | -  **RELEASE_RESOURCE_FAILED**: Stop task failed.                                                                 |
   |                       |                                                                                 | -  **RELEASE_RESOURCE_COMPLETE**: The task is stopped.                                                            |
   |                       |                                                                                 | -  **CHANGE_JOB_STARTED**: The task is being changed.                                                             |
   |                       |                                                                                 | -  **CHANGE_JOB_FAILED**: Change task failed.                                                                     |
   |                       |                                                                                 | -  **CHILD_TRANSFER_STARTING**: The subtask is being started.                                                     |
   |                       |                                                                                 | -  **CHILD_TRANSFER_STARTED**: The subtask is being migrated.                                                     |
   |                       |                                                                                 | -  **CHILD_TRANSFER_COMPLETE**: The subtask migration is complete.                                                |
   |                       |                                                                                 | -  **CHILD_TRANSFER_FAILED**: Migrate subtask failed.                                                             |
   |                       |                                                                                 | -  **RELEASE_CHILD_TRANSFER_STARTED**: The subtask is being stopped.                                              |
   |                       |                                                                                 | -  **RELEASE_CHILD_TRANSFER_COMPLETE**: The subtask is complete.                                                  |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | description           | String                                                                          | Task description.                                                                                                 |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | create_time           | String                                                                          | Time when a task is created                                                                                       |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | engine_type           | String                                                                          | Engine type of a DRS task. Values:                                                                                |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **mysql**: used for migration and synchronization from MySQL to MySQL                                          |
   |                       |                                                                                 | -  **mongodb**: used for migration from MongoDB to DDS                                                            |
   |                       |                                                                                 | -  **cloudDataGuard-mysql**: used for DR from MySQL to MySQL                                                      |
   |                       |                                                                                 | -  **mysql-to-taurus**: used for synchronization from MySQL to TaurusDB Cluster                                   |
   |                       |                                                                                 | -  **postgresql**: used for synchronization from PostgreSQL to PostgreSQL                                         |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | net_type              | String                                                                          | Network type. Values:                                                                                             |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **vpn**                                                                                                        |
   |                       |                                                                                 | -  **vpc**                                                                                                        |
   |                       |                                                                                 | -  **eip**                                                                                                        |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | billing_tag           | Boolean                                                                         | Billing tag.                                                                                                      |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | job_direction         | String                                                                          | Task direction. Values:                                                                                           |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **up**                                                                                                         |
   |                       |                                                                                 | -  **down**                                                                                                       |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | db_use_type           | String                                                                          | Task scenario. Values:                                                                                            |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **migration**: real-time migration.                                                                            |
   |                       |                                                                                 | -  **sync**: real-time synchronization.                                                                           |
   |                       |                                                                                 | -  **cloudDataGuard**: real-time disaster recovery.                                                               |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | task_type             | String                                                                          | Task mode. Values:                                                                                                |
   |                       |                                                                                 |                                                                                                                   |
   |                       |                                                                                 | -  **FULL_TRANS**: full migration                                                                                 |
   |                       |                                                                                 | -  **FULL_INCR_TRANS**: full+incremental migration                                                                |
   |                       |                                                                                 | -  **INCR_TRANS**: incremental migration                                                                          |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | children              | Array of :ref:`ChildrenJobInfo <drs_03_0138__response_childrenjobinfo>` objects | Subtask information body.                                                                                         |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
   | node_newFramework     | Boolean                                                                         | Whether the framework is a new framework.                                                                         |
   +-----------------------+---------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------+

.. _drs_03_0138__response_childrenjobinfo:

.. table:: **Table 6** ChildrenJobInfo

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                              |
   +=======================+=======================+==========================================================================================+
   | billing_tag           | Boolean               | Billing tag.                                                                             |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | create_time           | String                | Time when a task is created                                                              |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | db_use_type           | String                | Replication scenario. Values:                                                            |
   |                       |                       |                                                                                          |
   |                       |                       | -  **migration**: real-time migration.                                                   |
   |                       |                       | -  **sync**: real-time synchronization.                                                  |
   |                       |                       | -  **cloudDataGuard**: real-time disaster recovery.                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | description           | String                | Task description.                                                                        |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | engine_type           | String                | Engine type of a DRS task. Values:                                                       |
   |                       |                       |                                                                                          |
   |                       |                       | -  **mysql**: used for migration and synchronization from MySQL to MySQL                 |
   |                       |                       | -  **mongodb**: used for migration from MongoDB to DDS                                   |
   |                       |                       | -  **cloudDataGuard-mysql**: used for DR from MySQL to MySQL                             |
   |                       |                       | -  **mysql-to-taurus**: used for synchronization from MySQL to TaurusDB Cluster          |
   |                       |                       | -  **postgresql**: used for synchronization from PostgreSQL to PostgreSQL                |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | error_msg             | String                | Task failure cause.                                                                      |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | id                    | String                | Task ID.                                                                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | job_direction         | String                | Migration direction. Values:                                                             |
   |                       |                       |                                                                                          |
   |                       |                       | -  **up**: The current cloud is the standby cloud in the DR and to-the-cloud scenarios.  |
   |                       |                       | -  **down**: The current cloud is the active cloud in the DR and out-of-cloud scenarios. |
   |                       |                       | -  **non-dbs**: self-built databases.                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | name                  | String                | Task name.                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | net_type              | String                | Network type. Values:                                                                    |
   |                       |                       |                                                                                          |
   |                       |                       | -  **vpc**                                                                               |
   |                       |                       | -  **vpn**                                                                               |
   |                       |                       | -  **eip**                                                                               |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | node_newFramework     | Boolean               | New framework                                                                            |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | status                | String                | Task status.                                                                             |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+
   | task_type             | String                | Task mode. Values:                                                                       |
   |                       |                       |                                                                                          |
   |                       |                       | -  **FULL_TRANS**: full migration                                                        |
   |                       |                       | -  **FULL_INCR_TRANS**: full+incremental migration                                       |
   |                       |                       | -  **INCR_TRANS**: incremental migration                                                 |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------+

Example Request
---------------

-  Example of querying the real-time migration task list:

   .. code-block::

      https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs

   .. code-block::

      {
        "cur_page" : 1,
        "db_use_type" : "migration",
        "engine_type" : "",
        "name" : "",
        "net_type" : "",
        "per_page" : 5,
        "status" : ""
      }

Example Response
----------------

**Status code: 200**

OK

-  Example response for querying the real-time migration tasks:

   .. code-block::

      {
        "jobs" : [ {
          "id" : "24834eb6-be30-464e-a299-f7aa730jb101",
          "name" : "DRS-3999-lws",
          "status" : "INCRE_TRANSFER_FAILED",
          "description" : "",
          "create_time" : "2020-12-21 10:57:49",
          "error_msg" : "service LOGMANAGER failed, cause by: Unable to connect to DBMS: url=jdbc:mysql://172.22.74.56:3306?useUnicode=true&allowLoadLocalInfile=false&characterEncoding=UTF-8&connectTimeout=5000&useSSL=false&allowPublicKeyRetrieval=true&verifyServerCertificate=false&serverTimezone=UTC user=root",
          "engine_type" : "mysql",
          "net_type" : "eip",
          "billing_tag" : false,
          "job_direction" : "up",
          "db_use_type" : "migration",
          "task_type" : "FULL_INCR_TRANS",
          "node_newFramework" : false
        }, {
          "id" : "140b5236-88ad-43c8-811c-1268453jb101",
          "name" : "DRS-0042-linxiaolu",
          "status" : "CONFIGURATION",
          "description" : "",
          "create_time" : "2020-12-19 16:23:24",
          "engine_type" : "mysql",
          "net_type" : "eip",
          "billing_tag" : false,
          "job_direction" : "up",
          "db_use_type" : "migration",
          "task_type" : "FULL_INCR_TRANS",
          "node_newFramework" : false
        }, {
          "id" : "7f8e6f74-72d2-4ddd-bb8f-6c41397jb101",
          "name" : "DRS-0796",
          "status" : "RELEASE_RESOURCE_COMPLETE",
          "description" : "",
          "create_time" : "2020-12-18 10:48:11",
          "engine_type" : "mysql",
          "net_type" : "eip",
          "billing_tag" : false,
          "job_direction" : "non-dbs",
          "db_use_type" : "migration",
          "task_type" : "FULL_INCR_TRANS",
          "node_newFramework" : false
        }, {
          "id" : "14d88eeb-ee7e-4d30-a46e-a5ec8eajb101",
          "name" : "masj-mysql_migration_down-1",
          "status" : "INCRE_TRANSFER_STARTED",
      "description": "[using] api test 2\n1. This API is used to configure the source and destination database information. Before selecting a table, you must perform this operation. \n2. If the description of a task in the configuration is successfully modified, 202 success is returned. \n3. If the description of a task in an incremental migration fails to be modified, 202 failed DRS.M01504\nAnother operation is being performed on the migration task or the migration task is abnormal. Try again later./",
          "create_time" : "2020-12-15 15:43:02",
          "engine_type" : "mysql",
          "net_type" : "eip",
          "billing_tag" : true,
          "job_direction" : "down",
          "db_use_type" : "migration",
          "task_type" : "FULL_INCR_TRANS",
          "node_newFramework" : false
        }, {
          "id" : "d54691d2-f105-434d-a75d-809b017jb101",
          "name" : "masj-2-mysql_migration_down",
          "status" : "CONFIGURATION",
      "description": "[using] api test 2\n1. This API is used to configure the source and destination database information. Before selecting a table, you must perform this operation. \n2. If the description of a task in the configuration is successfully modified, 202 success is returned. \n3. If the description of a task in an incremental migration fails to be modified, 202 failed DRS.M01504\nAnother operation is being performed on the migration task or the migration task is abnormal. Try again later./",
          "create_time" : "2020-12-14 21:39:07",
          "engine_type" : "mysql",
          "net_type" : "eip",
          "billing_tag" : false,
          "job_direction" : "down",
          "db_use_type" : "migration",
          "task_type" : "FULL_INCR_TRANS",
          "node_newFramework" : false
        } ],
        "total_record" : 7
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
