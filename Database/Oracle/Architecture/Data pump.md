### Intro
Data pump contains utilitties for importing/exeporting data.   
Executing data pump jobs is listed in `DBA_DATAPUMP_JOBS` for all user and `USER_DATAPUMP_JOBS` for current user.
### Including:

1. Terminal command
   With expdp and impdp
```
expdp system/password@db10g full=Y directory=TEST_DIR dumpfile=DB10G.dmp logfile=expdpDB10G.log

impdp system/password@db10g full=Y directory=TEST_DIR dumpfile=DB10G.dmp logfile=impdpDB10G.log
```
2. PL/SQL API
   With DBMS_DATAPUMP
``` sql
DECLARE
  l_dp_handle       NUMBER;
BEGIN
  -- Open an schema export job.
  l_dp_handle := DBMS_DATAPUMP.open(
    operation   => 'EXPORT',
    job_mode    => 'SCHEMA',
    remote_link => NULL,
    job_name    => 'SCOTT_EXPORT',
    version     => 'LATEST');

  -- Specify the dump file name and directory object name.
  DBMS_DATAPUMP.add_file(
    handle    => l_dp_handle,
    filename  => 'SCOTT.dmp',
    directory => 'TEST_DIR');

  -- Specify the log file name and directory object name.
  DBMS_DATAPUMP.add_file(
    handle    => l_dp_handle,
    filename  => 'expdpSCOTT.log',
    directory => 'TEST_DIR',
    filetype  => DBMS_DATAPUMP.KU$_FILE_TYPE_LOG_FILE);

  -- Specify the schema to be exported.
  DBMS_DATAPUMP.metadata_filter(
    handle => l_dp_handle,
    name   => 'SCHEMA_EXPR',
    value  => '= ''SCOTT''');

  DBMS_DATAPUMP.start_job(l_dp_handle);
 
  -- To run job in background, another option would be waiting for the job
  DBMS_DATAPUMP.detach(l_dp_handle);
END;
/
```
### Features:
1. Table import/export
2. Schema import/export
3. Database import/export
4. Include/Exclude: by a pattern or a list
5. Netword import: import by a database link, not a file
6. Flashback export: all tables which is exported consistent to the same point in time. By default it is only consistent per table.  
