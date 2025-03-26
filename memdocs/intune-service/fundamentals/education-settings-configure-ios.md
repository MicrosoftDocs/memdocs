---
# required metadata

title: Intune settings for the iOS/iPadOS Classroom app 
titleSuffix: Microsoft Intune
description: Learn the Intune settings you can use to control settings for the Classroom app on iOS/iPadOS devices.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/14/2019
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.assetid: 1381a5ce-c743-40e9-8a10-4c218085bb5f

# optional metadata

#ROBOTS: NOINDEX
#audience:

ms.reviewer: derriw
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# How to configure Intune settings for the iOS/iPadOS Classroom app

> [!NOTE]
> Intune doesn't currently support configuring the Classroom app. This article is only applicable for users with existing iOS/iPadOS education profiles in Intune.  

## Introduction
[Classroom](https://itunes.apple.com/app/id1085319084) is an app that helps teachers to guide learning, and control student devices in the classroom. For example, the app enables teachers to:

- Open apps on student devices
- Lock, and unlock the iPad screen
- View the screen of a student iPad
- Navigate students iPads to a bookmark, or chapter in a book
- Display the screen from a student iPad on an Apple TV

To set up Classroom on your device, you will need to create and configure an Intune iOS/iPadOS education device profile.

## Before you start

Consider the following before you begin to configure these settings:

- Both teachers and student iPads must be enrolled in Intune.
- Ensure that you have installed the [Apple Classroom](https://itunes.apple.com/us/app/classroom/id1085319084?mt=8) app on the teacher's device. You can either install the app manually, or use [Intune app management](../apps/app-management.md).
- You must configure certificates to authenticate connections between teacher and student devices (see Step 2, Create and assign an iOS/iPadOS Education profile in Intune).
- Teacher and student iPads must be on the same Wi-Fi network, and also have Bluetooth enabled.
- The Classroom app runs on supervised iPads running iOS/iPadOS 9.3 or later.
- In this release, Intune supports managing a 1:1 scenario where each student has their own dedicated iPad.


<a name='step-1---import-your-school-data-into-azure-active-directory'></a>

## Step 1 - Import your school data into Microsoft Entra ID

Use Microsoft's School Data Sync (SDS) to import school records from an existing Student Information System (SIS) to Microsoft Entra ID.
SDS synchronizes information from your SIS and stores it in Microsoft Entra ID. Microsoft Entra ID is a Microsoft management system that helps you organize users and devices. You can then use this data to help you manage your students and classes. [Learn more about how to deploy SDS](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91).

### How to import data using SDS

You can import information into SDS by using one of the following methods:

- [CSV files](https://support.office.com/article/Follow-these-steps-71d5fe4a-aa51-4f35-9b53-348898a390a1) - Manually export and compile comma-separated value (.csv) files
- [PowerSchool API](https://support.office.com/article/Follow-these-steps-851b5edc-558f-43a9-9122-b2d63458cb8f) - An SIS provider that simplifies syncing with Microsoft Entra ID
- [OneRoster](https://support.office.com/article/Follow-these-steps-f43cbb2a-b502-497d-a8b1-783dc05a57ab) - A CSV format that you can export and convert to sync with Microsoft Entra ID

### Find out more

- [Find out more about the full experience of syncing on-premises school data to Microsoft Entra ID](/azure/active-directory/connect/active-directory-aadconnect)
- [Find out more about Microsoft School Data Sync](https://sds.microsoft.com/)
- [Find out more about licensing in Microsoft Entra ID](/azure/active-directory/active-directory-licensing-whatis-azure-portal)

## Step 2 - Create and assign an iOS/iPadOS Education profile in Intune

### Configure general settings

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Manage devices** > **Configuration** > **Create** > **New policy**.
3. Enter the following properties:

    - **Platform:** Select **iOS/iPadOS**.
    - **Profile type**: Select **Templates** > **Secure assessment (Education)**.

    Select **Create**.

4. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. For example, enter **iOS/iPadOS education profile**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

5. In **Configuration settings**, you'll create certificates to establish a trust relationship between teacher and student iPads. Certificates are used to seamlessly and silently authenticate connections between devices without having to enter user names and passwords.

>[!IMPORTANT]
>The teacher and student certificates you use must be issued by different certification authorities (CAs). You must create two new subordinate CAs connected to your existing certificate infrastructure; one for teachers, and one for students.

iOS education profiles support only PFX certificates. SCEP certificates are not supported.

Created certificates must support server authentication and user authentication.

### Configure teacher certificates

On the **Education** pane, choose **Teacher certificates**.

#### Configure teacher root certificate

Under **Teacher root certificate**, choose the browse button. Select the root certificate with either:
- Extension .cer (DER, or Base64 encoded) 
- Extension .P7B (with or without full chain)

#### Configure teacher PKCS#12 certificate

Under **Teacher PKCS#12 certificate**, configure the following values:

- **Subject name format** - Intune automatically prefixes common names for teacher certificates with **leader**. Common names for Student certificates are prefixed with **member**.
- **Certification authority** - An Enterprise Certification Authority (CA) that runs on an Enterprise edition of Windows Server 2008 R2 or later. A Standalone CA is not supported. 
- **Certification authority name** - Enter the name of your certification authority.
- **Certificate template name** - Enter the name of a certificate template that has been added to an issuing CA. 
- **Renewal threshold (%)** - Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.
- **Certificate validity period** - Specify the amount of remaining time before the certificate expires.
You can specify a value that is lower than the validity period in the specified certificate template, but not higher. For example, if the certificate validity period in the certificate template is two years, you can specify a value of one year but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA certificate.

When you're finished configuring certificates, choose **OK**.

### Configure student certificates

1. On the **Education** pane, choose **Student certificates**.
2. On the **Student certificates** pane, from the **Student device certificates** type list, choose **1:1**.

#### Configure student root certificate

Under **Student root certificate**, choose the browse button. Select the root certificate with either:
- Extension .cer (DER, or Base64 encoded) 
- Extension .P7B (with or without full chain)

#### Configure student PKCS#12 certificate

Under **Student PKCS#12 certificate**, configure the following values:

- **Subject name format** - Intune automatically prefixes common names for teacher certificates with **leader**. Common names for Student certificates are prefixed with **member**.
- **Certification authority** - An Enterprise Certification Authority (CA) that runs on an Enterprise edition of Windows Server 2008 R2 or later. A Standalone CA is not supported. 
- **Certification authority name** - Enter the name of your certification authority.
- **Certificate template name** - Enter the name of a certificate template that has been added to an issuing CA. 
- **Renewal threshold (%)** - Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.
- **Certificate validity period** - Specify the amount of remaining time before the certificate expires.
You can specify a value that is lower than the validity period in the specified certificate template, but not higher. For example, if the certificate validity period in the certificate template is two years, you can specify a value of one year but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA certificate.

When you're finished configuring certificates, choose **OK**.

## Finish up

1. On the **Education** pane, choose OK.
2. On the **Create profile** pane, choose **Create**.

The profile is created and appears on the profiles list pane.

Assign the profile to student devices in the classroom groups that were created when you synchronized your school data with Microsoft Entra ID (see [How to assign device profiles](../configuration/device-profile-assign.md)).

## Next steps

Now when teachers use the Classroom app, they'll have full control over student devices.

For more information about the Classroom app, see [Classroom help](https://help.apple.com/classroom/ipad/2.0/), on the Apple web site.

If you want to configure shared iPad devices for students, see [How to configure Intune education settings for shared iPad devices](education-settings-configure-ios-shared.md).
