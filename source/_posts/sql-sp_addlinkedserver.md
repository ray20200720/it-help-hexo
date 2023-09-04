---
title: sql 連線問題
date: 2023-09-04 18:09
---

今天遇到一個很常見的SQL Server問題,順利解決了.記錄一下:

假設有

第1台 DB IP: 111.111.111.111  使用port:1433
第2台 DB IP: 222.222.222.222  使用port:1433

現已連接到第1台,但想直接查詢第2台DB的資料,會在查詢SQL前面加上IP.

``` sql
SELECT * FROM [222.222.222.222].MS.dbo.Product
```

但Server升級後,使用上述的連接查詢會出現下面錯誤

``` sql
訊息 7202，層級 11，狀態 2，行 1
Could not find server '222.222.222.222' in sys.servers. Verify that the correct server name was specified. If necessary, execute the stored procedure sp_addlinkedserver to add the server to sys.servers.
```

從提示的內容得知,先以下列語句查看是否已經有DBLink

``` sql
select * from sys.servers
```

| server_id	| name            | product    | provider | data_source     | location |
|-----------|-----------------|------------|----------|-----------------|----------|
|0          | 111.111.111.111 | SQL Server | SQLNCLI  | 111.111.111.111 |NULL      |

執行下列語句增加DBLink

``` sql
EXEC sp_addlinkedserver @server = '222.222.222.222'
```

再次查詢,可發現有多一筆

| server_id	| name            | product    | provider | data_source     | location |
|-----------|-----------------|------------|----------|-----------------|----------|
|0          | 111.111.111.111 | SQL Server | SQLNCLI  | 111.111.111.111 |NULL      |
|1          | 222.222.222.222 | SQL Server | SQLNCLI  | 222.222.222.222 |NULL      |

``` sql
select * from sys.servers
```

此時就可以查詢第2台的資料

``` sql
SELECT * FROM [222.222.222.222].MS.dbo.Product
```
