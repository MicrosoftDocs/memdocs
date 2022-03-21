---
# required metadata

title: Remotely assist mobile devices managed by Intune 
description: You can use a four different options to remotely assist users with their mobile devices.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 11/22/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Remotely assist mobile devices managed by Microsoft Endpoint Manager

There are four options available for remotely administering devices managed by  Microsoft Endpoint Manager:

- [Microsoft Teams](https://products.office.com/microsoft-teams/) is the hub for teamwork where you can chat, meet, and collaborate no matter where you are.
- [Quick Assist](https://support.microsoft.com/help/4027243/windows-10-solve-pc-problems-with-quick-assist) is a Windows 10 application that lets two people share a device over a remote connection.
- [TeamViewer](https://www.teamviewer.com/) is a third-party program that you purchase separately. It provides a comprehensive set of remote access and support capabilities. The Intune and [TeamViewer integration](teamviewer-support.md) enables remote support using TeamViewer and the connector is managed directly in Intune.
- [Remote help](remote-help.md) is in public preview for Microsoft Endpoint Manager. When installed on a users device, your organizations users can provide remote assistance to other users within the same tenant, including between devices that are and aren't enrolled with Intune.
- [Remote control](/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) is included in Microsoft Endpoint Configuration Manager. It's used to remotely administer, provide assistance, or view any workgroup computer and domain-joined computer.

| Features, Platforms, Licensing | **Teams** | Quick Assist | TeamViewer (Intune) | Remote help (*preview*) | Remote control (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|:---:|
| Remote view and control |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)||
| File transfer |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Elevated admin access |  |  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Unattended access |||![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png) \**|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Simultaneous remote control |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |  |  |
| Multi-user support |||![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Remote actions ||![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Over-the-internet support |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |
| Audit reporting |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Support for all platforms (Windows, iOS, Android, macOS) |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |  |
| Integrated with Windows 10 – no additional app required |  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |  |  |
| Requires device to be co-managed by Configuration Manager and Intune |  |  |  |  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Requires additional licensing\* |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|  |![Checkmark icon alt-text="Checkmark icon"](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams requires Microsoft 365 licensing. Use of TeamViewer and Intune requires licensing from both TeamViewer and Intune. Remote Control is a feature of Configuration Manager and requires Configuration Manager licensing.

\** Unattended access can be initiated from the TeamViewer Management Console, but not from the Microsoft Endpoint Manager admin center.
