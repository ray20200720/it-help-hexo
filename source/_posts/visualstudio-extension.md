title: 開發Visual Studio 2019 延伸模組範例
date: 2024-01-05 14:32
categories: Visual Studio, Extension
---------------------------------------

想了解怎麼開發Visual Studio的延伸模組(Extension)

# 安裝 Visual Studio SDK

啟動 `Visual Studio Installer`, 點選 `修改`

![Visual Studio Installer](pic/VSIX/installer.png)

在 `工作負載` 頁籤 找到 `Visual Studio 擴充功能開發`, 勾選後點 `關閉` 進行安裝

![Visual Studio SDK](pic/VSIX/sdk.png)

# 建立新專案名稱為 HelloWorld

Step 1. From the File menu, select New > Project. Search for "vsix" and select the Visual C# VSIX Project and then Next.

Step 2. Enter "HelloWorld" for the Project name and select Create.

# Add a custom command

Step 1. If you select the .vsixmanifest manifest file, you can see what options are changeable, such as description, author, and version.

Step 2. Right-click the project (not the solution). On the context menu, select Add, and then New Item.

Step 3. Select the Extensibility section, and then choose Command.

Step 4. In the Name field at the bottom, enter a filename such as Command.cs.

Your new command file is visible in Solution Explorer. Under the Resources node, you'll find other files related to your command. For example, if you wish to modify the image, the PNG file is here.

# Modify the source code

Step 1. In Solution Explorer, find the VSCT file for your extension VS package. In this case, it will be called HelloWorldPackage.vsct.

Step 2. Change the ButtonText parameter to Say Hello World!.

``` cs
  <Button guid="guidCommandPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidCommandPackageCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
        <ButtonText>Say Hello World!</ButtonText>
     </Strings>
  </Button>
```
Step 3. Go back to Solution Explorer and find the Command.cs file. In the Execute method, change the string message from string.Format(..) to Hello World!.

``` cs
  private void Execute(object sender, EventArgs e)
  {
    ThreadHelper.ThrowIfNotOnUIThread();
    string message = "Hello World!";
    string title = "Command";

    // Show a message box to prove we were here
    VsShellUtilities.ShowMessageBox(
        this.ServiceProvider,
        message,
        title,
        OLEMSGICON.OLEMSGICON_INFO,
        OLEMSGBUTTON.OLEMSGBUTTON_OK,
        OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST);
  }
```

# Run it

ou can now run the source code in the Visual Studio Experimental Instance.

Step 1. Press F5 to run the Start Debugging command. This command builds your project and starts the debugger, launching a new instance of Visual Studio called the Experimental Instance.

Step 2. On the Tools menu of the Experimental Instance, click Say Hello World!.

# How to reset Experimental instance of Visual Studio

執行底下的捷徑

``` sh
C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019\Microsoft Visual Studio SDK\Tools\Reset the Visual Studio 2019 Experimental Instance
```

# 參考來源

- [Install the Visual Studio SDK](https://learn.microsoft.com/en-us/visualstudio/extensibility/installing-the-visual-studio-sdk?view=vs-2022)
- [Tutorial - Create your first extension: Hello World](https://learn.microsoft.com/en-us/visualstudio/extensibility/extensibility-hello-world?view=vs-2022)
- [Resetting Experimental instance of Visual Studio](https://stackoverflow.com/questions/54958880/resetting-experimental-instance-of-visual-studio)