:original_name: drs_08_0012.html

.. _drs_08_0012:

Creating a User and Granting Permissions
========================================

This section describes IAM's fine-grained permissions management for DRS.

-  With IAM, you can:

   -  Create IAM users for employees based on the organizational structure of your enterprise. Each IAM user has their own security credentials, providing access to DRS resources.
   -  Grant only the permissions required for users to perform a specific task.
   -  Entrust an account or cloud service to perform professional and efficient O&M on your DRS resources.

If your account does not require individual IAM users, skip this chapter.

This section describes the procedure for granting permissions (see :ref:`Figure 1 <drs_08_0012__en-us_topic_0000001183831354_en-us_topic_0000001205509291_fig158351985619>`).

Prerequisites
-------------

Learn about the permissions (see :ref:`Permissions Management <drs_01_0201>`) supported by DRS and choose policies or roles according to your requirements.

Process Flow
------------

.. _drs_08_0012__en-us_topic_0000001183831354_en-us_topic_0000001205509291_fig158351985619:

.. figure:: /_static/images/en-us_image_0000001358599932.jpg
   :alt: **Figure 1** Process for granting DRS permissions

   **Figure 1** Process for granting DRS permissions

#. .. _drs_08_0012__en-us_topic_0000001183831354_en-us_topic_0000001205509291_li1658301914563:

   Create a user group and assign permissions to it.

   Create a user group on the IAM console, and assign the **DRS Administrator** policy to the group.

#. Create a user.

   Create a user on the IAM console and add the user to the group created in :ref:`1 <drs_08_0012__en-us_topic_0000001183831354_en-us_topic_0000001205509291_li1658301914563>`.

#. Log in and verify permissions.

   Log in to the management console using the newly created user, and verify that the user only has read permissions for DRS.

   Go to the DRS console, click **Create Migration Task** in the upper right corner to create a migration task. If a migration task (assume that there is only the **DRS Administrator** permission) is created, the **DRS Administrator** policy has taken effect.
