---
# required metadata

title: Validate your app protection policy setup
titleSuffix: Microsoft Intune
description: Learn how to test that your app protection policy is set up and working correctly in Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/31/2023
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.topic: how-to
ms.technology:
ms.assetid: 15f8a838-0b69-412b-a42e-c6edb61f0cae

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# How to validate your app protection policy setup in Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Validate that your app protection policy is correctly set up and working. This guidance applies to app protection policies in the portal.

## Checking for symptoms
Users are unlikely to report issues since app protection is a data protection tool. If there's a problem with the app protection configuration, the user will have unrestricted access, as they would have without app protection, and they wouldn't know there's an issue. For this reason, we recommend you validate your app protection configuration by piloting your app protection policies with a small group of users who can deliberately test the app protection restrictions.

## What to check

If testing shows that your app protection policy behavior isn't functioning as expected, check these items:

- Are the users licensed for app protection?
- Are the users licensed for Microsoft 365?
- Is the status of each of the users' app protection apps as expected. The possible statuses for the apps are **Checked in** and **Not checked in**.

### User app protection status
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Select **Apps** > **Monitor** >  **App protection status**, and then select the **Assigned users** tile. 
4. On the **App reporting** page, select **Select user** to bring up a list of users and groups. 
5. Search for and select a user from the list, then choose **Select user**. At the top of the **App reporting** pane, you can see whether the user is licensed for app protection. You can also see whether the user has a license for Microsoft 365 and the app status for all of the user's devices.

## What to do
Here are the actions to take based on the user status:

- If the user isn't licensed for app protection, assign an [Intune license](../fundamentals/licenses.md) to the user.
- If the user isn't licensed for Microsoft 365, get a [license](../fundamentals/licenses.md) for the user.
- If a user's app is listed as **Not checked in**, check if you've correctly configured an [app protection policy](app-protection-policies-validate.md) for that app.
- Ensure that these conditions apply across all users to which you want [app protection policies](app-protection-policies-monitor.md) to apply.

## See also

- [What is Intune app protection policy?](app-protection-policies.md)
- [Licenses that include Intune](../fundamentals/licenses.md)
- [Assign licenses to users so they can enroll devices in Intune](../fundamentals/licenses-assign.md)
- [How to validate your app protection policy setup](app-protection-policies-validate.md)
- [How to monitor app protection policies](app-protection-policies-monitor.md)

