Oracle-AI-Database-26ai-Free-on-Docker
======================================

A set of scripts for using Oracle AI Database 26ai Free Container Image in [Oracle Container Registry](https://container-registry.oracle.com/ords/ocr/ba/database/free).

Configuration
-------------

Copy the file `dotenv.sample` to a file named `.env` and modify the contents as needed.

```shell
ORACLE_CONTAINER_NAME=oracle_ai_database_26ai_free
ORACLE_LISTENER_PORT=1521
ORACLE_PWD=oracle
```

Examples of Use
---------------

### [run.sh](run.sh)

Create a new container and start an Oracle Database server instance.

```console
$ ./run.sh
Starting an Oracle Database Server Instance.
Trying to pull container-registry.oracle.com/database/free:23.26.0.0...
Getting image source signatures
Copying blob 80e077127e4d done   |
Copying blob 1f1cf24bbf7e done   |
Copying blob 4acf832d90b3 done   |
Copying blob b9396890732e done   |
Copying blob 0ff37fff6869 done   |
Copying blob 5a07736fdde8 done   |
Copying blob cd7b8ba429c8 done   |
Copying blob 1b6fc027e13a done   |
Copying blob 6dd3b1e173c3 done   |
Copying blob fdabdccae093 done   |
Copying blob 3eca54462a88 done   |
Copying blob f88fb65e9580 done   |
Copying blob 274ee7eae0eb done   |
Copying blob e512329394fd done   |
Copying blob 1e28433bae34 done   |
Copying blob c1ddce606179 done   |
Copying blob ae4df28d16d5 done   |
Copying blob 61481f80e884 done   |
Copying blob b8b4e463ec9c done   |
Copying blob 9d5777971f73 done   |
Copying blob 3fe4d7e78842 done   |
Copying blob 878564f7347e done   |
Copying config 4cb8a09d3b done   |
Writing manifest to image destination
7e9ec7681fafc8a5762dbafa58ce819cc65cf40e7b629778b8bb471efb22c6c9
Waiting for oracle_ai_database_26ai to get healthy ........................................................... done
$
```

### [install-sample.sh](install-sample.sh)

Installs sample schemas.

```console
$ ./install-sample.sh


SQLcl: Release 25.3 Production on Wed Oct 15 05:58:24 2025

Copyright (c) 1982, 2025, Oracle.  All rights reserved.

Last Successful login time: Wed Oct 15 2025 05:58:25 +00:00

Connected to:
Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0


Thank you for installing the Oracle Human Resources Sample Schema.
This installation script will automatically exit your database session
at the end of the installation or if any error is encountered.
The entire installation will be logged into the 'hr_install.log' log file.

Enter a password for the user HR:
...
...
...
Installation verification
_________________________
Verification:

Table                      provided actual
__________________________ ________ ______
channels                          5      5
costs                         82112  82112
countries                        35     35
customers                     55500  55500
products                         72     72
promotions                      503    503
sales                        918843 918843
times                          1826   1826
supplementary_demographics     4500   4500

Thank you!
________________________________________________________
The installation of the sample schema is now finished.
Please check the installation verification output above.
You will now be disconnected from the database.
Thank you for using Oracle Database!
Disconnected from Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0
$
```

### [sqlplus.sh](sqlplus.sh)

Connect to CDB root with SQL*Plus and confirm the connection.

```console
$ ./sqlplus.sh system/oracle

SQL*Plus: Release 23.26.0.0.0 - Production on Wed Oct 15 06:01:29 2025
Version 23.26.0.0.0

Copyright (c) 1982, 2025, Oracle.  All rights reserved.

Last Successful login time: Wed Oct 15 2025 05:58:46 +00:00

Connected to:
Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0

SQL> show con_name

CON_NAME
------------------------------
CDB$ROOT
SQL> exit
Disconnected from Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0
$
```

Connect to PDB with SQL*Plus and confirm the connection. If you have sample schemas installed, browse to the sample table.

```console
$ ./sqlplus.sh system/oracle@FREEPDB1

SQL*Plus: Release 23.26.0.0.0 - Production on Wed Oct 15 06:02:20 2025
Version 23.26.0.0.0

Copyright (c) 1982, 2025, Oracle.  All rights reserved.

Last Successful login time: Wed Oct 15 2025 06:01:29 +00:00

Connected to:
Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0

SQL> SHOW CON_NAME

CON_NAME
------------------------------
FREEPDB1
SQL> -- If you have sample schemas installed
SQL> SELECT JSON_OBJECT(*) FROM hr.employees WHERE rownum <= 3;

JSON_OBJECT(*)
--------------------------------------------------------------------------------
{"EMPLOYEE_ID":100,"FIRST_NAME":"Steven","LAST_NAME":"King","EMAIL":"SKING","PHO
NE_NUMBER":"1.515.555.0100","HIRE_DATE":"2013-06-17T00:00:00","JOB_ID":"AD_PRES"
,"SALARY":24000,"COMMISSION_PCT":null,"MANAGER_ID":null,"DEPARTMENT_ID":90}

{"EMPLOYEE_ID":101,"FIRST_NAME":"Neena","LAST_NAME":"Yang","EMAIL":"NYANG","PHON
E_NUMBER":"1.515.555.0101","HIRE_DATE":"2015-09-21T00:00:00","JOB_ID":"AD_VP","S
ALARY":17000,"COMMISSION_PCT":null,"MANAGER_ID":100,"DEPARTMENT_ID":90}

{"EMPLOYEE_ID":102,"FIRST_NAME":"Lex","LAST_NAME":"Garcia","EMAIL":"LGARCIA","PH
ONE_NUMBER":"1.515.555.0102","HIRE_DATE":"2011-01-13T00:00:00","JOB_ID":"AD_VP",
"SALARY":17000,"COMMISSION_PCT":null,"MANAGER_ID":100,"DEPARTMENT_ID":90}

JSON_OBJECT(*)
--------------------------------------------------------------------------------


SQL> SELECT 2*3;

       2*3
----------
         6

SQL> exit
Disconnected from Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0
$
```

### [sql.sh](sql.sh)

Connect to PDB with SQLcl and browse to the sample table.

```console
$ ./sql.sh hr/oracle@FREEPDB1


SQLcl: Release 25.3 Production on Wed Oct 15 06:03:33 2025

Copyright (c) 1982, 2025, Oracle.  All rights reserved.

Connected to:
Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0

SQL> set sqlformat csv
SQL> SELECT * FROM hr.employees WHERE rownum <= 3;
"EMPLOYEE_ID","FIRST_NAME","LAST_NAME","EMAIL","PHONE_NUMBER","HIRE_DATE","JOB_ID","SALARY","COMMISSION_PCT","MANAGER_ID","DEPARTMENT_ID"
100,"Steven","King","SKING","1.515.555.0100",17-JUN-13,"AD_PRES",24000,,,90
101,"Neena","Yang","NYANG","1.515.555.0101",21-SEP-15,"AD_VP",17000,,100,90
102,"Lex","Garcia","LGARCIA","1.515.555.0102",13-JAN-11,"AD_VP",17000,,100,90

SQL> exit
Disconnected from Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0
$
```

### [logs.sh](logs.sh)

Show the database alert log and others.

```console
./logs.sh
Starting Oracle Net Listener.
Oracle Net Listener started.
Starting Oracle AI Database instance FREE.
Oracle AI Database instance FREE started.

The Oracle base remains unchanged with value /opt/oracle

SQL*Plus: Release 23.26.0.0.0 - Production on Wed Oct 15 06:13:10 2025
Version 23.26.0.0.0

Copyright (c) 1982, 2025, Oracle.  All rights reserved.


Connected to:
Oracle AI Database 26ai Free Release 23.26.0.0.0 - Develop, Learn, and Run for Free
Version 23.26.0.0.0

SQL>
User altered.
...
...
...
$
```

### [start.sh](start.sh)

Start container and Oracle Database server instance.

```console
$ ./start.sh
oracle_ai_database_26ai
Waiting for oracle_ai_database_26ai to get healthy ........................................................... done
$
```

### [stop.sh](stop.sh)

Shutdown database and stop container.

```console
./stop.sh
oracle_ai_database_26ai
$
```

### [remove.sh](remove.sh)

Remove container.

```console
$ ./remove.sh
oracle_ai_database_26ai
$
```

Author
------

[Shinichi Akiyama](https://github.com/shakiyam)

License
-------

[MIT License](https://opensource.org/licenses/MIT)
