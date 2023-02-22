---
# required metadata

title: Audit, export, or delete personal data collected by Intune
titleSuffix: Microsoft Intune
description: Learn how to audit, export, or delete personal data that's been collected by Intune.
keywords: GDPR, personal data, privacy
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/08/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 96990be0-eb1e-43a4-a0e4-09c7dbdc2bf4

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: kerimh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Audit, export, or delete personal data in Intune

Intune admins can use audit logs to track activities surrounding personal data. Admins can also export and delete personal data.

[!INCLUDE [GDPR-related guidance](../includes/gdpr-intro-sentence.md)]

## Audit personal data

Audit logs provide tenant admins with a record of activities that generate a change in Microsoft Intune. Audit logs are available for many manage activities and typically create, update (edit), delete, and assign actions. Remote tasks that generate audit events can also be reviewed. These audit logs may contain personal data from users whose devices are enrolled in Intune.  

For security purposes Intune may maintain audit logs for user and device actions for one year. These logs are automatically deleted after the one-year retention period.

To review audit logs, see [Audit logs for Intune activities](../fundamentals/monitor-audit-logs.md). 

Admins can't delete audit logs.

These audit events are retained for one year. Tenant admins can request audit logs using [this support request form](https://privacy.microsoft.com/en-US/privacy-questions?).

## Export personal data

Admins can export end user personal data, including accounts, service data, and associated logs to comply with Data Subject Rights requests. It's up to you and your organization to decide whether or not to provide the data subject with a copy of the personal data or if you have a legitimate business reason to withhold it. If you decide to provide it, you can provide them with a copy of the actual document, an appropriately redacted version, or a screenshot of the portions you have deemed appropriate to share.

To export a user's personal data, you can use:

- the *Export* option on the *All devices* node of the Microsoft Endpoint Manager admin center to export a list of devices. You can also copy device data directly.
- the [Export-IntuneData.ps1 script](https://aka.ms/intunedataexport).

## Delete end user personal data

There are three ways to remove personal data from Intune management:

- Delete the user from Azure Active Directory
- Reset the device to factory settings
- User self-removal

### Delete a user from Intune

To delete an end user's personal data from Intune, an admin must [delete the user from Azure Active Directory (Azure AD)](/azure/active-directory/fundamentals/add-users-azure-active-directory#delete-a-user). When the user is deleted from Azure AD (hard deleted), Intune receives the delete signal from Azure AD and then automatically begins purging all of that user's personal data from the Intune service. The user's information will be deleted from Intune service within 30 days of the removal action.

### Reset device to factory settings

Resetting to factory settings restores all company and personal data and settings to the original factory settings. It's useful before providing a device to the next employee. User files, user installed applications, and non-default settings are removed and this data is deleted from the Intune service within 30 days of the removal action.

### User self-removal from Intune management

Users can remove their [Android](../user-help/unenroll-your-device-from-intune-android.md), [Apple](../user-help/unenroll-your-device-from-intune-ios.md), or [Windows](../user-help/unenroll-your-device-from-intune-windows.md) personal device from Intune management without admin assistance.

### Retire

The **Retire** action removes Intune provisioned data like company applications, data about apps that Intune is managing, policy settings, and email profiles that are provisioned through Intune. This action leaves the user's personal data on the device.

### Delete a tenant from Microsoft Intune

If an Intune tenant customer cancels their Intune account, all tenant data is deleted within 180 days after the customer closes the Intune account. If the Azure AD tenant is associated with other Microsoft enterprise subscriptions (Azure, Microsoft 365), then only the Intune Customer Data is deleted. The Azure AD tenant resource is maintained for use by the other subscriptions. If the Intune account is the only subscription associated with the Azure AD tenant, then the tenant will be deleted and all resources and Customer Data will also be deleted.

## Next steps

Find out how to [view and correct personal data](privacy-data-view-correct.md) personal data in Intune.
