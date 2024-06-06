---
title: include file
description: include file
author: MandiOhlinger
ms.service: microsoft-intune
ms.topic: include
ms.date: 02/27/2024
ms.author: mandia
ms.custom: include file
ms.reviewer: miepping
---

<!-- This include file is used in the Apple Enterprise SSO deployment guide docs. -->

## Microsoft Enterprise SSO plug-in vs. Kerberos SSO extension

When you use the SSO app extension, you use the **SSO** or **Kerberos** Payload Type for authentication. The SSO app extension is designed to improve the sign-in experience for apps and websites that use these authentication methods.

The Microsoft Enterprise SSO plug-in uses the **SSO** Payload Type with **Redirect** authentication. The SSO Redirect and Kerberos extension types can both be used on a device at the same time. Be sure to create separate device profiles for each extension type you plan to use on your devices.

To determine the correct SSO extension type for your scenario, use the following table:

---
| Microsoft Enterprise SSO plug-in for Apple Devices | Single sign-on app extension with Kerberos |
| --- | --- |
| Uses the **Microsoft Entra ID** SSO app extension type | Uses the **Kerberos** SSO app extension type |
| Supports the following apps: <br/> - Microsoft 365 <br/> - Apps, websites or services integrated with Microsoft Entra ID | Supports the following apps: <br/> - Apps, websites or services integrated with AD <br/> <br/> |
