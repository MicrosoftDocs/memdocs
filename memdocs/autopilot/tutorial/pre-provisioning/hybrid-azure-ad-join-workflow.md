---
title: Overview for Windows Autopilot for pre-provisioned deployment hybrid Azure AD join in Intune
description: Overview for Windows Autopilot for pre-provisioned deployment hybrid Azure AD join in Intune.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
---

# Step by step tutorial for Windows Autopilot for pre-provisioned deployment hybrid Azure AD join in Intune

This step by step tutorial guides you through using Intune to perform a Windows Autopilot for pre-provisioned deployment scenario when the devices are also joined to an on-premises domain, also known as hybrid Azure AD join.

The purpose of this tutorial is to provide a step by step guide for all the steps required for the configuration for a successful Autopilot for pre-provisioned deployment hybrid Azure AD join deployment using Intune. The tutorial is also designed as a walkthrough in a lab or testing scenario, but can be expanded for use in a production environment.

Before beginning, refer to the [Plan your hybrid Azure Active Directory join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan) to make sure all prerequisites are met for joining on-premises AD devices to Azure AD.

> [!NOTE]
>
> Since Windows Autopilot for pre-provisioned deployment hybrid Azure AD join builds on top of [Windows Autopilot hybrid user-driven Azure AD join](../user-driven/hybrid-azure-ad-join-workflow.md), it's strongly recommended that the Windows Autopilot hybrid user-driven Azure AD join scenario is setup, tested, and working first before attempting to use the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join scenario. If the Windows Autopilot user-driven hybrid Azure AD join doesn't work, then most likely the Windows Autopilot pre-provisioned deployment hybrid Azure AD join scenario won't work either.

## Workflow

Set up Windows automatic Intune enrollment > Install the Intune Connector > Increase the computer account limit in the Organizational Unit (OU) > Register devices as Autopilot devices > Create a device group > Configure and assign Autopilot Enrollment Status Page (ESP) > Create and assign hybrid Azure AD join Autopilot profile > Configure and assign domain join profile > Assign Autopilot device to a user (optional) > Technician flow > User flow

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
> [!div class="checklist"]
> - Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
> - Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
> - Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
> - Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
> - Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
> - Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
> - Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
> - Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
> - Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
> - Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
> - Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

> [!NOTE]
>
> Although the workflow is designed for lab or testing scenarios, it can also be used in a production environment. Some of the steps in the workflow are interchangeable and interchanging some of the steps may make more sense in a production environment. For example, the **Create a device group** step followed by the **Register devices as Autopilot devices** step may make more sense in a production environment.

## Walkthrough

> [!div class="nextstepaction"]
> [Step 1: Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)

## More information

For more information on Windows Autopilot for pre-provisioned deployment hybrid Azure AD join, see the following article(s):

- [Windows Autopilot for pre-provisioned deployment](/mem/autopilot/pre-provision)
- [Deploy hybrid Azure AD-joined devices by using Intune and Windows Autopilot](/mem/autopilot/windows-autopilot-hybrid)
