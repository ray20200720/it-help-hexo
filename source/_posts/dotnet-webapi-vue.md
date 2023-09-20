---
title: .NET Web API 遇見 Vue
date: 2023-09-15 14:00
---

嘗試前台用Vue,後台使用.NET Web API, 前台向後台要資料,將結果返回輸出至前台:

### 創建vue專案

``` bash
cd ~/Project/vue-dotnet
npm create vue@latest
```

``` bash 
✔ Project name: … Web
✔ Add TypeScript? … No / Yes
✔ Add JSX Support? … No / Yes
✔ Add Vue Router for Single Page Application development? … No / Yes
✔ Add Pinia for state management? … No / Yes
✔ Add Vitest for Unit testing? … No / Yes
✔ Add an End-to-End Testing Solution? … No / Cypress / Playwright
✔ Add ESLint for code quality? … No / Yes
✔ Add Prettier for code formatting? … No / Yes
```

``` bash
cd Web
npm install
npm run dev
```

### 修改 Web

1. 刪除 `Web\src\components\` 下其它的 xxx.vue
2. 在 `Web\src\componets\` 下 增加 MyComponent.vue

``` js
<template>
    <li class="my-blue" v-for="item in items" :key="item.id" >
        {{ item.date }} {{ item.temperatureC }} {{ item.temperatureF }} {{  item.summary }}
    </li>
</template>
  
<script>
export default {
    data() {
        return {
            items: []
        }
    },
    mounted() {
        fetch("http://localhost:5021/WeatherForecast")
        .then(res => res.json())
        .then(data => this.items = data)
    },
}
</script>
  
<style>
.my-blue {
    color: blue
}
</style>
```

3. 修改 `Web\src\App.vue`

``` js
<script setup>
import MyComponent from './components/MyComponent.vue';
</script>

<template>
  <MyComponent>{{ items }}</MyComponent>
</template>

<style>
</style>
``` 


### 創建dotnet web api專案

``` bash
mkdir ~/Project/vue-dotnet
```

``` bash
cd ~/Project/vue-dotnet
dotnet new webapi -o WebAPI
```

### 修改 WebAPI 支援 CORS 

修改 `Program.cs` 內容如下

``` cs
var MyAllowSpecificOrigins = "_myAllowSpecificOrigins";

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddCors(options =>
{
    options.AddPolicy(MyAllowSpecificOrigins,
                          policy =>
                          {
                              policy.WithOrigins("http://localhost:5173")
                                                  .AllowAnyHeader()
                                                  .AllowAnyMethod();
                          });
});

// Add services to the container.

builder.Services.AddControllers();
// Learn more about configuring Swagger/OpenAPI at https://aka.ms/aspnetcore/swashbuckle
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseHttpsRedirection();

app.UseCors(MyAllowSpecificOrigins);

app.UseAuthorization();

app.MapControllers();

app.Run();
```


### 啟動

``` bash
cd ~/Project/vue-dotnet/WebAPI
dotnet run
```

``` bash
cd ~/Project/vue-dotnet/Web
npm run dev
```

開瀏覽器 輸入 `http://localhost:5173/` , 可以看到後台傳來的資料