:original_name: en-us_topic_0000002701480753.html

.. _en-us_topic_0000002701480753:

Viewing and Downloading Logs
============================

Scenarios
---------

If you have enabled log reporting to LTS for a DRS task in :ref:`Log Reporting <en-us_topic_0000002701600831>`, you can analyze logs, search for logs, visualize logs, download logs, and view real-time logs on the LTS console.

Viewing Logs Reported to LTS
----------------------------

#. Log in to the management console.
#. Click |image1| in the upper left corner and select a region and project.
#. Choose **Management & Deployment** > **Log Tank Service** in the service list. The **Log Tank Service** page is displayed.
#. In the **Log Groups** area, locate a target log group and click its name.

   .. table:: **Table 1** Log field description

      +-----------------+--------+-------------------------------------------------------------------+
      | Name            | Type   | Description                                                       |
      +=================+========+===================================================================+
      | \_resource_id   | String | Resource ID. The value is fixed to **projectId** for DRS.         |
      +-----------------+--------+-------------------------------------------------------------------+
      | \_resource_name | String | Resource name. The value is fixed to **DRS**.                     |
      +-----------------+--------+-------------------------------------------------------------------+
      | \_service_type  | String | Service type. The value is fixed to **Data Replication Service**. |
      +-----------------+--------+-------------------------------------------------------------------+

Downloading Logs Reported to LTS
--------------------------------

#. Log in to the management console.
#. Click |image2| in the upper left corner and select a region and project.
#. Under **Management & Governance**, click **Log Tank Service**.
#. In the **Log Groups** area, locate a target log group and click its name.
#. Click **Download** on the right to download logs.

.. |image1| image:: /_static/images/en-us_image_0000002773114001.png
.. |image2| image:: /_static/images/en-us_image_0000002772994107.png
