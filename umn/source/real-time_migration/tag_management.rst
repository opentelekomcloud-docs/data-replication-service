:original_name: drs_online_tag.html

.. _drs_online_tag:

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

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** tab, click **Add Tag**. In the displayed dialog box, enter a tag key and value, and click **OK**.

   -  The tag key must be unique and must consist of 1 to 36 characters. Only letters, digits, hyphens (-), sign (@), and underscores (_) are allowed.
   -  The tag value can be empty or consist of 1 to 43 characters. Only letters, digits, hyphens (-), sign (@), and underscores (_) are allowed.
   -  The key of a tag cannot be **\_sys_enterprise_project_id**. **\_sys_enterprise_project_id** is a fixed tag of the enterprise project system and cannot be manually added.

#. After a tag has been added, you can view and manage it on the **Tags** page.

Editing a Tag
-------------

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** page, click **Add/Edit Tags**. In the displayed dialog box, modify the tag and click **OK**.

Delete a Tag
------------

#. On the **Online Migration Management** page, click the target migration task name in the **Task Name/ID** column.
#. On the **Basic Information** tab, click the **Tags** tab.
#. On the **Tags** page, locate the tag to be deleted and click **Delete** in the **Operation** column. In the displayed dialog box, click **Yes**.
#. After the tag is deleted, it will no longer be displayed on the **Tags** page.
