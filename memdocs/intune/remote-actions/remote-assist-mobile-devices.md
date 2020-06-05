---
# required metadata

title: Remotely assist mobile devices managed by Intune 
description: You can use a four different options to remotely assist users with their mobile devices.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

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
- [Remote control](https://docs.microsoft.com/configmgr/core/clients/manage/remote-control/introduction-to-remote-control) is included in Microsoft Endpoint Configuration Manager. It's used to remotely administer, provide assistance, or view any workgroup computer and domain-joined computer.

| Features, Platforms, Licensing | **Teams** | Quick Assist | TeamViewer (Intune) | Remote control (ConfigMgr) |
|:---:|:---:|:---:|:---:|:---:|
| Remote view and control |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Chat |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||
| File transfer |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Elevated admin access |||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Unattended access |||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Simultaneous remote control |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Multi-user support |||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Remote actions ||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Over-the-internet support |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Audit reporting |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Support for all platforms (Windows, iOS, Android, macOS) |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||
| Integrated with Windows 10 – no additional app required ||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|||
| Requires device to be co-managed by Configuration Manager and Intune ||||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|
| Requires additional licensing\* |![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)||![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|![Checkmark](../enrollment/media/enrollment-method-capab/checkmark.png)|

\* Teams requires O365 or M365 licensing. Use of TeamViewer and Intune requires licensing from both TeamViewer and Intune. Remote Control is a feature of Configuration Manager and requires Configuration Manager licensing.
