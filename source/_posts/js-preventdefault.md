title: OnKeyPress ENTER Reloads The Page
date: 2023-11-17 16:02
categories: JavaScript
---------------------------

專案上遇到一個常見的問題. 過兩週又忘記了,所以記錄一下,方便下次查看

## How to avoid reload the page after ENTER

### Source Code

原始頁面 

``` html
<input type="text" id="txtInput" runat="server" maxlength="300" style="width: 80%;" onkeypress="DoFilter(this.value.trim());"/>
```

``` js
function DoFilter(val) {
    if (val) {
        // doSomething();
    } else {
        // doOtherThing();
    }
}
```

問題描述: 

    當在文字框按下ENTER鍵時,整個頁面會reload,導致頁面上的數據會丟失.

解決方法: 

    在 `onkeypress="DoFilter(this.value.trim());"` 後面加上 `event.preventDefault();`

完整代碼:

``` html
<input type="text" id="txtInput" runat="server" maxlength="300" style="width: 80%;" onkeypress="DoFilter(this.value.trim()); event.preventDefault();"/>
```

### More Info :
- [JavaScript For Of](https://stackoverflow.com/questions/12781308/onkeypress-enter-reloads-the-page)