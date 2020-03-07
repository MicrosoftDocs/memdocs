---
# required metadata

title: Microsoft Intune email settings for Windows Phone 8.1
titleSuffix:
description: Learn about the Intune settings you can use to configure email connections on devices running Windows Phone 8.1.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 3/6/2018
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Email profile settings in Microsoft Intune for devices running Windows Phone 8.1



This article shows you the email profile settings you can configure for your devices running Windows Phone 8.1.

>[!IMPORTANT]
>Windows Phone 8.1 email profiles are also applied to Windows 10 devices.

- **Email server** - The host name of your Exchange server.
- **Account name** - The display name for the email account as it appears to users on their devices.
- **Username attribute from AAD** - This is the attribute in Active Directory (AD) or Azure AD, that is used to generate the username for this email profile. Select **Primary SMTP Address**, such as **user1@contoso.com** or **User Principal Name**, such as **user1** or **user1@contoso.com**.
- **Email address attribute from AAD** - How the email address for the user on each device is generated. Select **Primary SMTP Address** to use the primary SMTP address to log into Exchange or use **User Principal Name** to use the full principal name as the email address.


## Security settings

- **SSL** - Use Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server.



## Synchronization settings

- **Amount of email to synchronize** - Choose the number of days of email that you want to synchronize, or select **Unlimited** to synchronize all available email.
- **Sync schedule** - Select the schedule by which devices synchronize data from the Exchange server. You can also select **As Messages arrive**, which synchronizes data as soon as it arrives, or **Manual**, where the user of the device must initiate the synchronization.

## Content sync settings

- **Content type to sync** - Select the content types that you want to synchronize to devices from:
  - **Contacts**
  - **Calendar**
  - **Tasks**
