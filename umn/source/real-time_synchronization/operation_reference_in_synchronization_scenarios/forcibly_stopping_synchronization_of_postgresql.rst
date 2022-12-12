:original_name: drs_12_0009.html

.. _drs_12_0009:

Forcibly Stopping Synchronization of PostgreSQL
===============================================

This section describes how to clear the logical replication slot of the source database, how to synchronize sequence values, and how to reset the sequence values in the destination database when the source database cannot be connected after the PostgreSQL synchronization task is forcibly stopped.

Clearing the Logical Replication Slot of the Source Database
------------------------------------------------------------

#. Log in to the source database as the source database user used in the synchronization task.

#. .. _drs_12_0009__li54681355871:

   Query the name of the streaming replication slot of the database object selected in the synchronization task.

   .. code-block::

      select slot_name from pg_replication_slots where database = 'database';

   .. important::

      In the preceding command, *database* indicates the database selected in the synchronization task.

#. Run the following statement to delete the streaming replication slot:

   .. code-block::

      select * from pg_drop_replication_slot('slot_name');

   .. important::

      In the preceding command, *slot_name* indicates the name of the streaming replication slot queried in :ref:`2 <drs_12_0009__li54681355871>`.

#. Run the following statement to check whether the streaming replication slot is successfully deleted:

   .. code-block::

      select slot_name from pg_replication_slots where slot_name = 'slot_name';

   If the query result is empty, the streaming replication slot is deleted.

Synchronizing Sequence Values
-----------------------------

If sequence objects are not synchronized or the destination database is GaussDB(for openGauss), skip this section.

#. Use a high-privilege account (with the USAGE permission for all sequences) to connect to the source database and run the following statement:

   .. code-block::

      select 'SELECT pg_catalog.setval('||quote_literal(quote_ident(n.nspname)||'.'||quote_ident(c.relname))||', '||nextval(c.oid)||');' as sqls from pg_class c join pg_namespace n on c.relnamespace=n.oid where c.relkind = 'S' and n.nspname !~'^pg_' and n.nspname<>'information_schema' and not (c.relname='hwdrs_ddl_info_id_seq' and n.nspname='public') order by n.nspname, c.relname;

   The query result is the SQL statement that needs to be executed in the destination database.

#. Log in to the destination database as the destination database user used in the synchronization task and run the SQL statement queried in :ref:`1 <drs_12_0009__li772212346119>` in the destination database.

#. Run the following statement in the destination database to check the sequence value synchronization result:

   .. code-block::

      SELECT n.nspname, c.relname, nextval(c.oid) from pg_class c join pg_namespace n on c.relnamespace=n.oid where c.relkind = 'S' and n.nspname !~'^pg_' and n.nspname<>'information_schema' order by 1,2;

Resetting Sequence Values in the Destination Database
-----------------------------------------------------

If the source database failed and cannot be connected, you can reset the sequence values related to automatic increment or decrement columns in the destination database. If the source database can be connected, skip this section.

#. .. _drs_12_0009__li772212346119:

   Log in to the destination database as the destination database user used in the synchronization task.

#. .. _drs_12_0009__li872283414114:

   Run the following statement to query the SQL statement for resetting the sequence value corresponding to the sequence that uses nextval as the default value of the table column:

   .. code-block::

      set search_path to ''; select 'SELECT pg_catalog.setval('||quote_literal(quote_ident(s.sequence_schema)||'.'||quote_ident(s.sequence_name))||', (SELECT '||case when s.increment::int<0 then 'min(' else 'max(' end|| quote_ident(c.column_name)||')'||case when s.increment::int<0 then '-1' else '+1' end||' FROM '||quote_ident(c.table_schema)||'.'||quote_ident(c.table_name)||'));' as sqls from information_schema.columns c join information_schema.sequences s on (position(quote_literal (quote_ident(s.sequence_schema)||'.'||quote_ident(s.sequence_name))||'::regclass' in c.column_default) > 0) where c.data_type in ('bigint', 'int', 'integer', 'smallint', 'numeric', 'real', 'double precision', 'double') and c.column_default like 'nextval(%%' order by s.sequence_schema, s.sequence_name;

   The query result is the SQL statement that needs to be executed in the destination database.

#. .. _drs_12_0009__li672243411111:

   If the source database version is earlier than 10.0, skip this step. If the source database version is 10.0 or later, run the following statement in the destination database to query the SQL statement for resetting the sequence value corresponding to the additional column of the table identity column:

   .. code-block::

      set search_path to ''; select 'SELECT pg_catalog.setval('||quote_literal(seqname)||', (SELECT '||case when increment::int<0 then 'min(' else 'max(' end||colname||')'||case when increment::int<0 then '-1' else '+1' end||' FROM '||tablename||'));' as sqls from (select objid::regclass::text, refobjid::regclass::text, (pg_identify_object(refclassid,refobjid,refobjsubid)).identity, (pg_sequence_parameters(objid)).increment from pg_depend where deptype='i' and refobjsubid>0 and objid in (select c.oid from pg_class c join pg_namespace n on c.relnamespace=n.oid where c.relkind='S' and n.nspname !~ '^pg_' and n.nspname<>'information_schema')) p(seqname,tablename,colname,increment);

   The query result is the SQL statement that needs to be executed in the destination database.

#. Run the SQL statements queried in :ref:`2 <drs_12_0009__li872283414114>` and :ref:`3 <drs_12_0009__li672243411111>` in the destination database.

#. Run the following statement in the destination database to check the sequence value synchronization result:

   .. code-block::

      SELECT n.nspname, c.relname, nextval(c.oid) from pg_class c join pg_namespace n on c.relnamespace=n.oid where c.relkind = 'S' and n.nspname !~'^pg_' and n.nspname<>'information_schema' order by 1,2;
