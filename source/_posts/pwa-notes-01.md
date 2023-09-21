---
title: 建立最簡易可安裝的PWA網頁
date: 2023-09-21 11:24
---

要建立可安裝的PWA網頁,有以下幾個步驟

### 建立 index.html

index.html 內引用 `manifest.json` 和 `app.js`

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="manifest" href="manifest.json">
    <script src="app.js"></script>
    <title>Document</title>
</head>
<body>
    <h1>PWA Test</h1>
</body>
</html>
```

### 建立 icons 目錄

將要使用到的 icon 檔案 ex: `pwa.png` 放置至 `icons` 此目錄下

### 建立 manifest.json

除了 `name` 和 `icons` 外, `start_url` 和 `display` 也是必要的,不能省略

``` json
{
    "name": "pwa test",
    "start_url": "index.html",
    "display": "standalone",
    "icons": [
        {
            "src": "icons/pwa.png",
            "type": "image/png",
            "sizes": "512x512"
        }
    ]
}
```

### 建立 app.js

在 `app.js` 內註冊 Service Worker (使用 `sw.js` )

``` js
const registerServiceWorker = async () => {
    if ("serviceWorker" in navigator) {
      try {
        const registration = await navigator.serviceWorker.register("/sw.js", {
          scope: "/",
        });
        if (registration.installing) {
          console.log("Service worker installing");
        } else if (registration.waiting) {
          console.log("Service worker installed");
        } else if (registration.active) {
          console.log("Service worker active");
        }
      } catch (error) {
        console.error(`Registration failed with ${error}`);
      }
    }
};
  
registerServiceWorker();
```

### 建立 sw.js

``` js
const addResourcesToCache = async (resources) => {
    const cache = await caches.open("v1");
    await cache.addAll(resources);
};

self.addEventListener("install", (event) => {
    event.waitUntil(
        addResourcesToCache([
            "/",
            "/index.html",
            "/app.js",
        ]),
    );
});
```



### 執行 live server

用瀏覽器訪問 http://localhost:5500

### reference 

- [Making PWAs installable](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable)
- [制作可安装的 PWA](https://developer.mozilla.org/zh-CN/docs/Web/Progressive_web_apps/Guides/Making_PWAs_installable)
- [Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
- [使用 Service Worker](https://developer.mozilla.org/zh-CN/docs/Web/API/Service_Worker_API/Using_Service_Workers)
