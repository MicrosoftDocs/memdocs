---
title: IProgressUI::CloseProgressDialog
titleSuffix: Configuration Manager
description: IProgressUI::CloseProgressDialog method
ms.date: 04/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual


ms.assetid: ab7508e4-0976-4217-b701-ca76e4a583ce
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# IProgressUI::CloseProgressDialog method

In Configuration Manager, the `CloseProgressDialog` method closes open instances of `IProgressUI`.

## Syntax  

```  
[IDL]  
HRESULT CloseProgressDialog();  
```  

## Parameters

None

## Return values

An `HRESULT` code. Possible values include, but aren't limited to, the following value. There are no `HRESULT` values returned that are specific to this method.

S_OK  
The method succeeded.  

## See also

- [OS deployment client COM automation classes](operating-system-deployment-client-com-automation-classes.md)  

- [IProgressUI interface](iprogressui-interface.md)  

- [About reporting Configuration Manager custom action progress](../../../../osd/about-reporting-configuration-manager-custom-action-progress.md)  

- [How to use task sequence variables in a running Configuration Manager task sequence](../../../../osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  
