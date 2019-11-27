---
authors:
  - r-richmond
title: " Setting up Oracle ODBC on macOS with ISQL"
date: 2019-11-24
draft: false
categories :
  - Tinkerer
tags:
  - SQL
  - Oracle
  - isql
  - ODBC
---

# 0) Install ISQL

If you're on macOS the easiest way to install isql is using [homebrew](https://brew.sh) `brew install unixodbc`.

# 1) Download drivers

  1. Download ODBC Package & Basic Package from [here](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html)
  1. Create an oracle account if necessary

# 2) Prepare driver files

  1. `cd Downloads`
  1. `unzip instantclient-basic-macos.x64-19.3.0.0.0dbru.zip`
  1. `unsip instantclient-odbc-macos.x64-19.3.0.0.0dbru.zip`
  1. `mkdir ~/lib`
  1. `mkdir -p /opt/oracle/`
  1. `mv $(pwd)/instantclient_19_3 /opt/oracle/`
  1. `ln -s /opt/oracle/instantclient_19_3/libclntsh.dylib.19.1 /opt/oracle/instantclient_19_3/libclntshcore.dylib.19.1 ~/lib`

# 3) Update ODBC ini files

  1. update `odbcinst.ini` to add
```
[ODBC Drivers]
Oracle ODBC Driver = Installed
...
...
[Oracle ODBC Driver]
Description = Oracle 19 ODBC driver
Driver      = /opt/oracle/instantclient_19_3/libsqora.dylib.19.1
Setup       =
FileUsage   =
CPTimeout   =
CPReuse     =
```
  1. Update `odbc.ini` to add
```
[ODBC Data Sources]
{dsn_name} = [Oracle ODBC Driver]
...
...
[{dsn_name}]
AggregateSQLType=FLOAT
Application Attributes=T
Attributes=W
BatchAutocommitMode=IfAllSuccessful
BindAsFLOAT=F
CacheBufferSize=20
CloseCursor=F
DisableDPM=F
DisableMTS=T
DisableRULEHint=T
Driver=/opt/oracle/instantclient_19_3/libsqora.dylib.19.1
DSN={dsn_name}
EXECSchemaOpt=
EXECSyntax=T
Failover=T
FailoverDelay=10
FailoverRetryCount=10
FetchBufferSize=64000
ForceWCHAR=F
LobPrefetchSize=8192
Lobs=T
Longs=T
MaxLargeData=0
MaxTokenSize=8192
MetadataIdDefault=F
QueryTimeout=T
ResultSets=T
ServerName={host}:{port}/{server}
SQLGetData extensions=F
SQLTranslateErrors=F
StatementCache=F
Translation DLL=
Translation Option=0
UseOCIDescribeAny=F
UserID={username}
Password={password}
```

# 4) Verify installation

  1. Verify by connecting `isql -v {dsn_name}`
  1. Note: on macOS Catalina or later you may have to workaround the lack of notarization by navigating to "system preferences>security>allow" and approving multiple files after multiple connection attempts using step 4.1
