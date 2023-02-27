---
# required metadata

title: Where did my Intune feature go in Azure?
titleSuffix: Microsoft Intune
description: Helps you find Microsoft Intune features in the Azure portal.
keywords:
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 1/4/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 809d9d76-20f8-4329-9e18-cd7d4946a9af

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---
# Where did my Intune feature go in Azure?
We took the opportunity to organize some tasks more logically as we moved Intune into the Azure portal. But every improvement comes with the cost of learning the new organization. This reference guide is for those of you who are thoroughly familiar with Intune in the classic portal and are wondering how to get something done in Intune in the Azure portal. If this article doesn't cover a feature you're trying to find, leave a comment at the end of the article so we can update it.
## Quick reference guide

|Feature |Path in classic portal|Path in Intune in the Azure portal|
|------------|---------------|---------------|
|Device Enrollment Program (DEP) [iOS only]|Admin > Mobile Device Management > iOS > Device Enrollment Program|[Device enrollment > Apple Enrollment > Enrollment Program Token](#where-did-apple-dep-go) |
|Device Enrollment Program (DEP) [iOS only]| Admin > Mobile Device Management > iOS and Mac OS X > Device Enrollment Program |[Device enrollment > Apple Enrollment > Enrollment Program Serial Numbers](#where-did-apple-dep-go) |
|Enrollment Rules |Admin > Mobile Device Management > Enrollment Rules|[Device enrollment > Enrollment Restrictions](#where-did-enrollment-rules-go) |
|Groups by iOS Serial Number |Groups > All Devices > Corporate Pre-enrolled devices > By iOS Serial Number|[Device enrollment > Apple Enrollment > Enrollment Program Serial Numbers](#where-did-corporate-pre-enrolled-devices-go) |
|Groups by iOS Serial Number |Groups > All Devices > Corporate Pre-enrolled devices > By iOS Serial Number| [Device enrollment > Apple Enrollment > AC Serial numbers](#where-did-corporate-pre-enrolled-devices-go)|
|Groups by IMEI (all platforms)| Groups > All Devices > Corporate Pre-enrolled devices > By IMEI (All platforms) | [Device enrollment > Corporate Device Identifiers](#by-imei-all-platforms)|
| Corporate Device Enrollment profile| Policy > Corporate Device Enrollment | [Device enrollment > Apple Enrollment > Enrollment Program Profiles](#where-did-corporate-pre-enrolled-devices-go) |
| Corporate Device Enrollment profile | Policy > Corporate Device Enrollment | [Device enrollment > Apple Enrollment > AC Profiles](#where-did-corporate-pre-enrolled-devices-go) |
| Android for Work | Admin > Mobile Device Management > Android for Work | Device enrollment > Android enrollment |
| Terms and Conditions | Policy > Terms and Conditions | Device enrollment > Terms and Conditions |
Company Portal settings|Admin > Company Portal|**Manage** > Mobile apps<br> **Setup** > Company Portal branding

## Where do I manage groups?
Intune in the Azure portal uses [Azure Active Directory (AD)](/azure/active-directory/active-directory-groups-create-azure-portal) to manage groups.

## Where did enrollment rules go?
In the classic portal, you could set rules governing the MDM enrollment of mobile and modern Windows and macOS devices.

![Image of classic mobile device enrollment rules](./media/ui-changes/01-classic-rules.png)

These rules applied to all users in your Intune account without exception. In the Azure portal, these rules now appear in two distinct policy types: Device Type Restrictions and Device Limit Restrictions.

![Image of Azure mobile device enrollment restrictions](./media/ui-changes/02-azure-enroll-restrictions.png)

The default Device Limit Restriction corresponds to the Device Enrollment Limit in the classic portal.

![Image of Azure device limit restrictions](./media/ui-changes/03-azure-device-limit.png)

The default Device Type Restriction corresponds to the Platform Restrictions in the classic portal.

![Image of Azure device type restrictions](./media/ui-changes/04-azure-platform-restrictions.png)

The ability to allow or block personally owned devices is now managed under the Device Type Restriction's Platform Configurations.

![Image of Azure personal device block settings](./media/ui-changes/05-azure-personal-block.png)

New restriction capabilities are added to the Azure portal only.

## Where did my Conditional Access policies go?
After your tenant migrates to the Azure portal, your tenant's Conditional Access policies continue to be enforced. However, you are not able to view or modify them from Intune in the Azure portal.

If you would like to view and make changes to Conditional Access policies from the Azure portal, you will need to remove the old policies from the classic portal. Then recreate them in the Azure portal. For more information about migrating Conditional Access policies, see [Migrate classic policies in the Azure Portal](/azure/active-directory/active-directory-conditional-access-migration).

## Where did my compliance policies go?
After your tenant migrates to the Azure portal, your tenant's compliance policies continue to be enforced. However, you are not able to view or modify them from Intune in the Azure portal.

If you would like to view and make changes to compliance policies from the Azure portal, you will need to remove the old policies from the classic portal. Then recreate them in the Azure portal. For more information about device compliance policies, see [Get started with device compliance policies in Intune](../protect/device-compliance-get-started.md). 

## Where did Apple DEP go?
In the classic portal, you could set up Intune to integrate with Apple's Device Enrollment Program and manually request synchronization with Apple's service:

![Image of classic DEP token](./media/ui-changes/06-classic-dep-token.png)

In the Azure portal, you set up Apple Device Enrollment Program with the same steps as in Intune classic:

![Image of Azure DEP token](./media/ui-changes/07-azure-dep-token.png)

However the **Sync** option in the classic portal has been moved to the serial number management workflow since the results of a manual sync appear there:

![Image of Azure DEP sync](./media/ui-changes/08-azure-dep-sync.png)

## Where did corporate pre-enrolled devices go?
### By iOS serial number
In the classic portal, you can enroll iOS devices through the Apple Device Enrollment Program (DEP) and the Apple Configurator tool. Both methods offer device pre-enrollment by serial number and involve the assignment of special Corporate Device Enrollment profiles. Prior to enrollment, the enrollment profile assignment can be managed through the **Corporate Pre-enrolled Device by iOS Serial Number** device group:

![Image of classic Apple serial numbers](./media/ui-changes/09-classic-apple-serials.png)

This lists serial numbers for both Apple DEP and Configurator enrollment in a single list. To reduce profile assignment mis-match (DEP profile to AC serial number and vice-versa), we have separated the serial numbers into two lists in the Azure portal:

**DEP serial numbers**
![Image of Azure DEP serial numbers](./media/ui-changes/10-azure-dep-serials.png)

**Apple Configurator serial numbers**
![Image of Azure Apple Configurator serial numbers](./media/ui-changes/11-azure-ac-serials.png)

### By IMEI (all platforms)

In the classic portal, you can pre-list the IMEI numbers of devices to mark them as corporate when they enrolled to Intune:

![Image of classic list of IMEI numbers](./media/ui-changes/12-classic-corp-imei.png)

In the Azure portal, you must upload the same IMEI to the Corporate Device Identifiers list with a comma-separated-values (CSV) file. The new portal does not support manual entry of IMEI numbers:

![Image of Azure list of IMEI number](./media/ui-changes/13-azure-corp-imei.png)

Intune in the Azure portal is future-proofed to support other types of identifiers beside IMEI, but currently only allows IMEI numbers for pre-listing.

## Where did Corporate Device Enrollment profiles go?
To enroll iOS devices through the Apple Device Enrollment Program or with the Apple Configurator tool, you must supply a Corporate Device Enrollment profile to be assigned the device. In the classic portal, the creation and management of these profiles was located in a single list:

![Image of classic device enrollment profiles](./media/ui-changes/14-classic-corp-profiles.png)

This list shows profiles enabled for use with the Apple Device Enrollment Program (**DEP On**) and profile only enabled for use with the Apple Configurator tool (**DEP Off**).

To reduce confusion between the two profile types and potential mis-matched assignments (DEP profile to Configurator devices and vice-versa), we have separated creation and management of Enrollment Program profiles (support both Apples Device Enrollment Program and Apple School Manager) and Apple Configurator profiles:

**DEP profiles**
![Image of Azure DEP profiles](./media/ui-changes/15-azure-dep-profiles.png)

**Apple Configurator profiles**
![Image of Azure Apple Configurator profiles](./media/ui-changes/16-azure-ac-profiles.png)
