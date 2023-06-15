---
# required metadata

title: Intune shared device settings for the iOS/iPadOS Classroom app
titleSuffix: Microsoft Intune
description: Learn the Intune settings you can use to control settings for the Classroom app on shared iOS/iPadOS devices.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/06/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology:
ms.assetid: 1381a5ce-c743-40e9-8a10-4c218085bb5f

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---


# Configure Intune education settings for shared iPad devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

> [!NOTE]
> Intune doesn't currently support configuring the Classroom app. This article is only applicable for users with existing iOS/iPadOS education profiles in Intune.

Intune supports the iOS/iPadOS Classroom app that helps teachers to guide learning, and control student devices in the classroom. In addition, to the Classroom app, Apple supports the ability for student iPad devices to be configured such that multiple students can share a single device. This document guides you to achieve this goal with Intune.

For information about configuring dedicated (1:1) iPad devices to use the Classroom app, see [How to configure Intune settings for the iOS/iPadOS Classroom app](education-settings-configure-ios.md).

## Before you start

The prerequisites to use the shared iPad capabilities are:

- Setup [Apple School Manager](../enrollment/apple-school-manager-set-up-ios.md) and [School Data Sync (SDS)](https://support.office.com/article/Apple-School-Manager-integration-with-Intune-for-Education-and-School-Data-Sync-974bd1f9-2c7a-45cb-9447-b58166108617).
- As part of Apple School Manager setup, configure [Managed Apple IDs](https://school.apple.com/) for students. [Learn more about Managed Apple IDs](https://support.apple.com/HT205918).
- Create an enrollment profile for the device serial numbers synced from Apple School Manager.

## Step 1 - Import your school data into Azure Active Directory

Use Microsoft's School Data Sync (SDS) to import school records from an existing Student Information System (SIS) to Azure Active Directory (Azure AD).
SDS synchronizes information from your SIS and stores it in Azure AD. Azure AD is a Microsoft management system that helps you organize users and devices. You can then use this data to help you manage your students and classes. [Learn more about how to deploy SDS](https://support.office.com/article/Overview-of-School-Data-Sync-and-Classroom-f3d1147b-4ade-4905-8518-508e729f2e91).

### How to import data using SDS

You can import information into SDS by using one of the following methods:

- [CSV files](https://support.office.com/article/Follow-these-steps-71d5fe4a-aa51-4f35-9b53-348898a390a1) - Manually export and compile comma-separated value (.csv) files
- [PowerSchool API](https://support.office.com/article/Follow-these-steps-851b5edc-558f-43a9-9122-b2d63458cb8f) - An SIS provider that simplifies syncing with Azure AD
- [OneRoster](https://support.office.com/article/Follow-these-steps-f43cbb2a-b502-497d-a8b1-783dc05a57ab) - A CSV format that you can export and convert to sync with Azure AD

### Find out more

- [Find out more about the full experience of syncing on-premises school data to Azure AD](/azure/active-directory/connect/active-directory-aadconnect)
- [Find out more about Microsoft School Data Sync](https://sds.microsoft.com/)
- [Find out more about licensing in Azure Active Directory](/azure/active-directory/active-directory-licensing-whatis-azure-portal)


## Step 2 - Create and assign an iOS/iPadOS Education profile in Intune

### Configure general settings

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Device configuration**.
2. On the **Device configuration** pane under the **Manage** section, choose **Profiles**.
5. On the profiles pane, choose **Create profile**.
6. On the **Create profile** pane, enter a **Name** and **Description** for the iOS/iPadOS education profile.
7. From the **Platform** drop-down list, choose **iOS**.
8. From the **Profile type** drop-down list, choose **Education**.
9. Choose **Settings** > **Configure**.

Next, you need certificates to establish a trust relationship between teacher and student iPads. Certificates are used to seamlessly and silently authenticate connections between devices without having to enter user names and passwords.

>[!Important]
>The teacher and student certificates you use must be issued by different certificate authorities (CAs). You must create two new subordinate CAs connected to your existing certificate infrastructure; one for teachers, and one for students.

iOS education profiles support only PFX certificates. SCEP certificates are not supported.

Certificates you create must support server authentication in addition to user authentication.

### Configure teacher certificates

On the **Education** pane, choose **Teacher certificates**.

#### Configure teacher root certificate

Under **Teacher root certificate**, choose the browse button to select the teacher root certificate with the extension .cer (DER, or Base64 encoded), or .P7B (with or without full chain).

#### Configure teacher PKCS#12 certificate

Under **Teacher PKCS#12 certificate**, configure the following values:

- **Subject name format** - Intune automatically prefixes the certificate common name with **leader**, for the teacher certificate, and **member**, for the student certificate.
- **Certification authority** - An Enterprise Certification Authority (CA) that runs on an Enterprise edition of Windows Server 2008 R2 or later. A Standalone CA is not supported.
- **Certification authority name** - Enter the name of your certification authority.
- **Certificate template name**- Enter the name of a certificate template that has been added to an issuing CA.
- **Renewal threshold (%)** - Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.
- **Certificate validity period** - Specify the amount of remaining time before the certificate expires. You can specify a value that is lower than the validity period in the specified certificate template, but not higher. For example, if the certificate validity period in the certificate template is two years, you can specify a value of one year but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA certificate.

When you have finished configuring teacher certificates, choose **OK**.

### Configure student certificates

1. On the **Education pane**, choose **Student certificates**.
2. On the **Student certificates** pane, from the **Student device certificates type** list, choose **Shared iPad**.

#### Configure student root certificate

Under **Device root certificate**, choose the browse button to select the student root certificate with the extension .cer (DER, or Base64 encoded), or .P7B (with or without full chain).

#### Configure device PKCS#12 certificate

Under **Student PKCS#12 certificate**, configure the following values:

- **Subject name format** - Intune automatically prefixes the certificate common name with leader, for the teacher certificate, and member, for the device certificate.
- **Certification authority** - An Enterprise Certification Authority (CA) that runs on an Enterprise edition of Windows Server 2008 R2 or later. A Standalone CA is not supported.
- **Certification authority name** - Enter the name of your certification authority.
- **Certificate template name** - Enter the name of a certificate template that has been added to an issuing CA.
- **Renewal threshold (%)** - Specify the percentage of the certificate lifetime that remains before the device requests renewal of the certificate.
- **Certificate validity period** - Specify the amount of remaining time before the certificate expires. You can specify a value that is lower than the validity period in the specified certificate template, but not higher. For example, if the certificate validity period in the certificate template is two years, you can specify a value of one year but not a value of five years. The value must also be lower than the remaining validity period of the issuing CA certificate.

When you are finished configuring certificates, choose **OK**.

### Complete Certificate Setup

1. On the **Education** pane, choose **OK**.
2. On the **Create profile** pane, choose **Create**.

The profile is created and appears on the profiles list pane.

## Step 3 - Create a device category

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Device enrollment**.
4. On the **Device enrollment - Overview** pane, choose **Device categories**.
5. On the **Device enrollment - Device Categories** pane, choose **Create**.
6. On the **Create device category** pane, enter a **Name** and **Description** for the category.
7. On the **Create device category** pane, choose **Create**.

The device category is created in the **Enrollment – Device Categories** pane.

## Step 4 – Create a dynamic group

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Groups**.
4. On the **Users and Groups – All Groups** pane, choose **New group**.
5. On the **Group** pane, choose a **Group type** and then enter a **Name** and **Description** for the group.
6. From the **Membership type** drop-down list, choose **Dynamic Device**.
7. Choose **Dynamic device members** to create membership rules.
8. On the **Dynamic membership rules** pane:
1. Select **deviceCategory** from the **Add devices where** drop-down list.
2. Choose **Equals**.
3. Enter the device category you created in the blank text box.
9. On the **Dynamic membership rules** pane, choose **Add query**.
10. On the **Group** pane, choose **Create**.

The dynamic group is created in the **Users and Groups – All Groups** pane.

## Step 5 – Assign a device to a category (Carts)

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Devices**.
4. On the **Devices** pane, choose **All devices**.
5. On the **Devices – All devices** pane, choose a device.
6. On the device pane, choose **Properties**.
7. On the device's properties pane, enter the device category in the **Device category** text box.
8. On the device pane, choose **Save**.

The device is now associated to the device category. Repeat this process for all the devices you want to associate to the device category you created.

## Step 6 – Create classroom profiles

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Device configuration**.
4. On the **Device configuration** pane, choose **Manage** > **Cart Profiles**.
5. On the profiles pane, choose **Create Profile**.
6. On the **Create Association** pane, enter a **Name** and **Description**.
7. Choose **Select Classes** > **Configure** to associate groups to the Cart Profile.
8. Choose the classes to include to the Cart Profile then choose **Select**. 
9. Choose **Select Carts** > **Configure** to associate groups to the Cart Profile.
10. Choose the groups to include to the Cart Profile then choose **Select**.
11. On the **Create Association** pane, choose **Save** to save the Cart Profile.

The profile is created and appears on the profiles list pane.

## Step 7 - Assign the Cart Profile to Classes

1. Sign in to [Intune](https://go.microsoft.com/fwlink/?linkid=2090973).
3. On the **Intune** pane, choose **Device configuration**.
4. On the **Device configuration** pane, choose **Monitor** > **Assignment status**.
5. On the **Assignment status** pane, select the **Cart Profile** you created.
6. On the **Cart Profile** pane choose **Assignments** and then, under **Include** choose **Select groups to include**.
7. Select the classes you want the cart profile to target (do not select a group), then choose **Select**. 
8. When you are finished, choose **Save**.

The assignment completes, and Intune deploys the Classroom profile to the targeted devices based on the classroom assignment.

## Next Steps

Now students can share devices between students, and students can pick up any iPad in a classroom, log in with a PIN and have it personalized with their content. For more information about Shared iPads, see the [Apple website](https://www.apple.com/education/).
