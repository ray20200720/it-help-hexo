title: IIS 架設 FTP
date: 2023-11-17 13:58
categories: IIS, FTP
----------------------

每過一段時間就會忘記IIS怎麼設定FTP Server,這次做一下筆記,供未來查詢參考用

## Quick Start

### 開啟 Windows 功能

首先開啟 「控制台」 ,點擊 「程式集」 

![程式集](pic/control.png)

點擊 「開啟或關閉 Windows 功能」 

![開啟或關閉 Windows 功能](pic/windows.png)

勾選 「Internet Information Services」 
    - [FTP 伺服器]
        - [FTP 服務]
        - [FTP 擴充性]

![Internet Information Services](pic/iis.png)

### 開啟 Internet Information Services

搜尋 [IIS] 點擊 「Internet Information Services (IIS 管理員)」 

![Internet Information Services (IIS 管理員)](pic/iis-admin.png)

![IIS](pic/iis-admin-2.png)

在 「站台」 點 滑鼠右鍵 「新增FTP站台」

![FTP](pic/iis-add-ftp.png)

「新增FTP站台」視窗內輸入 「FTP站台名稱」 並指定對應的 「實體路徑」,完成後點擊 「下一步」

![FTP](pic/iis-add-ftp-2.png)

「命令提示字元」 輸入 「ipconfig」 查詢IP

![ftp-ipconfig](pic/ftp-ipconfig.png)

「繫結和SSL 設定」 「IP位址」 內輸入 上一步查詢出的 IP

「SSL」 選擇  「沒有SSL」

完成後點擊 「下一步」

![Binding IP](pic/ftp-binding-ip.png)

「驗證和授權資訊」 勾選 「匿名」
「授權」 「允許存取」 選擇 「所有使用者」
「權限」 勾選 「讀取」 和 「寫入」
 
 完成後點擊 「完成」

![ftp-anonymous.png](pic/ftp-anonymous.png)

### FTP 連線測試

開啟 「命令提示字元」 ,輸入 「FTP <IP>」

接著輸入帳號 「anonymous」 和 密碼 「」 (此處為空白)

可看見 「User logged in.」 訊息, 表示 FTP 連線成功

![ftp-connect](/pic/ftp-connect.png)




