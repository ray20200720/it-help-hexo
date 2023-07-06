---
title: TypeScript Notes
date: 2023-07-05 13:05
---

### 安裝TypeScript

``` bash
$ sudo npm install -g typescript
```

### 編寫第一個TypeScript

``` bash
$ emacs index.ts
```

`index.ts`

``` bash
const message = 'Hello World';

console.log(message)
```

### 編譯TypeScript

``` bash
$ tsc
```

執行tsc會自動尋找所有`.ts`結尾的檔案並產生js檔案

### 執行

``` bash
$ node index.js
```

reference : [Day 01. 遠征 TypeScript・行前準備](https://ithelp.ithome.com.tw/articles/10214714)
