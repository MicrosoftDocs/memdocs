---
description: Learn how to use lazy properties, which are properties that exist and contain data, but the data isn't available through the SMS Administrator console.
title: SMS object lazy properties
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: b6eb9f5c-78a8-4ded-b032-5d8c4f533694
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Lazy Properties
A few SMS object properties are described as lazy. This means that the property exists and contains data, but the data isn't available through the SMS Administrator console. In practical terms, the property isn't visible in Query Builder.  

 The lazy properties generally contain data that is useless when displayed in the SMS Administrator console. For example, the **Icon[ ]** property in **SMS_PDF_Package** is an array of icon data that appears in the SMS Administrator console as a large amount of uninterpretable numeric data.  

 Lazy properties can be accessed programmatically if you have an application that requires the data that they store. The data can only be retrieved by explicitly calling **GetInstance** on the object.
