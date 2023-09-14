---
title: Linux上部屬 .NET
date: 2023-09-14 11:37
---

今天看到一篇關於如何將.NET Web部屬在Linux Server上的文章.覺得很實用.
文章連結如下[ASP.NET Core 实战：Linux 小白的 .NET Core 部署之路](https://www.cnblogs.com/danvic712/p/9975402.html).

另外一篇是Microsoft官方文件寫的,內容圖文並茂,寫的很不錯.
連結為[使用 SDK 建立 .NET Core Web 應用程式](https://learn.microsoft.com/zh-tw/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/2-1-create-configure-aspnet-core-applications).

如果要安裝Nginx,可以參考另外一篇:
[安裝 Nginx 並將其設定為反向 Proxy 伺服器](https://learn.microsoft.com/zh-tw/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/2-2-install-nginx-configure-it-reverse-proxy)

記錄一下具體作法:

創建專案

``` bash
dotnet new webapp -n AspNetCoreDemo -o firstwebapp 
cd firstwebapp
dotnet run
```

建置專案 

``` bash
dotnet publish
```

部屬專案

``` bash
cd bin/Debug/net7.0/publish
dotnet AspNetCoreDemo.dll
```