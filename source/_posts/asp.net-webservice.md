title: ASP.NET Web Service
date: 2023-11-21 11:05
categories: ASP.NET, Web Service
---------------------------------

在aspx頁面添加ScriptManager及Services之後,無法正常呼叫 Web Service.
老是出現找不到Service. 後來比對官方文件找到問題點

WebForm1.aspx 程式碼如下:

``` html
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="WebForm3.aspx.cs" Inherits="ITHelp.WebForm3" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>調用WebService</title>
</head>
<script type="text/javascript" language="JavaScript">
    function OnButtonClick() {
        ITHelp.WebService1.EchoString(
            document.getElementById('inputName').value, OnRequestComplete
        );

        return false;
    }

    function OnRequestComplete(result) {
        alert(result);
    }
</script>
<body>
    <form id="form1" runat="server">
        <asp:ScriptManager ID="ScriptManager1" runat="server">
            <Services>
                <asp:ServiceReference Path="WebService1.asmx" />
            </Services>
        </asp:ScriptManager>
        <div>
            <input type="text" id="inputName" size="20" />
            <input id="button" type="button" value="調用" onclick="return OnButtonClick()" />
        </div>
    </form>
</body>
</html>

```
WebService1.asmx.cs 程式碼如下:

``` cs 
using System;
using System.Web.Services;

namespace ITHelp
{
    /// <summary>
    /// Summary description for WebService1
    /// </summary>
    [WebService(Namespace = "http://tempuri.org/")]
    [WebServiceBinding(ConformsTo = WsiProfiles.BasicProfile1_1)]
    [System.ComponentModel.ToolboxItem(false)]
    // To allow this Web Service to be called from script, using ASP.NET AJAX, uncomment the following line. 
    [System.Web.Script.Services.ScriptService]
    public class WebService1 : System.Web.Services.WebService
    {
        public WebService1() { }

        [WebMethod]
        public string HelloWorld()
        {
            return "Hello World";
        }

        [WebMethod]
        public string EchoString(String s)
        {
            return "Hello " + s;
        }
    }
}
```

如果無法從aspx呼叫webservice,主要有2個地方要檢查:

1. WebService的 `[System.Web.Script.Services.ScriptService]` 要取消註解
2. aspx呼叫service,在service前面加上namespace, ex: `ITHelp.WebService1.EchoString`

### 參考資料

- [Error: Webservice not defined](https://stackoverflow.com/questions/21545465/error-webservice-not-defined)
- [Exposing Web Services to Client Script](https://learn.microsoft.com/en-us/previous-versions/aspnet/bb398998(v=vs.100))