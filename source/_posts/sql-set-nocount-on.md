---
title: sql SET NOCOUNT ON
date: 2023-08-18 17:36
---

在查SQL Store Pocedure時,看到一句寫法,不明白是幹嘛用的

``` sql
SET NOCOUNT ON;
```

官方原文如下:

When SET NOCOUNT is ON, the count isn't returned. When SET NOCOUNT is OFF, the count is returned.

The @@ROWCOUNT function is updated even when SET NOCOUNT is ON.

SET NOCOUNT ON prevents the sending of DONEINPROC messages to the client for each statement in a stored procedure. For stored procedures that contain several statements that don't return much actual data, or for procedures that contain Transact-SQL loops, setting SET NOCOUNT to ON can provide a significant performance boost, because network traffic is greatly reduced.

The setting specified by SET NOCOUNT is in effect at execute or run time and not at parse time.

To view the current setting for this setting, run the following query.
