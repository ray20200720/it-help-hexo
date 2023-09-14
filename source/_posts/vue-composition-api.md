---
title: Vue 3 - Composition API
date: 2023-09-14 15:10
---

Vue 3 的 Composition API 老是學了又忘, 在這裡記錄一下最簡單的用法:

HTML 內添加 `id="app"` 元素

``` html
  <div id="app">
    <button @click="count++">
      Count is: {{ count }}
    </button>
  </div>
```

JavaScript 添加 Composition API 的寫法

``` js
  <script type="module">
  import { createApp, ref } from 'https://cdnjs.cloudflare.com/ajax/libs/vue/3.3.4/vue.esm-browser.min.js'
  const app = createApp({
      setup() {
          return {
              count: ref(0)
          }
      }
  }).mount('#app')
  </script>
```

以上開啟網頁即可生效.

如果將vue.esm-browser.min.js下載下來.在本地引用的話,必須要啟動 Server 才能正常載入.
可以透過 `Live Server` 插件, 或者用 其他可以啟動 Server 的方式. ex: dotnet run 或 nodejs等
