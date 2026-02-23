---
description: Learn how to use lazy properties, which are properties that exist and contain data, but the data isn't available through the SMS Administrator console.
title: SMS object lazy properties
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: article
ms.collection: tier3
---
# Lazy Properties
A few SMS object properties are described as lazy. This means that the property exists and contains data, but the data isn't available through the SMS Administrator console. In practical terms, the property isn't visible in Query Builder.

 The lazy properties generally contain data that is useless when displayed in the SMS Administrator console. For example, the **Icon[ ]** property in **SMS_PDF_Package** is an array of icon data that appears in the SMS Administrator console as a large amount of uninterpretable numeric data.

 Lazy properties can be accessed programmatically if you have an application that requires the data that they store. The data can only be retrieved by explicitly calling **GetInstance** on the object.
