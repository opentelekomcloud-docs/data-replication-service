:original_name: drs_11_0457.html

.. _drs_11_0457:

Data Synchronization Topologies
===============================

DRS real-time synchronization supports multiple topology types. You can plan the topology types as required. For details, see the following content.

.. note::

   To ensure data consistency, do not modify the synchronization objects in the destination database.

One-to-One Real-Time Synchronization
------------------------------------

|image1|

You can create a one-to-one synchronization task.

One-to-Many Real-Time Synchronization
-------------------------------------

|image2|

You need to create multiple synchronization tasks to implement one-to-many real-time synchronization. For example, to synchronize data from instance A to instances B, C, and D, you need to create three synchronization tasks.

Many-to-One Real-Time Synchronization
-------------------------------------

|image3|

You need to create multiple synchronization tasks to implement many-to-one real-time synchronization. For example, to synchronize data from instances B, C, and D to instance A, you need to create three synchronization tasks. Multiple tables can be synchronized to one table.

.. |image1| image:: /_static/images/en-us_image_0000001710629888.png
.. |image2| image:: /_static/images/en-us_image_0000001758549321.png
.. |image3| image:: /_static/images/en-us_image_0000001710470404.png
