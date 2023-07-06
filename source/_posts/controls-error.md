---
title: ASP.NET - 無法修改 Controls 集合，因為控制項包含程式碼區塊 (例如 <% ... %>)。
date: 2023-07-03 16:22:37
tags:
---

### 問題描述:

當畫面啟動時,會出現 **無法修改 Controls 集合，因為控制項包含程式碼區塊 (例如 <% ... %>)** 錯誤訊息

### 發生原因:

主要是在&lt;head&gt;&lt;/head&gt;裡面有使用到<% %>

``` html
<%@ Master Language="C#" AutoEventWireup="true" CodeFile="MasterPage.master.cs" Inherits="MasterPage" %>
<%@ Import Namespace="org.ithelp.web" %>
<!doctype html>
<html>
<head runat="server">
    <script type="text/javascript" src="<%=Page.GetFileVersion("~/jquery-1.7.1.min.js")%>"></script>
</head>
<body>
</body>
</html>
```

### 解決方法:

- 方法 1: 加上&lt;asp:PlaceHolder runat="server"&gt;&lt;/asp:PlaceHolder&gt;使其延後執行

``` html
<!doctype html>
<html>
<head runat="server">
    <asp:PlaceHolder runat="server">
        <script type="text/javascript" src="<%=Page.GetFileVersion("~/jquery-1.7.1.min.js")%>"></script>
    </asp:PlaceHolder>
</head>
<body>
</body>
</html>
```

- 方法 2: 將&lt;script&gt;&lt;/script&gt;移至其它位置,例如: &lt;head&gt;&lt;/head&gt;外&lt;body&gt;&lt;/body&gt;內

``` html
<!doctype html>
<html>
<head runat="server">
</head>
<body>
    <script type="text/javascript" src="<%=Page.GetFileVersion("~/jquery-1.7.1.min.js")%>"></script>
</body>
</html>
```
