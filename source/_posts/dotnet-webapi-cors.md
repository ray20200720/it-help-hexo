---
title: .NET Web API 解決 CORS
date: 2023-09-15 13:50
---

嘗試前台用Vue,後台使用.NET Web API,前台向後台要資料,會遇到 CORS問題,記錄一下解法:

參考MicroSoft官方文件:
[在 ASP.NET 核心中啟用跨原始來源要求 （CORS）](https://learn.microsoft.com/zh-tw/aspnet/core/security/cors?view=aspnetcore-7.0)

### 創建專案

``` bash
dotnet new webapi -o HelloWorld
```

### 修改 `Program.cs`

修改內容如下

完整程式碼如下

``` cs
var MyAllowSpecificOrigins = "_myAllowSpecificOrigins";

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddCors(options =>
{
    options.AddPolicy(MyAllowSpecificOrigins,
                          policy =>
                          {
                              policy.WithOrigins("http://example.com",
                                                  "http://www.contoso.com")
                                                  .AllowAnyHeader()
                                                  .AllowAnyMethod();
                          });
});

builder.Services.AddControllers();

var app = builder.Build();
app.UseHttpsRedirection();
app.UseStaticFiles();
app.UseRouting();

app.UseCors(MyAllowSpecificOrigins);

app.UseAuthorization();

app.MapControllers();

app.Run();
```



