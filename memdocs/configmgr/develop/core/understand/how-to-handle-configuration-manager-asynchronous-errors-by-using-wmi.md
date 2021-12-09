---
title: "Handle Asynchronous Errors by Using WMI"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 6371b349-5bd0-41c5-93e8-14157c053417
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Handle Configuration Manager Asynchronous Errors by Using WMI
In Configuration Manager, when an error occurs in an asynchronous call, the error object is passed as the second parameter to the `OnCompleted` method. Inside your `OnCompleted` implementation, you check the error object the same as you would for a synchronous call.  

 You determine if there is an error by checking the `HResult` parameter of the `OnCompleted` method.  

## Example  
 This VBScript sample displays error information if there is a error during an asynchronous operation. To test, change the query to an invalid query such as `Select * From ?????`.  

 For information about calling the sample code, see [Calling Configuration Manager Code Snippets](../../../develop/core/understand/calling-code-snippets.md).  

```vbs  

Sub sink_OnCompleted(HResult, oErr, oCtx)  
    WScript.Echo "All collections returned"  

    if HResult <> 0 Then   
    ' Determine the type of error.  
        If oErr.Path_.Class = "__ExtendedStatus" Then  
            WScript.Echo "WMI Error: "& oErr.Description              
        ElseIf ExtendedStatus.Path_.Class = "SMS_ExtendedStatus" Then  
            WScript.Echo "Provider Error: "& oErr.Description  
            WScript.Echo "Code: " & oErr.ErrorCode  
        End If  
    End If      
    bdone = true  
End sub  

```  

## .NET Framework Security  
 Using script to pass the user name and password is a security risk and should be avoided where possible.  

## See Also  
 [About errors](about-configuration-manager-errors.md)\
 [WMI SDK](/windows/win32/wmisdk/wmi-start-page)   
 [How to Handle Configuration Manager Synchronous Errors by Using WMI](../../../develop/core/understand/how-to-handle-configuration-manager-synchronous-errors-by-using-wmi.md)
