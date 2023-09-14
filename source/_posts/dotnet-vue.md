---
title: .NET 遇見 Vue
date: 2023-09-14 15:22
---

今天嘗試在.NET Web App裡使用Vue,有成功顯示, 在這裡記錄一下最簡單的用法:

先執行
``` bash
dotnet new webapp -o DotnetVueWebApp
```

修改 `Index.cshtml`

1. 引用 vue

``` html
<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
```

2. 修改 `<div class="text-center">` 元素如下

``` html
<div id="app" class="text-center">
    <h1 class="display-4">Welcome</h1>
    <p>Learn about <a href="https://docs.microsoft.com/aspnet/core">building Web apps with ASP.NET Core</a>.</p>
    <p>{{ message }} <a :href="[url]">Vue</a>.</p>
    <button v-on:click="count++">{{ count }}</button>
    <p>Has published books:</p>
    <span>{{ author.books.length > 0 ? 'Yes' : 'No' }}</span>
</div>
```
3. JavaScript 用 Vue

``` js
<script>
  const { createApp } = Vue
  createApp({
    data() {
      return {
        url: 'https://vuejs.org/',
        message: 'Learn about ',
        count: 0,
        author: {
            name: 'John Doe',
            books: [
                'Vue 2 - Advanced Guide',
                'Vue 3 - Basic Guide',
                'Vue 4 - The Mystery'
            ]
        }
      }
    }
  }).mount('#app')
</script>
```

4. 執行 `dotnet run`

5. 開啟瀏覽器 瀏覽 `http://localhost:5500`


