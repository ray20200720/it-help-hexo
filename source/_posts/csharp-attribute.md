title: C# Attribute
date: 2023-10-03 10:50
categories: C# ASP.NET
---

每過一段時間就會忘記C#的 `Attribute`, 今天又看了一次, 記錄一下. 

本文主要參考自 [手冊網-C#特性](https://www.shouce.ren/api/view/a/7434).

## C#程式碼中, 類別上面有一個用中括號包住的東西, ex: [Obselete] 或是 [Conditional("DEBUG")] 等, 這是什麼 ?

在C#程式碼中看到出現中括號 類似 `[Obselete]` 之類的, 主要放在 `class`, 或 `method` 或 `struct` 等...的上面.那個就是Attribute.

## 怎麼使用Attribute呢?

最簡單的使用方法可以在某個Method上方,添加 `[Obsolete]`, 這樣在IDE裡撰寫程式碼的時候, 會提示`xxx is Obsolete`.表示這個方法已經被棄用. 如果想要提示更多訊息,可以傳參數,改寫成 `[Obsolete("Do not use this method.")]`.如果想更進一步不允許使用這個方法,可以再傳入error=true,寫成 `[Obsolete("Do not use this method.", true)]`,這樣一來,建置時有發現使用這個方法,會直接報錯,編譯無法通過.

`Hello.cs` 範例如下:

``` cs
class Hello
{
    [Obsolete]
    public void SayHello()
    {
        Console.WriteLine("No! This is old method.");
    }

    [Obsolete("try others")]
    public void SayHello2()
    {
        Console.WriteLine("No! No! This is also old method.");
    }

    [Obsolete("try others again", true)]
    public void SayHello3()
    {
        Console.WriteLine("No! No! No! You can't call this method.");
    }

    public void SayHello()
    {
        Console.WriteLine("Hello!");
    }
}
```

`Program.cs` 範例如下:

``` cs
Hello hello = new Hello();

hello.SayHello();       //warning

hello.SayHello2();      //warning

//hello.SayHello3();    //Error
```

## 還有其他的使用方法嗎?

還有一種用法,在 method上方加上 `[Conditional("DEBUG")]`,這樣一來,該方法只有在Debug模式下才會執行,在Release模式是不會執行.

## 如何自定義Attribute?

1. 定義一個新的類別,並繼承 `System.Attribute`

2. 









