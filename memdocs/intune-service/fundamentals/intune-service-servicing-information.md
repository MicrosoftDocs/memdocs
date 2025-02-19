---
# required metadata

title: Microsoft Intune servicing information and details
description: Learn more about the frequency of the Microsoft Intune service updates, the release cadence, and how to check your tenant release version.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/12/2023
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
- get-started
- intro-get-started
ms.collection:
- tier2
- M365-identity-device-management
---

# Service information for Microsoft Intune release updates

New feature releases for Intune typically have a six to eight week cadence, from planning to release. This cadence is called a sprint. Intune releases use a `YYMM` naming convention. For example, 2301 is the January 2023 release.

This article provides information about the frequency of the Microsoft Intune service updates, the release cadence, and how to check your tenant release version.

## How updates are released

The monthly release process involves many different environments and is deployed to multiple Azure services. After it's deployed to Azure, the release updates are deployed to the Intune admin center, which makes the release features available for you to use.

An internal environment called Self Host is the first environment to receive the release. Self Host is used only by the Intune engineering teams. After Self Host, the service release is deployed to the Microsoft tenant that manages many devices. Once it's validated that there are no key issues with the service release, the release begins deploying to customer environments in a phased approach. Once all tenants are successfully updated, the Microsoft Intune admin center is updated. This phased approach helps identify issues before they affect the service or our customers.

Updating the Company Portal app is a different process. Microsoft is subject to the release requirements and processes of the Apple App Store, Google Play, and sometimes mobile carriers. It isn't always possible to align the Intune release updates with updates to the Company Portal app. For more information on the Company Portal app updates, go to [UI updates for Intune end-user apps](whats-new-app-ui.md).

### How can I tell if a service update is complete for my tenant?

To check the release version of your tenant, use the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Tenant status**. Your tenant's name, location, MDM authority, account status, and service release number are shown.

In the following example, the tenant has the 2311 (November 2023) service release:

:::image type="content" source="./media/intune-service-servicing-information/intune-admin-center-tenant-status.png" alt-text="In the Intune admin center, select tenant administration and then tenant status to see the service release version." lightbox="./media/intune-service-servicing-information/intune-admin-center-tenant-status.png":::

## Keep current with release features

Keeping up to date about releases and changes is an important part of your Intune deployment. Intune provides several ways to stay current about latest updates:

- **[What's new in Intune](whats-new.md)**: Learn what's new in a Microsoft Intune release. When a feature is released, some information about that feature is added to this article. It also includes an overview of the current release, any notices, information about earlier releases, and other information.

  Content is published at the end of the current sprint, which is when the UI updates start deploying to the Microsoft Intune admin center.

- **[In development for Microsoft Intune](in-development.md)**: Learn more about what features are in development for Microsoft Intune. This article is updated regularly with upcoming features and changes.
- **[Microsoft 365 Message center](/microsoft-365/admin/manage/message-center)**: When the service update finishes deploying, a message is posted in the **Message center**. Or, you can view the same messages in the Message center at `portal.office.com`. Service APIs pull only the Microsoft Intune messages from Microsoft 365 into the Microsoft Intune admin center.
- **[Microsoft Intune tenant status](tenant-status.md)**: This message center is a centralized hub where you can view current information and communications about the Intune service and your tenant status.

  To see the hub, use the following steps:

  1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
  2. Go to **Tenant administration** > **Tenant status** > **Service health and message center**.
  3. Under **Message center**, select any message to read it.

- **Social media**: Get the latest announcements on X at `@IntuneSuppTeam`.

For more information from the Intune support team, go to the following blog posts:

- [Staying up to date on Intune new features, service changes, and service health](https://aka.ms/MEMServiceChangeBlog)
- [Tips and tricks for managing Intune](https://aka.ms/mem-tipsandtricks-blog)

## Privacy and personal data in Intune

You should understand how Intune collects, stores, retains, processes, secures, shares, audits, and exports personal data. Microsoft Intune doesn't use any personal data collected as part of providing the service for profiling, advertising, or marketing purposes.

The following resources can help you understand privacy and personal data in Intune:

- [Privacy and personal data in Intune](../protect/privacy-personal-data.md)
- [Optional diagnostic data from Intune Client apps](../protect/client-apps-optional-data.md)
- [Data collection in Intune](../protect/privacy-data-collect.md)
- [Data storage and processing in Intune](../protect/privacy-data-store-process.md)
- [Audit, export, or delete personal data in Intune](../protect/privacy-data-audit-export-delete.md)

## Related content

- [Get started with Microsoft Intune](get-started-with-intune.md)
- [Planning guide to move to Microsoft Intune](intune-planning-guide.md)
