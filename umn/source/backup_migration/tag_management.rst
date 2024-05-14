:original_name: drs_backup_tag.html

.. _drs_backup_tag:

Tag Management
==============

Scenarios
---------

Tag Management Service (TMS) enables you to use tags on the management console to manage resources. TMS works with other cloud services to manage tags. TMS manages tags globally, and other cloud services manage their own tags. If you have to manage a large number of tasks, you can use different tags to identify and search for tasks.

-  You are advised to set predefined tags on the TMS console.
-  A tag consists of a key and value. You can add only one value for each key.
-  Each DB instance can have up to 20 tags.

Adding a Tag
------------

#. On the **Backup Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** tab, click **Add/Edit Tag**. In the displayed dialog box, enter a tag key and value, click **Add**, and click **OK**.

   -  The tag key cannot be empty and must be unique. It cannot start or end with a space or start with \_sys_. It can contain 1 to 128 characters, including letters, numbers, spaces, and the following characters: \_ . : = + - @.
   -  The tag value can be empty. It cannot start or end with a space and can contain 0 to 255 characters, including letters, numbers, spaces, and the following characters: \_ . : / = + - @.
   -  The key of a tag cannot be **\_sys_enterprise_project_id**. **\_sys_enterprise_project_id** is a fixed tag of the enterprise project system and cannot be manually added.

#. After a tag has been added, you can view and manage it on the **Tags** page.

Editing a Tag
-------------

#. On the **Backup Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** page, click **Add/Edit Tags**. In the displayed dialog box, modify the tag and click **OK**.

Delete a Tag
------------

#. On the **Backup Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** page, locate the tag to be deleted and click **Delete** in the **Operation** column. In the displayed dialog box, click **Yes**.
#. After the tag is deleted, it will no longer be displayed on the **Tags** page.
