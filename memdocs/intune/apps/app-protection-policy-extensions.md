---
# required metadata

title: App protection policies for extensions
titleSuffix: Microsoft Intune
description: This topic describes the app protection policy (APP) for extensions.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Protecting application extensions

This article describes app protection policies for extensions in Microsoft Intune.

## Add-ins for Outlook app

Outlook add-ins let you integrate popular apps with the email client. Add-ins for Outlook are available on the web, Windows, Mac, and Outlook for Android and iOS/iPadOS. The Intune APP SDK and Intune app protection policies do not include support for managing add-ins for Outlook, but there are other ways to limit their use. Since add-ins are managed via Microsoft Exchange, users will be able to share data and messages across Outlook and unmanaged add-in applications unless add-ins are turned off for the user by their Exchange.

If you want to stop your end users from accessing and installing Outlook add-ins (this affects all Outlook clients), make sure you have the following changes to roles in the Exchange admin center:

- To prevent users from installing Office Store add-ins, remove the My Marketplace role from them.
- To prevent users from side loading add-ins, remove the My Custom Apps role from them.
- To prevent users from installing all add-ins, remove both, My Custom Apps and My Marketplace roles from them.

These instructions apply to Microsoft 365, Exchange 2016, Exchange 2013 across Outlook on the web, Windows, Mac, and mobile.

- Learn more about [add-ins for Outlook](/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/add-ins-for-outlook).
- Learn more about [how to specify the administrators and users who can install and manage add-ins for Outlook app](/exchange/clients-and-mobile-in-exchange-online/add-ins-for-outlook/specify-who-can-install-and-manage-add-ins).

## LinkedIn account connections for Microsoft apps

LinkedIn account connections allow users to see public LinkedIn profile information within certain Microsoft apps. By default, your users can choose to connect their LinkedIn and Microsoft work or school accounts to see additional LinkedIn profile information. 

> [!NOTE]
> LinkedIn integration is currently unavailable for United States Government customers and for organizations with Exchange Online mailboxes hosted in Australia, Canada, China, France, Germany, India, South Korea, United Kingdom, Japan, and South Africa.

The Intune SDK and Intune app protection policies don't include support for managing LinkedIn account connections, but there are other ways to manage them. You can disable LinkedIn account connections for your entire organization, or you can enable LinkedIn account connections for selected user groups in your organization. These settings affect LinkedIn connections across Microsoft 365 apps on all platforms (web, mobile, and desktop). You can:

- Enable or disable LinkedIn account connections for your tenant in the portal. 
- Enable or disable LinkedIn account connections for your organization's Office 2016 apps using Group Policy.

If LinkedIn integration is enabled for your tenant, when users in your organization connect their LinkedIn and Microsoft work or school accounts, they have two options: 

- They can give permission to share data between both accounts. This means that they give permission for their LinkedIn account to share data with their Microsoft work or school account, as well as their Microsoft work or school account to share data with their LinkedIn account. Data that is shared with LinkedIn leaves the online services. 
- They can give permission to share data only from their LinkedIn account to their Microsoft work and school account

If a user consents to sharing data between accounts, as with Office add-ins, LinkedIn integration uses existing Microsoft Graph APIs. LinkedIn integration uses only a subset of the APIs available to Office add-ins and supports various exclusions.


|Microsoft Graph permissions  |Description  |
|---------|---------|
|Read permissions for [People](/graph/permissions-reference#people-permissions)     |Allows the app to read a scored list of people relevant to the signed-in user. The list can include local contacts, contacts from social networking or your organization's directory, and people from recent communications (such as email and Skype).         |
|Read permissions for [Calendars](/graph/permissions-reference#calendars-permissions)     |Allows the app to read events in user calendars. Includes the meetings in signed-in user calendars, their times, locations, and attendees.         |
|Read permissions for [User Profile](/graph/permissions-reference#user-permissions)     |Allows users to sign in to the app, and allows the app to read the profile of signed-in users. It also allows the app to read basic company information for signed-in users.         |
|Subscriptions     |This scope isn't available and not yet in use. It includes subscriptions provided by the user's organization to Microsoft apps and services, such as Microsoft 365.         |
|Insights     |This scope isn't available and not yet in use. It includes the interests associated with the signed-in user's account based on their use of Microsoft services.         |

### Learn more

- Learn about [LinkedIn information and features in your Microsoft apps](https://go.microsoft.com/fwlink/?linkid=850740).
- Learn about LinkedIn account connections release on the [Microsoft 365 Roadmap page](https://products.office.com/en-US/business/office-365-roadmap?filters=%26freeformsearch=linkedin#abc). 
- Learn about [Configuring LinkedIn account connections](/azure/active-directory/linkedin-integration).
- For more information about data that is shared between users' LinkedIn and Microsoft work or school accounts, see [LinkedIn in Microsoft applications at your work or school](https://www.linkedin.com/help/linkedin/answer/84077).

