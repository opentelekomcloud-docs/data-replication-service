:original_name: drs_03_0088.html

.. _drs_03_0088:

Creating Triggers and Functions to Implement Incremental DDL Synchronization for PostgreSQL
===========================================================================================

This section describes how to perform real-time synchronization from PostgreSQL to RDS PostgreSQL. You can create triggers and functions in the source database to obtain the DDL information of the source database, and then synchronize DDL operations to the destination database during the incremental synchronization phase.

Prerequisites
-------------

-  The following DDL operations are supported:

   -  Table-level synchronization: TRUNCATE, DROP TABLE and ALTER TABLE (including ADD COLUMN, DROP COLUMN, ALTER COLUMN, RENAME COLUMN, ADD CONSTRAINT, DROP CONSTRAINT and RENAME)
   -  Database-level synchronization: TRUNCATE, CREATE SCHEMA/TABLE, DROP TABLE, ALTER TABLE (including ADD COLUMN, DROP COLUMN, ALTER COLUMN, RENAME COLUMN, ADD CONSTRAINT, DROP CONSTRAINT and RENAME), CREATE SEQUENCE, DROP SEQUENCE, ALTER SEQUENCE, CREATE INDEX, ALTER INDEX, DROP INDEX, CREATE VIEW, and ALTER VIEW

   .. caution::

      -  Table-level synchronization: If data is inserted into a renamed table, the data will not be synchronized to the destination database.
      -  Database-level synchronization: Tables that are created not using the CREATE TABLE statement in the source database will not be synchronized to the destination database. For example, you run CREATE TABLE AS to create a table or call a function to create a table.
      -  DDL statements starting with comments cannot be synchronized and are ignored.
      -  DDL statements executed in functions and stored procedures cannot be synchronized and are ignored.

-  If the source and destination databases are of different versions, use SQL statements that are compatible with both the source and destination databases to perform DDL operations. For example, if the source database is PostgreSQL 11 and the destination database is PostgreSQL 12, run the following statement to change the column type from char to int:

   .. code-block::

      alter table tablename alter column columnname type int USING columnname::int;

-  Check whether a table named **hwdrs_ddl_info**, a function named **hwdrs_ddl_function()**, and a trigger named **hwdrs_ddl_event** exist in the source database in public mode. If they exist, delete them.

-  During database-level synchronization, if a table without a primary key is created, run the following command to set the replication attribute of the table without a primary key to full.

   .. code-block::

      alter table tablename replica identity full;

Procedure
---------

.. note::

   If the source is an RDS for PostgreSQL instance on the current cloud, you can create related objects as user **root**. If the "Must be superuser to create an event trigger" error is reported, you can submit a service ticket. For details about permissions of user **root** of RDS for PostgreSQL on the current cloud, see Relational Database Service User Guide.

#. Connect to the database to be synchronized as a user who has permission to create event triggers.

#. .. _drs_03_0088__li1087504164812:

   Run the following statements to create a table for storing DDL information:

   .. code-block::

      DROP TABLE IF EXISTS public.hwdrs_ddl_info;
      DROP SEQUENCE IF EXISTS public.hwdrs_ddl_info_id_seq;
      CREATE TABLE public.hwdrs_ddl_info(
        id                             bigserial primary key,
        ddl                            text,
        username                       varchar(64) default current_user,
        txid                           varchar(16) default txid_current()::varchar(16),
        tag                            varchar(64),
        database                       varchar(64) default current_database(),
        schema                         varchar(64) default current_schema,
        client_address                 varchar(64) default inet_client_addr(),
        client_port                    integer default inet_client_port(),
        event_time                     timestamp default current_timestamp
      );

#. .. _drs_03_0088__li78731843114813:

   Run the following statements to create a function:

   .. code-block::

      CREATE OR REPLACE FUNCTION public.hwdrs_ddl_function()
          RETURNS event_trigger
          LANGUAGE plpgsql
          SECURITY INVOKER
      AS $BODY$
          declare ddl text;
          declare real_num int;
          declare max_num int := 50000;
      begin
        if (tg_tag in ('CREATE TABLE','ALTER TABLE','DROP TABLE','CREATE SCHEMA','CREATE SEQUENCE','ALTER SEQUENCE','DROP SEQUENCE','CREATE VIEW','ALTER VIEW','DROP VIEW','CREATE INDEX','ALTER INDEX','DROP INDEX')) then
            select current_query() into ddl;
            insert into public.hwdrs_ddl_info(ddl, username, txid, tag, database, schema, client_address, client_port, event_time)
            values (ddl, current_user, cast(txid_current() as varchar(16)), tg_tag, current_database(), current_schema,  inet_client_addr(), inet_client_port(), current_timestamp);
            select count(id) into real_num from public.hwdrs_ddl_info;
            if real_num > max_num then
              if current_setting('server_version_num')::int<100000 then
                delete from public.hwdrs_ddl_info where id<(select min(id)+1000 from public.hwdrs_ddl_info) and not exists (select 0 from pg_locks l join pg_database d on l.database=d.oid where d.datname=current_catalog and pid<>pg_backend_pid() and locktype='relation' and relation=to_regclass('public.hwdrs_ddl_info_pkey')::oid and mode='RowExclusiveLock');
              else
                delete from public.hwdrs_ddl_info where id<(select min(id)+1000 from public.hwdrs_ddl_info) and (xmax=0 or coalesce(txid_status(xmax::text::bigint), '')<>'in progress');
              end if;
            end if;
        end if;
      end;
      $BODY$;

#. Run the following statements to grant necessary permissions to the objects created in :ref:`2 <drs_03_0088__li1087504164812>` and :ref:`3 <drs_03_0088__li78731843114813>`:

   .. code-block::

      GRANT USAGE ON SCHEMA public TO public;
      GRANT SELECT,INSERT,DELETE ON TABLE public.hwdrs_ddl_info TO public;
      GRANT SELECT,USAGE ON SEQUENCE public.hwdrs_ddl_info_id_seq TO public;
      GRANT EXECUTE ON FUNCTION public.hwdrs_ddl_function() TO public;

#. Run the following statement to create a DDL event trigger:

   .. code-block::

      CREATE EVENT TRIGGER hwdrs_ddl_event ON ddl_command_end EXECUTE PROCEDURE public.hwdrs_ddl_function();

#. Run the following statement to set the created event trigger to enable:

   .. code-block::

      ALTER EVENT TRIGGER hwdrs_ddl_event ENABLE ALWAYS;

#. Return to the DRS console and create a PostgreSQL to RDS PostgreSQL synchronization task.

#. After the synchronization task is complete, run the following statements to delete the created tables, functions, and triggers.

   .. code-block::

      DROP EVENT trigger hwdrs_ddl_event;
      DROP FUNCTION public.hwdrs_ddl_function();
      DROP TABLE public.hwdrs_ddl_info;
