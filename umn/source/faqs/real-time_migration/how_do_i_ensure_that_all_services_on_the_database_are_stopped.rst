:original_name: drs_04_0020.html

.. _drs_04_0020:

How Do I Ensure that All Services on the Database Are Stopped?
==============================================================

To ensure that all services on the database are stopped, perform the following steps:

#. Run the following statement on the source database to check whether active connections exist:

   .. code-block:: text

      show processlist;


   .. figure:: /_static/images/en-us_image_0000001391694041.png
      :alt: **Figure 1** Checking active connections

      **Figure 1** Checking active connections

#. **Optional:** If there are active connections, locate the service processes based on the values in the **Host** column in the command output and stop the service processes.

#. Run the following statement in the source database to check the binlog position. Then, record the two values in the **file** and **position** columns as **ckpt1**:

   .. code-block:: text

      show master status;


   .. figure:: /_static/images/en-us_image_0000001341414136.png
      :alt: **Figure 2** Viewing the binlog position

      **Figure 2** Viewing the binlog position

#. Wait for more than 30s. Run the following statement in the source database to check the binlog position again. Then, record the two values in the **file** and **position** columns as **ckpt2**. If **ckpt1** and **ckpt2** are equal, no data is written to the source database.

   .. code-block:: text

      show master status;
