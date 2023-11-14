---
# required metadata

title: Try new Devices experience in Microsoft Intune 
description: Walk through the new Devices workload, now in public preview in the Microsoft Intune admin center.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/15/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: 
ms.localizationpriority: medium

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Try new Devices experience in Microsoft Intune

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Enroll devices, manage profiles and policies, and access monitoring and reports all in one place in Microsoft Intune. Now in public preview, you can go to the **Devices** area in the Microsoft Intune admin center to:

* Get at-a-glance actionable information and key metrics about your devices.  
* Access workloads for device onboarding, management, and monitoring.
* View, monitor, and drill down into active issues on the Overview page.
* Manage devices by OS platform.
* Access, apply, and view filters at the top of every list view.  

This article describes how to opt in to the public preview and access these updated workloads:

* **Devices** > **Overview**
* **Devices** > **All devices**  
* **Devices** > **Configuration**
* **Devices** > **Compliance**
* **Devices** > **Windows 10 and later updates**  
* **Devices** > **Apple updates**  
* **Devices** > **Enrollment**  

## Opt in to public preview  

To try the new Devices experience in the admin center:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Overview**. 
3. Select the notification banner that says **Preview upcoming changes to Devices and provide feedback**.  
4. The **Devices preview** page opens. Select **Try it now** to opt in.  

You can switch back and forth between the current UI and public preview without impacting other admins in your tenant.  

:::image type="content" source="./media/microsoft-intune-admin-center-devices/public-preview-toggle-intune-2311.png" alt-text="Screenshot highlighting the public preview opt-in banner and Try it now button in the Microsoft Intune admin center." lightbox="./media/microsoft-intune-admin-center-devices/public-preview-toggle-intune-2311.png":::   

You remain in public preview even if you close the browser. To exit public preview and return to the current version of the admin center, flip the switch next to **Use Devices preview**.  Wait while Intune refreshes the UI.

:::image type="content" source="./media/microsoft-intune-admin-center-devices/device-preview-toggle-off.png" alt-text="Screenshot highlighting the Use Devices preview toggle in the Microsoft Intune admin center." :::

As you return to the current version of the admin center, an optional feedback form opens where you can give us feedback about your experience in public preview. Select **x** to return to the admin center without giving feedback.  

## Overview workload

Go to **Devices** > **Overview** to access workloads by OS platform, view key metrics about assigned policies, and access associated reports.  

:::image type="content" source="./media/microsoft-intune-admin-center-devices/overview-devices-experience.png" alt-text="Screenshot of a tenant's Overview page." :::

Overview options include: 

* **Manage devices by platform**: Select an OS platform to pivot between management workloads by platform.  
* **Additional monitoring reports**: Access reports associated with your key metrics.  
* **Other devices**: Access other device workloads, such as configuration for the Chrome OS enterprise connector.  

This page also highlights key metrics about active issues, such as enrollment failures and Windows 365 provisioning failures, happening across devices. Select a metric for more information about the issue. Select **Refresh** to refresh all data on the page.    

## All devices workload

Go to **Devices** > **All devices** to view a list of all Intune-managed devices in your tenant. 

:::image type="content" source="./media/microsoft-intune-admin-center-devices/all-devices-experience.png" alt-text="Screenshot of a tenant's All devices page, highlighting the workload title in the navigation menu." :::  

Select **Columns** to add and remove data in the table.    

:::image type="content" source="./media/microsoft-intune-admin-center-devices/column-selector-all-devices.png" alt-text="Screenshot highlighting the column picker on the All devices page." :::  

Select a device for more granular information, such as:  

* Hardware details  
* Installed apps  
* Assigned policies  
* Available remote actions  

For more information about device details, see [See device details in Intune](../remote-actions/device-inventory.md).  

## Device onboarding workload  

Under **Device onboarding**, you can access onboarding options for cloud PC creation and enrollment. This section describes the public preview experience for the updated Enrollement page.  

Go to **Enrollment** to access enrollment subworkloads for all device operating systems. 

:::image type="content" source="./media/microsoft-intune-admin-center-devices/enrollment-devices-experience.png" alt-text="Screenshot of a tenant's Enrollment page, highlighting the subworkloads." :::  

Enrollment subworkloads include:  

* **Monitor**: Access reports and list views associated with enrollment profiles, policies, and Windows Autopilot deployment.
* **Windows**: Set up enrollment for devices running Windows 10 or Windows 11.
* **Apple**: Set up enrollment for iOS/iPadOS and Mac devices.  
* **Android**: Set up enrollment for supported Android devices.
* **Corporate device identifiers**: Add and manage corporate identifiers for devices that should have corporate-owned status.  
* **Device enrollment manager**: Add and manage device enrollment managers that oversee or help with enrolling devices.  

For more information about getting started with enrollment, see [Enrollment guide: Microsoft Intune enrollment](deployment-guide-enrollment.md).

## Manage devices workload  

Under **Manage devices**, you can access these essential management workloads (workloads with UI changes are marked as *New*):

* **Configuration** - *New*  
* **Compliance** - *New*  
* **Conditional access**  
* **Scripts**  
* **Windows 10 and later updates** - *New*
* **Apple updates** - *New*
* **Group Policy analytics**
* **eSIM cellular profiles (preview)**  
* **Policy sets**  
* **Device clean-up rules**
* **Device categories**  
* **Partner portals**

Monitored data and relevant reports are located in the same place as your management tasks to help you find and act on issues quickly. This section describes the public preview experience for all updated workloads.  

### Configuration   

Go to **Devices** > **Configuration** to monitor and manage device configuration policies in Microsoft Intune. 

:::image type="content" source="./media/microsoft-intune-admin-center-devices/configuration-devices-experience.png" alt-text="Screenshot of a tenant's Configuration page, highlighting the subworkloads." ::: 

Configuration subworkloads include:

* **Monitor**: Access key metrics, reports, and list views associated with device configuration profiles.
* **Policies**: Create and manage device configuration policies.
* **Import ADMX**: Import custom and partner ADMX and ADML templates that you can create device configuration policies from.

For more information about device configuration, see [Apply features settings on your devices using device profiles in Microsoft Intune](../configuration/device-profiles.md).  

### Compliance   

Go to **Devices** > **Compliance** to monitor and manage device compliance policies in Microsoft Intune.  

:::image type="content" source="./media/microsoft-intune-admin-center-devices/compliance-devices-experience.png" alt-text="Screenshot of a tenant's Compliance page, highlighting the subworkloads." :::  

Within Compliance, you can access these subworkloads:  

* **Monitor**: Access key metrics, reports, and list views associated with device compliance.
* **Policies**: Create and manage device compliance policies.
* **Notifications**: Create and send custom notifications to device users on managed iOS/iPadOS and Android devices.  
* **Retire noncompliant devices**: Remove all company data from a device and remove the device from Intune management.
* **Scripts**: Add and manage scripts used for custom compliance settings.

For more information about device compliance, see [Compliance overview](../protect/device-compliance-get-started.md).  

### Windows 10 and later updates 

Go to **Devices** > **Windows 10 and later updates** to monitor and manage software update policies for devices running Windows 10 or Windows 11. 

:::image type="content" source="./media/microsoft-intune-admin-center-devices/windows-10-devices-experience.png" alt-text="Screenshot of a tenant's Windows 10 and later updates page, highlighting the subworkloads." :::  

Within this area, you can access the following subworkloads:  

* **Monitor**: Access key metrics and active issues associated with Windows software update policies.
* **Update rings**: Create and manage update ring policies for Windows 10 and Windows 11 updates.
* **Feature updates**: Create and manage policies for feature updates.
* **Quality updates**: Create and manage policies for quality updates.  
* **Driver updates**: Create and manage policies for driver updates.

For more information about Windows updates, see [Manage Windows 10 and Windows 11 software updates in Intune](../protect/windows-update-for-business-configure.md).  

### Apple updates

Go to **Devices** > **Apple updates** to monitor and manage software update policies for Apple devices.  

:::image type="content" source="./media/microsoft-intune-admin-center-devices/apple-updates-devices-experience.png" alt-text="Screenshot of a tenant's Apple updates page, highlighting the subworkloads." :::  

Within this area, you can access the following subworkloads:  

* **Monitor**: Access key metrics and active issues associated with Apple update policies.
* **iOS/iPadOS updates**: Create and manage policies for iOS/iPadOS updates.
* **macOS updates**: Create and manage policies for macOS updates.

For more information about software update policies for Apple devices, see:

* [Manage iOS/iPadOS software updates in Intune](../protect/software-updates-ios.md)
* [Manage macOS software updates in Intune](../protect/software-updates-macos.md)

## Next steps  

For an overview of new features and features that are ready to try in public preview, see [What's New in Microsoft Intune](../fundamentals/whats-new.md).
