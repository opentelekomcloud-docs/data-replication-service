:original_name: drs_03_0035.html

.. _drs_03_0035:

Processing Data
===============

DRS processes synchronized objects and allows you to add rules for selected objects. The processing rules supported by each data flow type are different.

Adding Additional Columns
-------------------------

#. On the **Processing Data** page, click **Additional Columns**, locate the table to be processed, and click **Add** in the **Operation** column.
#. In the displayed **Add** dialog box, specify the column name, operation type, and field type. Click **OK**.

   .. note::

      -  In many-to-one mapping scenarios, additional columns for data processing are required to avoid data conflicts.
      -  The following operation types are supported:

         -  **Default**: Use the default value to fill in the new column.
         -  Use the create_time column and update_time column as an example to fill the new column with the data creation time and data update time.
         -  **Expression**: indicates that you need to fill the new column with an expression.
         -  If you fill in the new column in **serverName@database@table** format, you need to enter a server name and then the database name and table name will be automatically filled in.
         -  **Value**: Select a value, for example, synchronization time.

      -  You can apply the additional column information of the first editable table to all editable tables in batches.
      -  During MySQL to GaussDB(for MySQL) primary/standby synchronization, if the number of columns in a single table exceeds 500, the number of additional columns added to the table may exceed the upper limit. As a result, the task fails.

#. Click **Next**.

Filtering Data
--------------

After a data filtering rule is added, update the source database to ensure data consistency. For example:

-  The filter criteria are met after the update. You need to continue the synchronization and perform the same update operation on the destination database. If no data is matched, the operation will be ignored, causing data inconsistency.
-  The filter criteria are not met after the update. You need to continue the synchronization and perform the same update operation on the destination database.

#. On the **Processing Data** page, set **Processing Type** to **Data filtering**.
#. In the **Object** area, select the table to be processed.
#. In the **Filtering Criteria** area, enter the filter criteria (only the part after WHERE in the SQL statement, for example, id=1), and click **Verify**.

   .. note::

      -  Each table has only one verification rule.
      -  Up to 500 tables can be filtered at a time.
      -  The filter expression cannot use the package, function, variable, or constant of a specific DB engine. It must comply with the general SQL standard. Enter the part following WHERE in the SQL statement (excluding WHERE and semicolons), for example, sid > 3 and sname like "G %". A maximum of 512 characters are allowed.
      -  In SQL statements for setting filter criteria, keywords must be enclosed in backquotes, and the value of **datatime** (including date and time) must be enclosed in single quotation marks, for example, \`update\` > '2022-07-13 00:00:00' and age >10.
      -  Filter criteria cannot be configured for large objects, such as CLOB, BLOB, and BYTEA.
      -  You are not advised to set filter criteria for fields of approximate numeric types, such as FLOAT, DECIMAL, and DOUBLE.
      -  Do not use fields containing special characters as a filter condition.
      -  You are not advised to use non-idempotent expressions or functions as data processing conditions, such as SYSTIMESTAMP and SYSDATE, because the returned result may be different each time the function is called.

#. After the verification is successful, click **Generate Processing Rule**. The rule is displayed.
#. Click **Next**.

Advanced Settings for Data Filtering
------------------------------------

If you need to query an association table, you can use the advanced settings of data processing.

#. On the **Processing Data** page, set **Processing Type** to **Data filtering**.

#. In the **Object** area, select the table to be processed.

#. .. _drs_03_0035__li86533923817:

   In the **Filtering Criteria** area, specify the filtering criteria, for example, id1 in (select id from db1.tab1 where id >=3 and id <10), and click **Verify**.

   .. note::

      -  Each table has only one verification rule.
      -  Up to 500 tables can be filtered at a time.
      -  The filter expression cannot use the package, function, variable, or constant of a specific DB engine. It must comply with the general SQL standard. Enter the part following WHERE in the SQL statement (excluding WHERE and semicolons), for example, sid > 3 and sname like "G %". A maximum of 512 characters are allowed.
      -  Filter criteria cannot be configured for large objects, such as CLOB, BLOB, and BYTEA.
      -  You are not advised to set filter criteria for fields of approximate numeric types, such as FLOAT, DECIMAL, and DOUBLE.
      -  Do not use fields containing special characters as a filter condition.
      -  You are not advised to use non-idempotent expressions or functions as data processing conditions, such as SYSTIMESTAMP and SYSDATE, because the returned result may be different each time the function is called.

#. After the verification is successful, click **Generate Processing Rule**. The rule is displayed.

#. .. _drs_03_0035__li12654292385:

   In the **Advanced Settings** area, specify the configuration condition and rule for the association table to help you filter data.

   a. In the **Configuration Condition** area, enter the association table information entered in :ref:`3 <drs_03_0035__li86533923817>`.

      **Database Name**, **Table Name**, **Column Name**, **Primary Key**, **Index**, and **Filter Criteria** are mandatory. If the table does not have an index, enter its primary key.

      **Filter Criteria** is the filter condition of the association table information entered in :ref:`3 <drs_03_0035__li86533923817>`.

   b. Then, click **Verify**.

   c. After the verification is successful, click **Generate Configuration Rule**. The rule is displayed in the **Configuration Rule** area.

      To filter data in multiple association tables, repeat :ref:`5 <drs_03_0035__li12654292385>`.

      .. note::

         Configuration rules can be deleted.

#. Click **Next**.

Processing Columns
------------------

#. On the **Process Data** page, select **Processing Columns**.
#. In the **Object** area, select the objects to be processed.
#. Click **Edit** to the right of the selected object.
#. In the **Edit Column** dialog box, select the columns to be mapped and enter new column names.

   .. note::

      -  You can query or filter columns or create new column names.
      -  After the column name is edited, the column name of the destination database is changed to the new name.
      -  The new column name cannot be the same as the original column name or an existing column name.
      -  The column name in the synchronized table cannot be modified.
      -  Only the selected columns can be synchronized.
      -  MySQL to MySQL and MySQL to GaussDB(for MySQL) primary/standby synchronizations do not support column mapping based on the partitioning column of a partitioned table.

#. Click **Confirm**.
#. Click **Next**.

Viewing Data Filtering Results
------------------------------

#. In the task list, click the task to be processed.
#. Click the **Process Data** tab to view data filtering records. Click |image1| in the upper right corner to refresh the record list.

View Column Processing
----------------------

#. On the task management page, click the target task name in the **Task Name/ID** column.
#. In the navigation pane on the left, choose **Synchronization Mapping**. In the upper right corner, and select **Columns** to view column mapping records. Click |image2| in the upper right corner to refresh the record list.

.. |image1| image:: /_static/images/en-us_image_0000001341254064.png
.. |image2| image:: /_static/images/en-us_image_0000001391773837.png
