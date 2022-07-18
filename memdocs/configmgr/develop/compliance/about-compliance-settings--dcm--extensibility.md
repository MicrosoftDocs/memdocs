---
title: "About Compliance Settings Extensibility"
description: The content in this section provides information about extending the functionality of desired configuration management configuration items in Configuration Manager.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 0f9532cc-058c-46cf-8181-469cd6e1734b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Compliance Settings (DCM) Extensibility
The content in this section provides information about extending the functionality of desired configuration management configuration items in Configuration Manager.  

 In application configuration items, it is possible to detect applications or settings by using a script.  

 If the script returns a non-zero exit code, the result will be a discovery failure.  

 If the script returns a zero exit code, the script output will be evaluated.  

 It is the echoed output of a script that is detected and evaluated. For example:  

- No echoed output equals no instances detected.  

- "n" lines of output equals "n" instances detected.  

  In the case of application detection, two lines of output would indicate that two instances of the application are detected.  

  In the case of settings detection, no lines of output would indicate that no instances of the setting are detected.  

  In all cases, the evaluation of the script output is determined by the rule.  

> [!NOTE]
>  In the case of settings detection, the script output is cast to the type of setting being detected. If the cast of the script output fails, a discovery failure is returned. For example, a script that reads and returns registry values, passes a set of values back to the rule; however, one value is a string (1, 2, x). If the rule is expecting only integer values back, it will cast all of the values to integers, causing a failure. In this case, the rule returns an evaluation failure.  

