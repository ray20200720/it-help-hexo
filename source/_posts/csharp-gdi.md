title: C# Windows Form GDI
date: 2023-10-18 13:06
categories: C#, Windows Form
---

圖片檔案格式有bmp和metafile, metafile翻譯為中繼檔.

如何使用Windows Form的GDI讀取bmp檔案,以及輸出中繼檔?

# 讀取 bmp 檔
## 建立一個Windows Form專案
### 在 Form1.cs 添加一個方法

``` cs
private void Form1_Paint(object sender, PaintEventArgs e)
{
    Bitmap myBitmap = new Bitmap(@"D:\Ray\MyLabs\ICON\myPic.bmp");
    e.Graphics.DrawImage(myBitmap, 0, 0);
}
```

### 在 Form1.cs Design 的 Properties 的 Events 找到 Paint  

將 Paint 設定為 Form1_Paint. 在 Form1.Designer.cs 內會自動生成以下程式碼

``` cs
this.Paint += new System.Windows.Forms.PaintEventHandler(this.Form1_Paint);
```

完整程式碼如下:

``` cs
/// <summary>
/// Required method for Designer support - do not modify
/// the contents of this method with the code editor.
/// </summary>
private void InitializeComponent()
{
    this.SuspendLayout();
    // 
    // Form1
    // 
    this.AutoScaleDimensions = new System.Drawing.SizeF(9F, 18F);
    this.AutoScaleMode = System.Windows.Forms.AutoScaleMode.Font;
    this.ClientSize = new System.Drawing.Size(800, 450);
    this.Name = "Form1";
    this.Text = "Form1";
    this.Paint += new System.Windows.Forms.PaintEventHandler(this.Form1_Paint);
    this.ResumeLayout(false);

}
```

# 產生 metafile 檔
## 使用上述的Windows Form專案
### 在 Form1.cs 增加一個方法

``` cs
private void CreateMetaFile_Click(object sender, System.EventArgs e)
{
    Metafile curMetafile = null;
    // Create a Graphics object
    Graphics g = this.CreateGraphics();

    // Get HDC
    IntPtr hdc = g.GetHdc();

    // Create a rectangle
    Rectangle rect = new Rectangle(0, 0, 200, 200);

    // Use HDC to create a metafile with a name

    try
    {
        curMetafile = new Metafile("newFile.wmf", hdc);
    }

    catch (Exception exp)
    {
        MessageBox.Show(exp.Message);
        g.ReleaseHdc(hdc);
        g.Dispose();
        return;
    }

    // Create a Graphics object from the Metafile object
    Graphics g1 = Graphics.FromImage(curMetafile);

    // Set smooting mode
    g1.SmoothingMode = SmoothingMode.HighQuality;

    // Fill a rectangle on the Metafile object
    g1.FillRectangle(Brushes.Green, rect);
    rect.Y += 110;

    // Draw an ellipse on the Metafile object
    LinearGradientBrush lgBrush =
    new LinearGradientBrush(
    rect, Color.Red, Color.Blue, 45.0f);
    g1.FillEllipse(lgBrush, rect);

    // Draw text on the Metafile object
    rect.Y += 110;
    g1.DrawString("MetaFile Sample",
    new Font("Verdana", 20),
    lgBrush, 200, 200,
    StringFormat.GenericTypographic);

    // Release objects
    g.ReleaseHdc(hdc);
    g1.Dispose();
    g.Dispose();
}
```

### 在 Form1.cs Design 上增加一個 Button, 其 Properties 內 Events 找到 Click  

將 Click 設定為 CreateMetaFile_Click, 在 Form1.Designer.cs 內會自動生成以下程式碼

``` cs
this.button1.Click += new System.EventHandler(this.CreateMetaFile_Click);
```

# 參考來源

- [How to Add Graphics to a C# Windows Form Application](https://www.makeuseof.com/c-sharp-windows-form-graphics/)
- [如何：將現有點陣圖描繪至螢幕](https://learn.microsoft.com/zh-tw/dotnet/desktop/winforms/advanced/how-to-draw-an-existing-bitmap-to-the-screen?view=netframeworkdesktop-4.8)
- [Working with Metafiles in GDI+](https://www.c-sharpcorner.com/uploadfile/mahesh/working-with-metafiles-in-gdi/)