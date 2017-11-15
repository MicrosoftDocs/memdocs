---
title: "CNG certificates overview"
titleSuffix: "Configuration Manager"
description: "An overview of CNG certificates in Configuration Manager"
ms.custom: na
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 
author: vhorne
ms.author: victorh
manager: angrobe

---

# CNG certificates overview
<!-- 1356191 --> 
You can use [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) certificate templates for the following scenarios:

- Client registration and communication with an HTTPS management point.   
- Software distribution and application deployment with an HTTPS distribution point.   
- Operating system deployment.  
- Client messaging SDK (with latest update) and ISV Proxy.   
- Cloud Management Gateway configuration.  

To use CNG certificates, your certification authority (CA) needs to provide CNG certificate templates for target machines.  Template details vary according to the scenario; however, the following properties are required:

- **Compatibility** tab

    - **Certificate Authority** must be Windows Server 2008 or later. (Windows Server 2012 is recommended.)

    - **Certificate recipient** must be Windows Vista/Server 2008 or later. (Windows 8/Windows Server 2012 is recommended.)

- **Cryptography** tab

    - **Provider Category** must be **Key Storage Provider**.  (Required)

For best results, we recommend building the Subject Name from Active Directory information.  Use the DNS Name for **Subject name format** and include the DNS name in the alternate subject name.  Otherwise, you have to provide this information when the device enrolls into the certificate profile.