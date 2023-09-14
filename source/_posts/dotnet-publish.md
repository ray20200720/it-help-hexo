---
title: dotnet publish
date: 2023-09-14 16:15
---

之前知道了可用 `dotnet publish` 進行發佈,但產生的檔案是在 `bin\Debug` 目錄底下,感覺不太舒服,沒有 release的感覺. 抽空查了一下要怎麼產生在 `bin\Release` 目錄底下. 

### 推薦兩篇文章:

1. Microsoft官方文件:

[使用 .NET CLI 發佈 .NET 應用程式](https://learn.microsoft.com/zh-tw/dotnet/core/deploying/deploy-with-cli).

2. 黑大(黑暗執行緒)的詳細說明文:
[使用 dotnet 命令列工具發行 .NET 6 專案](https://blog.darkthread.net/blog/dotnet6-publish-notes/)

### 具體作法

使用 `dotnet publish` 指令帶參數 `-c Release`

``` bash
dotnet publish -c Release
```

### 補充

`dotnet publish` 之後會產生 `xxx.exe` 和 `xxx.dll`, 如果在 windows 底下,可以直接執行 exe 檔. 如果在 linux 底下, 用 `dotnet xxx.dll` 就啟動服務了.