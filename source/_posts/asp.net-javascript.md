title: ASP.NET $get
date: 2023-11-20 17:49
categories: ASP.NET, JavaScript
---

今天在網路上看到一個用法 `$get`, 不曉得這個`$get`是幹嘛用的.

``` html
<body id="bodytag">

</body>
```

``` js
var bodyTag = 'bodytag';

function doSomething(val) {
    if (val) {
        $get(bodyTag).style.backgroundColor = 'white';
    } else {
        $get(bodyTag).style.backgroundColor = 'gray';
    }
}
```

後來在 stackoverflow 查到


`$get` & `$find` are shortcut functions Microsoft has built into their Ajax JavaScript Library.

`$get` is short for the standard JavaScript `GetElementById` function. `$find` is short for .Net's `findComponent()` function. This is not a standard JavaScript function and is specific to Microsoft's Ajax JavaScript library.


原來 `$get` 是 Microsoft內建的JavaScript Library,等同於JS裡的`GetElmentById`

### 參考資料

- [What's the difference between $get and $find in JavaScript?](https://stackoverflow.com/questions/2726304/whats-the-difference-between-get-and-find-in-javascript)