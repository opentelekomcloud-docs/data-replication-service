:original_name: drs_10_0402.html

.. _drs_10_0402:

Importing Synchronization Objects
=================================

Real-time synchronization supports the import of objects through files. After a task is created, you can import object files on the **Set Synchronization Task** page.

.. note::

   -  Only Windows Microsoft Excel 97-2003 (``*``.xls), 2007, and later (``*``.xlsx) files can be imported. The downloaded compressed package provides the templates of the two versions.
   -  The file name can contain only spaces, letters, digits, hyphens (-), underscores (_), and parentheses.
   -  The format of the object information in the template must meet the requirements. The value is case-sensitive and cannot include angle brackets (<>), periods (.), and double quotation marks ("). Objects that start or end with a space are not supported.
   -  The task in the configuration supports table-level synchronization, database-level synchronization, or file import mode. Each time you switch to a new mode, the selected or imported database objects are cleared, and you need to select or import them again.
   -  If you want to import a file for mapping, fill in the first and second columns of the file based on the template. If the first two columns of a row are left blank, the row will be ignored.
   -  For the task created using the file import mode, database-level and table-level synchronization are not supported after the task is started.
   -  If you edit a task, the imported file must contain information about all objects. Importing only the updated objects is not allowed.
   -  If you edit a task again, the objects that have been synchronized cannot be mapped again. Ensure that the object names remain unchanged after the mapping.
   -  If you edit a task again, the exported object information is the synchronized object information.
   -  If the verification fails after the file is uploaded, click **View Failure Details** to download the error information.
   -  The object names entered in the Excel file must use the same letter case as the source object names.

Procedure
---------

#. On the **Set Synchronization Task** page, click **Import object file** in the **Synchronization Object** field.
#. Click **Download Template**.
#. Download the template and enter information about the objects to be imported.
#. Click **Select File**. In the displayed dialog box, select the edited template.
#. Click **Upload**.
