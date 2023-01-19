:original_name: drs_03_0123.html

.. _drs_03_0123:

Scenario 2: Querying Task Details in Batches
============================================

Scenarios
---------

This section describes how to query task details of a tenant by calling the API described in :ref:`Querying Task Details in Batches <drs_api_0151>`.

Procedure
---------

#. Obtain the ID of the task to be queried by referring to :ref:`Obtaining a Task ID <drs_api_0115>`.
#. URI format: /v3/{project_id}/jobs/batch-detail

   -  Example request:

      POST: https://{EndPoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-detail

      Obtain the endpoint from Regions and Endpoints.

   -  Request example:

      .. code-block:: text

         {
             "jobs": ["24834eb6-be30-464e-a299-f7aa730jb101", "140b5236-88ad-43c8-811c-1268453jb101"],
             "page_req": {
                 "cur_page": 1,
                 "per_page": 10
             }
         }

   -  Example Response:

      .. code-block:: text

         {
             "count": 2,
             "results": [{
                 "id": "24834eb6-be30-464e-a299-f7aa730jb101",
                 "name": "DRS-3999-lws",
                 "status": "STARTJOBING",
                 "description": "",
                 "create_time": "1608519469412",
                 "task_type": "FULL_INCR_TRANS",
                 "source_endpoint": {
                     "ip": "172.22.74.56",
                     "region": "eu-de",
                     "db_type": "mysql",
                     "db_port": 3306,
                     "ssl_link": false,
                     "project_id": "054ba152d480d55b2f5dc0069e7ddef0",
                     "db_user": "root"
                 },
                 "target_endpoint": {
                     "ip": "172.21.176.219",
                     "region": "eu-de",
                     "db_type": "mysql",
                     "db_port": 3306,
                     "ssl_link": false,
                     "inst_id": "3ef57dbcc8db478a9e346d26ef2575bfin01",
                     "project_id": "054ba152d480d55b2f5dc0069e7ddef0",
                     "inst_name": "rds-lws-target",
                     "db_user": "root",
                     "vpc_id": "0ff8df7b-f0e9-4b16-ac16-1db3dacb69e4",
                     "subnet_id": "f857d371-2f03-4622-85f6-2b7d42d0d82c"
                 },
                 "inst_info": {
                     "ip": "172.16.213.101",
                     "inst_type": "high",
                     "engine_type": "mysql",
                     "volume_size": 100,
                     "public_ip": "10.154.219.202",
                     "start_time": "0"
                 },
                 "actual_start_time": "1608520069393",
                 "update_time": "1608520068979",
                 "job_direction": "up",
                 "db_use_type": "migration",
                 "need_restart": false,
                 "is_target_readonly": true,
                 "speed_limit": [],
                 "schema_type": "Tungsten",
                 "object_switch": true,
                 "replace_definer": true,
                 "migrate_user": false,
                 "az_code": "az2xahz",
                 "vpc_id": "0ff8df7b-f0e9-4b16-ac16-1db3dacb69e4",
                 "subnet_id": "f857d371-2f03-4622-85f6-2b7d42d0d82c",
                 "security_group_id": "d90c971b-4b9d-402c-9c59-5c239389b8dd",
                 "issue_coupon": false,
                 "support_ip_v6": false
             }, {
                 "id": "140b5236-88ad-43c8-811c-1268453jb101",
                 "name": "DRS-0042-linxiaolu",
                 "status": "CONFIGURATION",
                 "description": "",
                 "create_time": "1608366204171",
                 "task_type": "FULL_INCR_TRANS",
                 "source_endpoint": {
                     "ip": "192.168.0.27",
                     "region": "eu-de",
                     "db_type": "mysql",
                     "db_port": 3306,
                     "ssl_link": false,
                     "project_id": "054ba152d480d55b2f5dc0069e7ddef0",
                     "db_user": "root"
                 },
                 "target_endpoint": {
                     "ip": "192.168.0.131",
                     "region": "eu-de",
                     "db_type": "mysql",
                     "db_port": 3306,
                     "ssl_link": false,
                     "inst_id": "e05a3679efe241d8b5dee80b17c1a863in01",
                     "project_id": "054ba152d480d55b2f5dc0069e7ddef0",
                     "inst_name": "rds-1417-lxl",
                     "db_user": "root",
                     "vpc_id": "65f0391c-0582-44a6-aa50-248f97ed82e1",
                     "subnet_id": "352ad828-3467-4f03-987a-c55a5a9dd417"
                 },
                 "inst_info": {
                     "ip": "192.168.0.229",
                     "status": "ACTIVE",
                     "inst_type": "high",
                     "engine_type": "mysql",
                     "volume_size": 100,
                     "public_ip": "10.154.219.72",
                     "start_time": "0"
                 },
                 "actual_start_time": "1608369232412",
                 "full_transfer_complete_time": "1608369510202",
                 "update_time": "1608517066434",
                 "job_direction": "up",
                 "db_use_type": "migration",
                 "need_restart": false,
                 "is_target_readonly": true,
                 "speed_limit": [],
                 "schema_type": "Tungsten",
                 "object_switch": false,
                 "replace_definer": true,
                 "migrate_user": false,
                 "az_code": "az2xahz",
                 "vpc_id": "65f0391c-0582-44a6-aa50-248f97ed82e1",
                 "subnet_id": "352ad828-3467-4f03-987a-c55a5a9dd417",
                 "security_group_id": "d90c971b-4b9d-402c-9c59-5c239389b8dd",
                 "issue_coupon": false,
                 "support_ip_v6": false
             }]
         }
