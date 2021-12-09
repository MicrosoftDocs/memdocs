---
title: "Handle Synchronous Errors by Using WMI"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: d11bbdc3-f47e-4088-bed8-7e38d119e278
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Handle Configuration Manager Synchronous Errors by Using WMI
You handle synchronous errors, in Configuration Manager, by inspecting the `SWbemLastError` object when an error occurs. An error has occurred when the error object `Number` property is non-zero.  

> [!NOTE]
>  In VBScript you should declare that you want to resume running the script if an error occurs. Otherwise, the script will end when an error condition occurs. To do this, use the `On Error Resume Next` declaration in your script.  

## Example  
 The following VBScript example displays the most recent error information that is available from the `SWbemLastError` object. You can use the following code, which tries to get an invalid SMS_Package package to test it.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub ExerciseError(connection)  

    On Error Resume next  

    Dim packages  
    Dim package  

    ' Run the query.  
    Set package = connection.Get("SMS_Package.PackageID='UNKNOWN'")  

    If Err.Number<>0 Then  
        Call DisplayLastError  
    End If  

End Sub      
```  

```vbs  

Sub DisplayLastError  
    Dim ExtendedStatus  

    ' Get the error object.  
    Set ExtendedStatus = CreateObject("WbemScripting.SWBEMLastError")  

    ' Determine the type of error.  
    If ExtendedStatus.Path_.Class = "__ExtendedStatus" Then  
        WScript.Echo "WMI Error: "& ExtendedStatus.Description              
    ElseIf ExtendedStatus.Path_.Class = "SMS_ExtendedStatus" Then  
        WScript.Echo "Provider Error: "& ExtendedStatus.Description  
        WScript.Echo "Code: " & ExtendedStatus.ErrorCode  
    End If  
End Sub  

```  

## See Also  
 [About errors](about-configuration-manager-errors.md)\
 [WMI SDK](/windows/win32/wmisdk/wmi-start-page)
