---
title: "Report Custom Action Progress"
titleSuffix: "Configuration Manager"
description: "A custom action can report progress information that is used to display a progress indicator."  
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e1fe4037-cd2a-416d-afe4-8a2de2ba4f33
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Reporting Configuration Manager Custom Action Progress
While a custom action is running on a Configuration Manager client, it can report progress information that is used to display a progress indicator.  

 You use the COM automation interface, [IProgressUI::ShowActionProgress](../../develop/reference/core/clients/client-classes/iprogressui--showactionprogress-method.md), to report progress information to the task sequence environment and to show a progress indicator.  

 `IProgressUI::ShowActionProgress` is implemented in the COM class, [ProgressUI](../../develop/reference/core/clients/client-classes/progressui-client-com-automation-class.md), which is an out-of-process COM object in TSProgressUI.exe.  

## ProgressUI in the Task Sequence Environment  
 Before the task sequence runs, `ProgressUI` is registered and then, when the task sequence finishes, it is unregistered. In the source operating system, `ProgressUI` runs under the logged-on user credentials. If no user is logged in when the task sequence runs, the registration for the COM object fails. In the target operating system, and in Windows PE, `ProgressUI` runs under the system account.  

## Calling IProgressUI::ShowActionProgress  
 In your custom action you must do the following to report the progress of your custom action and display a progress indicator.  

> [!NOTE]
>  Typically, you should report progress information if the action takes more than one minute to run.  

### Determining Whether the Progress Indicator Should Be Displayed  
 Using the following logic, you can use environment variables to determine whether the progress indicator should be displayed.  

 If you are running in WindowsPE ( `_SMSTSInWinPE` == "true"), or  

 If you are running in full operating system post installation (`_SMSTSReturnToGINA`=="true"), or  

 If the task sequence is started from media (`_SMSTSLaunchMode` is "CD", "DVD" or "USB"), or  

 If the task sequence is running in stand-alone mode (`_SMSTSStandAloneMode`=="true"), or  

 If the show progress UI flag is set (`_SMSTSShowProgressUI` == "true"), the progress indicator should be displayed; otherwise, it should not be displayed.  

### Creating the COM ProgressUI Object  
 You create a `ProgressUI` object by using the same technique that you use with any COM object. In C++ you use `CoCreateInstance`. In C# you add a reference to **SMS TSE Progress UI,** and in your source code you create an instance of the `ProgressUILib.ProgressUIClass` class.  

 In VBScript, call `CreateObject` with **Microsoft.SMS.TsProgressUI**.  

 For an example of creating a COM object in VBSript and C#, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-specify-the-supported-platforms-for-a-driver.md).  

### Getting the Required Environment Variables  
 Several environment variables contain information that you must pass to the `IProgressUI::ShowActionProgress` method. For example, the organization name that is needed for the `pszOrgName` parameter is available from the environment variable, `_SMSTSOrgName`. For more information, see [IProgressUI::ShowActionProgress](../../develop/reference/core/clients/client-classes/iprogressui--showactionprogress-method.md). For information about reading task sequence environment variables, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).  

### Calling IProgressUI::ShowActionProgress  
 Call `IProgressUI::ShowActionProgress` to show the progress indicator by using the information that is retrieved from the environment variables. To pass the current percentage progress, you use the parameters `uActionExecStep` and `uActionExecMaxStep`. For example, if you pass the value 2 in `uActionExecStep` and pass the value 10 in `uActionExecMaxStep`, then the percentage completion of the action is 20 percent.  

## See also

 [IProgressUI::ShowActionProgress](../../develop/reference/core/clients/client-classes/iprogressui--showactionprogress-method.md)
 [ProgressUI](../../develop/reference/core/clients/client-classes/progressui-client-com-automation-class.md)
