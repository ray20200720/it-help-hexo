title: ASP.NET Web API
date: 2024-02-07 10:55
categories: ASP.NET, Web API
----------------------------------

根據[Microsoft官方文件](https://learn.microsoft.com/zh-tw/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)建立了 Web API

### 建立 Web API 專案

步驟如下: 

1. 建立新的專案
2. ASP.NET web 應用程式(.NET Framework)
3. 專案名稱 ProductsApp
4. 空白 -> 勾選 Web API -> 取消 https

### 新增模型

步驟如下: 

1. Models 資料夾下 -> 加入 -> 類別 -> Product.cs

Product.cs 內容如下

``` cs
namespace ProductsApp.Models
{
    public class Product
    {
        public int Id { get; set; }
        public string Name { get; set; }
        public string Category { get; set; }
        public decimal Price { get; set; }
    }
}
```

### 新增控制器

步驟如下: 

1. Controllers 資料夾下 -> 加入 -> 控制器 
2. 新增 Scaffold 項目 -> Web API -> Web API 2 控制器 -> 空白 -> ProductsController

ProductsController.cs 內容如下

``` cs
using ProductsApp.Models;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Web.Http;

namespace ProductsApp.Controllers
{
    public class ProductsController : ApiController
    {
        Product[] products = new Product[] 
        { 
            new Product { Id = 1, Name = "Tomato Soup", Category = "Groceries", Price = 1 }, 
            new Product { Id = 2, Name = "Yo-yo", Category = "Toys", Price = 3.75M }, 
            new Product { Id = 3, Name = "Hammer", Category = "Hardware", Price = 16.99M } 
        };

        public IEnumerable<Product> GetAllProducts()
        {
            return products;
        }

        public IHttpActionResult GetProduct(int id)
        {
            var product = products.FirstOrDefault((p) => p.Id == id);
            if (product == null)
            {
                return NotFound();
            }
            return Ok(product);
        }
    }
}
```

### 測試

按 F5 在瀏覽器網址輸入 `http://localhost:56957/api/products`

###  使用 JAVAscript 和 jQuery 呼叫 Web API

步驟如下: 

1. ProductsApp 專案下 -> 加入 -> 新增項目 -> HTML頁面 -> index.html

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
    var uri = 'api/products';

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

### 測試

將 index.html 設定為起始頁後, 按 F5 執行

### 參考資料

- [開始使用 ASP.NET Web API 2 (C#)](https://learn.microsoft.com/zh-tw/aspnet/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)