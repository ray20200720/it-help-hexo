---
title: .NET Command
---

### 安裝.NET SDK或.NET Runtime

#### 安裝.NET 7

##### 安裝 SDK

``` bash
$ sudo dnf install dotnet-sdk-7.0
```

##### 安裝 runtime
``` bash
$ sudo dnf install aspnetcore-runtime-7.0
```

#### 安裝.NET 6

##### 安裝 SDK

``` bash
$ sudo dnf install dotnet-sdk-6.0
```

##### 安裝 runtime
``` bash
$ sudo dnf install aspnetcore-runtime-6.0
```

### 查詢.NET版本的各種指令

.NET版本

``` bash
$ dotnet --version
7.0.108
```

.NET詳細資訊

``` bash
$ dotnet --info
```

查看已安裝的dotnet sdk版本

``` bash
$ dotnet --list-sdks
```

查看已安裝的dotnet runtime版本

``` bash
$ dotnet --list-runtimes
```

### 如何指定特定的 SDK & Runtime 版本

建立 `global.json`

``` json
{
  "sdk": {
    "version": "6.0.000"
  }
}
```

More Info : 
- [dotnet command](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet)
- [dotnet 命令](https://learn.microsoft.com/zh-tw/dotnet/core/tools/dotnet)
- [Install the .NET SDK or the .NET Runtime on Fedora](https://learn.microsoft.com/en-us/dotnet/core/install/linux-fedora)