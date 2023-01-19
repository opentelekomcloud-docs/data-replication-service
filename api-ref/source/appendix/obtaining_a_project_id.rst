:original_name: drs_api_0106.html

.. _drs_api_0106:

Obtaining a Project ID
======================

Obtaining a Project ID from the Console
---------------------------------------

A project ID needs to be specified in the URLs of some APIs. Therefore, you need to obtain a project ID before calling such APIs. To do so, perform the following operations:

#. Sign up and log in to the management console.

#. Click the username and choose **My Credentials** from the drop-down list.

#. On the **API Credentials** page, view the project ID in the project list.

   If there are multiple projects in one region, expand **Region** and view subproject IDs in the **Project ID** column.

Obtaining the Project ID by Calling an API
------------------------------------------

You can also obtain the project ID by calling the API used to query project information based on the specified criteria.

The API used to obtain a project ID is **GET https://**\ *{Endpoint}*\ **/v3/projects/**, where *{Endpoint}* indicates the IAM endpoint. You can obtain the IAM endpoint from `Regions and Endpoints <https://docs.otc.t-systems.com/endpoint/index.html>`__. For details about API authentication, see :ref:`Authentication <drs_01_0005>`.

The following is an example response. The value of **id** is the project ID.

.. code-block::

   {
       "projects": [
           {
               "domain_id": "65382450e8f64ac0870cd180d14e684b",
               "is_domain": false,
               "parent_id": "65382450e8f64ac0870cd180d14e684b",
               "name": "eu-de",
               "description": "",
               "links": {
                   "next": null,
                   "previous": null,
                   "self": "https://www.example.com/v3/projects/a4a5d4098fb4474fa22cd05f897d6b99"
               },
               "id": "a4a5d4098fb4474fa22cd05f897d6b99",
               "enabled": true
           }
       ],
       "links": {
           "next": null,
           "previous": null,
           "self": "https://www.example.com/v3/projects"
       }
   }
