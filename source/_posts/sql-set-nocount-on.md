title: SQL語句 - SET NOCOUNT ON
date: 2023-08-18 17:36
categories: SQL
toc: true
---

在查SQL Store Pocedure時,看到一句寫法,不明白是幹嘛用的

``` sql
SET NOCOUNT ON;
```

### 測試

先執行以下 sql 語法

``` sql
SET NOCOUNT OFF;
SELECT 1, 2, 3, 4, 5;
```

![SET NOCOUNT OFF](../../public/images/SET-NOCOUNT-OFF.png)

切換到 `訊息` 頁面

![SET NOCOUNT OFF MESSAGE ](./SET-NOCOUNT-OFF-訊息.png)

再執行

``` sql
SET NOCOUNT ON;
SELECT 1, 2, 3, 4, 5;
```

![SET NOCOUNT ON](./SET-NOCOUNT-ON.png)

切換到 `訊息` 頁面

![SET NOCOUNT OFF MESSAGE ](./SET-NOCOUNT-ON-訊息.png)

### 結論

如果 `SET NOCOUNT ON` , 則不會返回顯示 `(n 個資料列受到影響)`

### Microsoft文件

[Microsoft原文](https://learn.microsoft.com/en-us/sql/t-sql/statements/set-nocount-transact-sql)說明如下:

> Controls whether a message that shows the number of rows affected by a Transact-SQL statement or stored procedure is returned after the result set. This message is an additional result set.

控制是否在結果集之後傳回顯示 Transact-SQL 語句或預存程式所影響之資料列數目的訊息。

> When SET NOCOUNT is ON, the count isn't returned. When SET NOCOUNT is OFF, the count is returned.

當 SET NOCOUNT 為 ON 時，不會傳回計數。 當 SET NOCOUNT 是 OFF 時，會傳回計數。

> The @@ROWCOUNT function is updated even when SET NOCOUNT is ON.

即使 SET NOCOUNT 是 ON，也會更新 @@ROWCOUNT 函數。

> SET NOCOUNT ON prevents the sending of DONEINPROC messages to the client for each statement in a stored procedure. For stored procedures that contain several statements that don't return much actual data, or for procedures that contain Transact-SQL loops, setting SET NOCOUNT to ON can provide a significant performance boost, because network traffic is greatly reduced.

SET NOCOUNT ON 會防止針對預存程序中的每個陳述式，將 DONEINPROC 訊息傳給用戶端。 對於包含數個未傳回實際資料的語句的預存程式，或針對包含 Transact-SQL 迴圈的程式，將 SET NOCOUNT 設定為 ON 可提供顯著的效能提升，因為網路流量大幅降低。

> The setting specified by SET NOCOUNT is in effect at execute or run time and not at parse time.

SET NOCOUNT 所指定的設定是在執行階段進行設定，而不是在剖析階段進行設定。

> To view the current setting for this setting, run the following query.

若要檢視此設定的目前設定，請執行下列查詢。

``` sql
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';
SELECT @NOCOUNT AS NOCOUNT;
```

