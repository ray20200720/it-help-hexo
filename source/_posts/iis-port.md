title: 無法啟動IIS Express Web 伺服器 
date: 2023-11-21 11:31
categories: IIS, Port
----------------------

用 Visual Studio開發 ASP.NET Web Form時,偶爾會出現 `無法啟動IIS Express Web 伺服器`, 

即使重新開機, 還是沒有解決. 最後是修改 `Project Url` 的Port, 改到能正常啟動

步驟如下:

1. `Solution Explorer` -> `YourProject` -> 滑鼠右鍵 `Properties` 
2. `Web` -> `Project Url` 

![iis-project-url](/pic/iis-project-url.png)


### 參考資料

- [解除「無法啟動IIS Express Web 伺服器」的問題](https://dotblogs.com.tw/whd/2017/03/08/001714)




