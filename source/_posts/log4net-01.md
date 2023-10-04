title: log4net 使用與配置及不能產生Log文件
date: 2023-10-04 16:40
categories: log4net
---

log4net 使用與配置

### 下載

- [Apache log4net™](https://logging.apache.org/log4net/) Apache官網可下載

- [nuget-log4net](https://www.nuget.org/packages/log4net/) 也可以透過nuget下載

### 使用方法

參考 程式人生的[關於Log4Net的使用及配置方式](https://www.796t.com/content/1579330922.html)

### 沒有產生Log文件

解決方法:

1. 在 `AssemblyInfo.cs` 添加一行 `[assembly: log4net.Config.XmlConfigurator(Watch = true)]`

``` cs
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]

[assembly: log4net.Config.XmlConfigurator(Watch = true)]
```

2. 或者在使用log4net的類別(namesapce上面)加上 log4net attribute 如下

``` cs
[assembly: log4net.Config.XmlConfigurator(Watch = true)]
namespace MyTestClass
{

}
```







