---
title: "Lazy Properties"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: b6eb9f5c-78a8-4ded-b032-5d8c4f533694searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Lazy Properties
A small number of SMS object properties are described as lazy. This means that the property exists and contains data, but the data is not available through the SMS Administrator console. In practical terms, the property is not visible in Query Builder.  

 The lazy properties generally contain data that is useless when displayed in the SMS Administrator console. For example, the **Icon[ ]** property in **SMS_PDF_Package** is an array of icon data that appears in the SMS Administrator console as a large amount of uninterpretable numeric data.  

 Lazy properties can be accessed programmatically if you have an application that requires the data that they store. The data can only be retrieved by explicitly calling **GetInstance** on the object.
