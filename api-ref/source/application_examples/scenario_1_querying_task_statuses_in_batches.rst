:original_name: drs_03_0122.html

.. _drs_03_0122:

Scenario 1: Querying Task Statuses in Batches
=============================================

Scenarios
---------

This section describes how to query the status of all tasks of a tenant by calling the API described in :ref:`Querying Task Statuses in Batches <drs_api_0150>`.

Procedure
---------

#. Obtain the ID of the task to be queried by referring to :ref:`Obtaining a Task ID <drs_api_0115>`.
#. URI format: /v3/{project_id}/jobs/batch-status

   -  Example request:

      POST: https://{endpoint}/v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-status

      Obtain the endpoint from Regions and Endpoints.

   -  Request example:

      .. code-block:: text

         {
             "jobs": ["9a470239-2308-4bb5-a6bc-1040402fjb21", "dc67695a-ee3e-49b8-a022-a099bd81jb21"],
             "pageReq": {
                 "cur_page": 1,
                 "per_page": 10
             }
         }

   -  Example Response:

      .. code-block:: text

         {
             "results": [{
                 "id": "9a470239-2308-4bb5-a6bc-1040402fjb21",
                 "status": "INCRE_TRANSFER_STARTED"
             }, {
                 "id": "dc67695a-ee3e-49b8-a022-a099bd81jb21",
                 "status": "INCRE_TRANSFER_FAILED"
             }],
             "count": 2
         }
