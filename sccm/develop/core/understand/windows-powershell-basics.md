---
title: "Windows PowerShell Basics"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 519ea4d0-94ed-4fff-beec-edb99e6089e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Windows PowerShell Basics
System Center 2012 Configuration Manager SP1 introduced native PowerShell support. Windows PowerShell is Microsoft’s approach to automation and is being implemented across all System Center products. This topic will introduce you to some of the basics of using Windows PowerShell with Configuration Manager.  

 First, you need to make sure that Windows PowerShell 3.0 or later is installed. If Windows PowerShell 3.0 or later is not installed, you can download the latest version of  Windows PowerShell as part of the [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395).  

 To get started:  

1.  Hit your Windows key and type “PowerShell��?.  

2.  From the results, right-click Windows PowerShell and choose “Run as administrator��?.  

3.  You should now see a Windows PowerShell command prompt.  

     ![Windows PowerShell command prompt](../../../develop/core/understand/media/powershellv5window.png "PowerShellv5Window")  

> [!TIP]
>  The Windows PowerShell command prompt is a fully functional command prompt. As you get started with Windows PowerShell, get used to opening up the Windows PowerShell command prompt even for non-Windows PowerShell specific tasks, such as ‘ping’ or ‘ipconfig’. You may find that this helps integrate Windows PowerShell into your normal workflow, and that the tips and tricks you pick up along your Windows PowerShell journey will be more readily at hand.  

## Concepts  
 Below are a few basic Windows PowerShell concepts to get you started on your journey:  

-   The Cmdlet  

-   The Variable  

-   The Module  

## The Cmdlet  
 “Cmdlet��? is also sometimes referred to as “Command-let��?.  The cmdlet is a basic instruction that you give Windows PowerShell.  All cmdlets are made up of two parts: a verb and a noun. They are separated by a hyphen ‘-‘ character. Cmdlets are the building blocks of Windows PowerShell and are what do all the work for you.  Some cmdlets come with Windows, and others are installed with programs like Configuration Manager. An example of a Windows cmdlet that restarts a print job is: **Restart-PrintJob**. An example of a Configuration Manager cmdlet that retrieves a Configuration Manager site is: **Get-CMSite**.  

 Before we jump into our second concept, let’s try a few cmdlets that retrieve (**Get**) data.  

 Go to your Windows PowerShell window, and type `Get-Service`, `Get-UICulture` and `Get-Date`:  

```  
PS C:\> Get-Service  
Note: This cmdlet returns the current list of services (not listed here).  

PS C:\> Get-UICulture  
LCID             Name             DisplayName  
----             ----             -----------  
1033             en-US            English (United States)  

PS C:\> Get-Date  
Tuesday, August 30, 2016 2:02:14 PM  

```  

 Besides retrieving information, Windows PowerShell can perform actions.  

> [!WARNING]
>  For this next part, there are different commands to try depending on the version of Windows you’re using.  

### For all versions of Windows and Windows Server  
 Go to your Windows PowerShell window, and type `Get-Location`, and `Get-History`:  

```  
PS C:\> Get-Location  
Path  
----  
C:\   
PS C:\> Get-History  
Id CommandLine  
-- -----------  
1 get-service  
2 get-uiculture  
3 get-date  
4 get-location  

```  

 The output of `Get-History` returns a list of commands that you’ve previously typed.  

 Now, instead of retrieving information (`Get`), let’s take action and clear the history using `Clear-History`.  

```  
PS C:\> Clear-History  
PS C:\>  
```  

 Now, if you type `Get-History` to retrieve the list of previously entered commands, you should see only `Clear-History`:  

```  
PS C:\> Get-History   
Id CommandLine  
-- -----------  
 5 clear-history  

```  

### For Windows 8 and Windows Server 2012 or Later  
 Another example of retrieving information (`Get`) using a cmdlet, taking action (`Enable/Disable`), and verifying state by retrieving information (`Get`) is listed below. This example uses various Windows Error Reporting cmdlets – notice how the basic noun (WindowsErrorReporting) remains the same, while the verb (Get/Enable/Disable) changes.  

 Go to your Windows PowerShell window, and type `Get-WindowsErrorReporting`:  

```  
PS C:\> Get-WindowsErrorReporting  
Enabled  
```  

 `Get-WindowsErrorReporting` returns the current state, which in this case is `Enabled`. There are specific cmdlets to enable or disable Windows Error Reporting. As an example of taking action using a cmdlet, use the `Disable-WindowsErrorReporting` cmdlet to disable Windows Error Reporting.  

> [!NOTE]
>  If you are not running Windows PowerShell as an administrator, you may not be able to change the value. In this case, the the `Disable-WindowsErrorReporting` cmdlet will return `False`, instead of `True` after running the cmdlet.  

 Go to your Windows PowerShell window, and type `Disable-WindowsErrorReporting`:  

```  
PS C:\> Disable-WindowsErrorReporting  
True  
PS C:\>  
```  

 To check the state of Windows Error Reporting, retrieve (Get) the current state by using the `Get-WindowsErrorReporting` cmdlet:  

```  
PS C:\> Get-WindowsErrorReporting  
Disabled  
```  

 To re-enable Windows Error Reporting, go to your Windows PowerShell window, and type `Enable-WindowsErrorReporting`:  

```  
PS C:\> Enable-WindowsErrorReporting  
True  
```  

 You’ve now successfully run several Windows PowerShell cmdlets, retrieving information and taking action.  

## The Variable  
 In Windows PowerShell, variables are quite powerful. You can store all kinds of data in a PowerShell variable, not just text and numbers, but also objects.  

### For Windows 7 and Windows Server 2008 or Later  
 In a previous example, you saw how `Get-Location` returned the current path.  That path can be stored in a Windows PowerShell variable for later use.  

 To store the result of a cmdlet, we need a variable. Variables all start with a $. To define a variable, simply identify it with a $ at the front, for example `$MyPath`.  

 Go to your Windows PowerShell window, and type `Get-Location`, and `$MyPath`:  

```  
PS C:\> Get-Location  
Path  
----  
C:\  
PS C:\> $MyPath  
PS C:\>  

```  

 To save the results from our `Get-Location` cmdlet into a variable, just assign the results of the cmdlet to the variable.  

```  
PS C:\> $MyPath = Get-Location  
PS C:\>  
```  

 The result of `Get-Location` are now stored in `$MyPath`. To see the value of the `$MyPath` variable, type the variable name and press Enter.  

```  
PS C:\> $MyPath  
Path  
----  
C:\  
PS C:\   
```  

### For Windows 8 and Windows Server 2012 or Later  
 In a previous example, you saw that the `Get-WindowsErrorReporting` cmdlet returned a value of `Enabled` (or `Disabled`). Windows PowerShell can store the results of the cmdlet in a variable. To store the result of a cmdlet, we need a variable. Variables all start with a $. To define a variable, simple identify it with a $ at the front, for example `$WERState`.  

 Go to your Windows PowerShell window, and type `$WERState`:  

```  
PS C:\> $WERState  
PS C:\>  
```  

 To save the results from our `Get-WindowsErrorReporting` cmdlet into a variable, just assign the results of the cmdlet to the variable.  

```  
PS C:\> $WERState = Get-WindowsErrorReporting  
PS C:\>  
```  

 The result of `Get-WindowsErrorReporting` are now stored in `$WERState`. To see the value of the `$WERState` variable, type the variable name and press Enter.  

```  
PS C:\> $WERState  
PS C:\> Enabled  
```  

 There are lots more things you can do with variables – but we’ve covered the most important concepts you’ll need in the beginning.  

## The Module  
 The last concept we'll cover here is the Module.  All Windows PowerShell cmdlets are coded and stored in a module.  The modules for Windows are available by default in your Windows PowerShell window. You can add modules to your Windows PowerShell session by importing them using the `Import-Module` cmdlet.  An example of importing a module is contained in the topic [Connecting to Configuration Manager with Windows PowerShell](../../../develop/core/understand/connecting-to-configuration-manager-with-windows-powershell.md).  

## Further Exploring  
 Now that we've covered these three basic concepts, try using the `Show-Command` cmdlet to browse Windows PowerShell cmdlets from all the modules currently installed.  

```  
PS C:\> Show-Command  
```  

 If you want to learn more Windows PowerShell basics, jump over to  [Getting Started with Windows PowerShell](https://msdn.microsoft.com/powershell/scripting/getting-started/getting-started-with-windows-powershell).  

## See Also  
 [Getting Started with Configuration Manager and Windows PowerShell](../../../develop/core/understand/getting-started-with-configuration-manager-and-windows-powershell.md)
