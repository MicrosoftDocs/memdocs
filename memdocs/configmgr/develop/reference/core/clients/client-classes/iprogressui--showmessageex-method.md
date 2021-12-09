---
title: IProgressUI::ShowMessageEx
titleSuffix: Configuration Manager
description: IProgressUI::ShowMessageEx method
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 24a048fc-c8dc-4fc5-a094-4e4e4d0ada64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# IProgressUI::ShowMessageEx method

<!--6448458-->

Starting in version 2006, the `ShowMessageEx` method displays a customizable dialog box. This method is similar to the [IProgressUI::ShowMessage](iprogressui--showmessage-method.md) method, but also includes a new integer result variable, **pResult**.

## Syntax  

```
[IDL]  
HRESULT ShowMessageEx(  
     BSTR pszText,  
     BSTR pszCaption,  
     ULONG uType,
     INT *pResult
);  
```  

### Parameters  

#### `pszText`

Data type: `BSTR`  

Qualifiers: [in]

The text displayed in the message box body.
  
#### `pszCaption`

Data type: `BSTR`  

Qualifiers: [in]  

The text displayed in the message box windows header.

#### `uType`

Data type: `ULONG`  

Qualifiers: [in]

The value corresponding to one of the following possible values for the buttons:

- 0 - Ok
- 1 - Ok/Cancel
- 2 - Abort/Retry/Ignore
- 3 - Yes/No/Cancel
- 4 - Yes/No
- 5 - Retry/Cancel
- 6 - Cancel/Try Again/Continue

#### `pResult`

Data type: `INT`

Qualifiers: [out]

The value of this variable is a standard [Windows message box return value](/windows/win32/api/winuser/nf-winuser-messagebox#return-value).

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.

S_OK  
The method succeeded.  

To evaluate the user's response to the message box, use the [pResult](#presult) parameter.

## Example

The following PowerShell script sample shows how to use this method:

```PowerShell
$Message = "Can you see this message?"
$Title = "Contoso IT"
$Type = 4 # Yes/No
$Output = 0

$TaskSequenceProgressUi = New-Object -ComObject "Microsoft.SMS.TSProgressUI"
$TaskSequenceProgressUi.ShowMessageEx($Message, $Title, $Type, [ref]$Output)

$TSEnv = New-Object -ComObject "Microsoft.SMS.TSEnvironment"
if ($Output -eq 6) {
$TSEnv.Value("TS-UserPressedButton") = 'Yes'
}
```

You can use a script like this in the [Run PowerShell Script](../../../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) step in the task sequence. If the user selects **Yes** in the custom window, the script creates a custom task sequence variable **TS-UserPressedButton** with a value of `Yes`. You can then use this task sequence variable in other scripts or as a condition on other task sequence steps.

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)
