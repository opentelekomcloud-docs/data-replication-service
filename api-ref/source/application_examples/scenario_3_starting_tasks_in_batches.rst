:original_name: drs_03_0124.html

.. _drs_03_0124:

Scenario 3: Starting Tasks in Batches
=====================================

Scenarios
---------

This section describes how to :ref:`start multiple configuration tasks <drs_03_0112>` by calling an API.

Procedure
---------

#. Obtain the ID of the task to be queried by referring to :ref:`Obtaining a Task ID <drs_api_0115>`.
#. URI format: /v3/{project_id}/jobs/batch-starting

   -  Example request:

      POST: https://{endpoint}/ /v3/054ba152d480d55b2f5dc0069e7ddef0/jobs/batch-starting

      Obtain the endpoint from Regions and Endpoints.

   -  Request example:

      .. code-block:: text

         {
             "jobs": [{
                 "job_id": "140b5236-88ad-43c8-811c-1268453jb101"
             }]
         }

   -  Example Response:

      .. code-block:: text

         {
             "count": 1,
             "results": [{
                 "id": "140b5236-88ad-43c8-811c-1268453jb101",
                 "status": "success"
             }]
         }
