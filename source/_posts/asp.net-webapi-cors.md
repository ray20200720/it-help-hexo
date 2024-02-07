title: ASP.NET Web API CORS
date: 2024-02-07 11:23
categories: ASP.NET, Web API, CORS
----------------------------------

根據[Microsoft官方文件](https://learn.microsoft.com/zh-tw/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)建立了 Web API

但當 index.html 另建立於其它專案下,會出現 CORS 錯誤.

``` html
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>Product App</title>
</head>
<body>

  <div>
    <h2>All Products</h2>
    <ul id="products" />
  </div>
  <div>
    <h2>Search by ID</h2>
    <input type="text" id="prodId" size="5" />
    <input type="button" value="Search" onclick="find();" />
    <p id="product" />
  </div>

  <script src="https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js"></script>
  <script>
    //var uri = 'api/products';
    var uri = 'http://localhost:56957/api/products';

    $(document).ready(function () {
      // Send an AJAX request
      $.getJSON(uri)
          .done(function (data) {
            // On success, 'data' contains a list of products.
            $.each(data, function (key, item) {
              // Add a list item for the product.
              $('<li>', { text: formatItem(item) }).appendTo($('#products'));
            });
          });
    });

    function formatItem(item) {
      return item.Name + ': $' + item.Price;
    }

    function find() {
      var id = $('#prodId').val();
      $.getJSON(uri + '/' + id)
          .done(function (data) {
            $('#product').text(formatItem(data));
          })
          .fail(function (jqXHR, textStatus, err) {
            $('#product').text('Error: ' + err);
          });
    }
  </script>
</body>
</html>
```

``` js
Access to XMLHttpRequest at 'http://localhost:56957/api/products' from origin 'null' has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

其實瀏覽器是有接收到回覆, 只是因為 CORS 所以擋掉

``` js
GET http://localhost:56957/api/products net::ERR_FAILED 200 (OK)
```

根據官方文件[在 ASP.NET Web API 2 中啟用跨原始來源要求](https://learn.microsoft.com/zh-tw/aspnet/web-api/overview/security/enabling-cross-origin-requests-in-web-api)還是解決不了.

後來在網路上搜到,參考 [asp.net webapi 跨域问题解决 No 'Access-Control-Allow-Origin' header i](https://blog.csdn.net/huazaizuiaiw/article/details/104147288) 後, 解決 CORS問題.

主要步驟有2個:

1. 修改 `Web.Config` 在 `system.webServer` 添加 `httpProtocol`

``` xml
<system.webServer>
	<httpProtocol>
		<customHeaders>
			<add name="Access-Control-Allow-Origin" value="*"/>
			<add name="Access-Control-Allow-Headers" value="Content-Type,Token" />
			<add name="Access-Control-Allow-Methods" value="GET, POST, PUT, DELETE, OPTIONS" />
		</customHeaders>
	</httpProtocol>
</system.webServer>
```

2. 配置 `Global.asax.cs`

增加 `Application_BeginRequest` 

``` cs
protected void Application_BeginRequest(object sender, EventArgs e)
{
    if (Request.HttpMethod.ToUpper() == "OPTIONS")
    {
        Response.StatusCode = 200;
        Response.End();
    }    
}
```

### 參考資料

- [asp.net webapi 跨域问题解决 No 'Access-Control-Allow-Origin' header i](https://blog.csdn.net/huazaizuiaiw/article/details/104147288)