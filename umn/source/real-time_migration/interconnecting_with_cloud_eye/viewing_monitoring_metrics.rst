:original_name: drs_03_0108.html

.. _drs_03_0108:

Viewing Monitoring Metrics
==========================

Scenarios
---------

Cloud Eye monitors the running statuses of replication, synchronization, and DR instances. You can obtain the monitoring metrics on the management console. Monitored data requires a period of time for transmission and display. The status of the monitored object displayed on the Cloud Eye page is the status obtained 5 to 10 minutes before. You can view the monitored data of a newly created DB instance 5 to 10 minutes later.

Prerequisites
-------------

An instance is running properly when it is in the following statuses:

-  Real-time migration: **Full migration** and **Incremental migration**
-  Real-time synchronization: **Full synchronization** and **Incremental synchronization**
-  Real-time disaster recovery: **Disaster recovery in progress**

Viewing Metrics
---------------

#. Log in to the management console.

#. Click |image1| in the upper left corner and select a region and project.

#. Choose **Database** > **Data Replication Service**. The **Data Replication Service** page is displayed.

#. Take real-time migration as an example. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.

#. On the displayed page, click **View Metric** in the upper right corner of the page to go to the Cloud Eye console.

   By default, the monitoring information about the DRS instance is displayed on this page.

#. View monitoring metrics of the instance.

   -  On the Cloud Eye console, click the target DB instance name and click **Select Metric** in the upper right corner. In the displayed dialog box, you can select the metrics to be displayed and sort them by dragging them at desired locations.
   -  You can sort graphs by dragging them based on service requirements.
   -  Cloud Eye can monitor performance metrics from the last 1 hour, 3 hours, 12 hours, 1 day, 7 days, and 6 months.

.. |image1| image:: /_static/images/en-us_image_0000001710471068.png
