:original_name: drs_04_0458.html

.. _drs_04_0458:

Manual Configuration
====================

Scenarios
---------

After data is migrated from the local host or VMs to the RDS SQL Server DB instance on the current cloud through DRS, the Login accounts, DBLink, AgentJobs, and key configurations of the source database also need to be synchronized to the destination database.

Login Account
-------------

Login account is an instance-level account of Microsoft SQL Server and is used to manage user server and database permissions. Generally, a user has multiple such accounts. After the user is migrated to the RDS SQL Server DB instance, you need to manually create corresponding Login accounts on the DB instance. The following describes how to create a Login account with the same name and password as those of your local Login account on the RDS SQL Server DB instance and grant permissions to the account.

#. .. _drs_04_0458__en-us_topic_0000001205509265_en-us_topic_0176256301_li165582910512:

   Execute the following script to obtain the script for creating a Local account on your local instance. The obtained script can be directly executed on the destination DB instance to create a Login account with the same name and password.

   .. code-block:: text

      SELECT 'IF (SUSER_ID('+QUOTENAME(SP.name,'''')+') IS NULL) BEGIN CREATE LOGIN ' +QUOTENAME(SP.name)+
      CASE
      WHEN SP.type_desc = 'SQL_LOGIN' THEN ' WITH PASSWORD = ' +CONVERT(NVARCHAR(MAX),SL.password_hash,1)+ ' HASHED,SID=' +CONVERT(NVARCHAR(MAX),SP.SID,1)+',CHECK_EXPIRATION = '
      + CASE WHEN SL.is_expiration_checked = 1 THEN 'ON' ELSE 'OFF' END +', CHECK_POLICY = ' +CASE WHEN SL.is_policy_checked = 1 THEN 'ON,' ELSE 'OFF,' END
      ELSE ' FROM WINDOWS WITH'
      END
      +' DEFAULT_DATABASE=[' +SP.default_database_name+ '], DEFAULT_LANGUAGE=[' +SP.default_language_name+ '] END;' as CreateLogin
      FROM sys.server_principals AS SP LEFT JOIN sys.sql_logins AS SL
      ON SP.principal_id = SL.principal_id
      WHERE SP.type ='S'
      AND SP.name NOT LIKE '##%##'
      AND SP.name NOT LIKE 'NT AUTHORITY%'
      AND SP.name NOT LIKE 'NT SERVICE%'
      AND SP.name NOT IN ('rdsadmin','rdsbackup','rdsuser','rdsmirror','public')

#. .. _drs_04_0458__en-us_topic_0000001205509265_en-us_topic_0176256301_li189242430518:

   Execute the script in :ref:`1 <drs_04_0458__en-us_topic_0000001205509265_en-us_topic_0176256301_li165582910512>`:


   .. figure:: /_static/images/en-us_image_0000001391854125.jpg
      :alt: **Figure 1** Obtaining the script

      **Figure 1** Obtaining the script

#. Copy and execute the script obtain in :ref:`2 <drs_04_0458__en-us_topic_0000001205509265_en-us_topic_0176256301_li189242430518>` on the destination instance. The created Login account is the same as the original one.

#. Map the newly created Login account to the database user permissions that have been migrated to the RDS SQL Server DB instance to ensure permission consistency.

   .. code-block:: text

      declare @DBName nvarchar(200)
      declare @Login_name nvarchar(200)
      declare @SQL nvarchar(MAX)
      set @Login_name = 'TestLogin7' //Enter the login name one by one.
      declare DBName_Cursor cursor for
      select quotename(name)from sys.databases where  database_id > 4 and state = 0
      and name not like '%$%'
      and name <> 'rdsadmin'
      open DBName_Cursor
      fetch next from DBName_Cursor into @DBName
      WHILE @@FETCH_STATUS= 0
      begin
      SET @SQL='    USE '+ (@DBName)+ '
      if exists(select top 1 1 from sys.sysusers where name = '''+ @Login_Name +''')
      begin
      ALTER USER '+@Login_name+' with login = '+@Login_name+';
      end
      '
      print @SQL
      EXEC (@SQL)
      fetch next from DBName_Cursor into @DBName
      end
      close DBName_Cursor
      deallocate DBName_Cursor

   .. note::

      After the preceding script is executed, you can view the Login account with the same name on the new instance, and the password and permission are the same as those on your local host.

Database Link
-------------

SQL Server allows you to create database links to interact with databases on external DB instances. Therefore you can query, synchronize, and compare databases of different types or on different DB instances. However, these links cannot be automatically synchronized to the DB instance on cloud so you need to synchronize them manually.

#. Connect the local DB instance and cloud DB instance through Microsoft SQL Server Management Studio. Choose **Server Objects** > **Linked Servers** and locate the DBLink of the current DB instance.


   .. figure:: /_static/images/en-us_image_0000001391773997.jpg
      :alt: **Figure 2** Viewing database links

      **Figure 2** Viewing database links

#. Select the linked server and press **F7**. The **Object Explore** page is displayed. On this page, you can quickly create a script.


   .. figure:: /_static/images/en-us_image_0000001341094552.jpg
      :alt: **Figure 3** Creating the script

      **Figure 3** Creating the script

#. In the displayed window, view all the scripts for creating DBLinks of the current DB instance. You only need to copy the scripts to the destination DB instance and change the password on @rmtpassword.

   .. code-block:: text

      USE [master]
      GO

      /****** Object:  LinkedServer [DRS_TEST_REMOTE]    Script Date: 2019/5/25 17:51:50 ******/
      EXEC master.dbo.sp_addlinkedserver @server = N'DRS_TEST_REMOTE', @srvproduct=N'', @provider=N'SQLNCLI', @datasrc=N'DESKTOP-B18JH5T\SQLSERVER2016EE'
      /* For security reasons the linked server remote logins password is changed with ######## */
      EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'DRS_TEST_REMOTE',@useself=N'False',@locallogin=NULL,@rmtuser=N'sa',@rmtpassword='########'
      GO

   .. note::

      The preceding script is an example. The created script may contain a large number of default system configuration items. You need to retain only the following two key scripts for each DBLink. In addition, you need to enter the account and password again.

Agent JOB
---------

Agent Job is the agent service of Microsoft SQL Server. It helps you quickly create scheduled tasks on DB instances, perform routine O&M, and process data. You need to manually migrate local Job scripts.

#. Connect the local DB instance and cloud DB instance through Microsoft SQL Server Management Studio. Choose **SQL Server Agent** > **Jobs** and locate all the jobs of the current DB instance.


   .. figure:: /_static/images/en-us_image_0000001341254212.jpg
      :alt: **Figure 4** Viewing Jobs

      **Figure 4** Viewing Jobs

#. Select a job and press **F7**. All jobs are displayed on the **Object Explore** page. Select all jobs and create a script in the new window.


   .. figure:: /_static/images/en-us_image_0000001341574092.jpg
      :alt: **Figure 5** Creating a script

      **Figure 5** Creating a script

#. Copy the T-SQL script in the new window to the new DB instance, and then modify the following key items to ensure that the creation is successful.

   -  Modify the owner account of each job.

      Example:

      @owner_login_name=N'rdsuser'

   -  Modify the DB instance name of each job.

      Example:

      @server=N' DB instance IP address'

      @server_name = N'DB instance IP address'

   .. note::

      The owner account of the new job is very important. On the RDS SQL Server DB instance, only the owner of the job can view the job of the DB instance. Therefore, it is recommended that all job owners use the same account to facilitate job management.

Key Configuration
-----------------

After the database is restored to the RDS SQL Server DB instance, some local important configuration items need to be synchronized to keep service running properly.

#. tempdb: The file configuration of the temporary database needs to be synchronized.

   It is recommended that you set 8 temporary files and ensure that the files are stored in **D:\\RDSDBDATA\\Temp\\**.

   Run the following script on the destination database to add the temporary database file configuration:

   .. code-block:: text

      USE [master]
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb1', FILENAME = N'D:\RDSDBDATA\Temp\tempdb1.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb2', FILENAME = N'D:\RDSDBDATA\Temp\tempdb2.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb3', FILENAME = N'D:\RDSDBDATA\Temp\tempdb3.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb4', FILENAME = N'D:\RDSDBDATA\Temp\tempdb4.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb5', FILENAME = N'D:\RDSDBDATA\Temp\tempdb5.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb6', FILENAME = N'D:\RDSDBDATA\Temp\tempdb6.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO
      ALTER DATABASE [tempdb] ADD FILE ( NAME = N'tempdb7', FILENAME = N'D:\RDSDBDATA\Temp\tempdb7.ndf' , SIZE = 65536KB , FILEGROWTH = 65536KB )
      GO


   .. figure:: /_static/images/en-us_image_0000001391694017.jpg
      :alt: **Figure 6** Checking temporary files

      **Figure 6** Checking temporary files

#. Database isolation level: Check whether the database isolation level is enabled on the source DB instance and synchronize the isolation level to the RDS SQL Server DB instance. There are two snapshot isolation parameters:

   -  Is Read Committed Snapshot On
   -  Allow Snapshot Isolation

   If the database isolation level of the source DB instance is enabled, you can run the following script on the destination database to enable the database isolation level:

   .. code-block:: text

      USE [DBName]
      GO
      ALTER DATABASE [DBName] SET READ_COMMITTED_SNAPSHOT ON WITH NO_WAIT
      GO
      ALTER DATABASE [DBName] SET ALLOW_SNAPSHOT_ISOLATION ON
      GO

#. Max Degree of Parallelism: The maximum degree of parallelism is set to **0** by default on the RDS SQL Server instance. You can also set the value based on the local settings to avoid exceptions in different service scenarios.

   In **Object Explorer**, right-click a local server and select **Properties**. Click the **Advanced** node. In the **Max Degree of Parallelism** box, view the value of the local instance and change the **max degree of parallelism** value in the parameter group of the destination RDS SQL Server instance to the same.


   .. figure:: /_static/images/en-us_image_0000001391534445.jpg
      :alt: **Figure 7** Max Degree of Parallelism

      **Figure 7** Max Degree of Parallelism

   Log in to the RDS console. On the **Instance Management** page, click the target DB instance name. Choose **Parameters**, search for the **max degree of parallelism** parameter, and change its value.


   .. figure:: /_static/images/en-us_image_0000001341414112.png
      :alt: **Figure 8** max degree of parallelism

      **Figure 8** max degree of parallelism

#. Check whether the database recovery model on the cloud is set to **Full**. If not, change the mode.

   Right-click the database and choose **Properties** from the shortcut menu. In the displayed page, select **Options**. Then, verify that **Recovery Model** is set to **Full**. Ensure that the database is highly available and the backup policy is executable.


   .. figure:: /_static/images/en-us_image_0000001391854129.png
      :alt: **Figure 9** Checking the database recovery model

      **Figure 9** Checking the database recovery model
