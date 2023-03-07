---
# required metadata

title : Set up Intune
titleSuffix: Microsoft Intune
description: Step 1 for deploying or setting up Intune. The starting point is to review supported configurations, sign-up for the trial, configure the custom domain name, add users and groups to Intune, assign licenses to users, manage roles, grant admin permissions , and set the MDM authority.  
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 01/31/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
- M365-identity-device-management 
- highpri
- tier1
---

# Step 1: Set up Microsoft Intune

In this article, you'll step through the process of setting up Microsoft Intune. Also, this article will provide the choices and considerations you need to make when setting up an endpoint-management solution such as Intune.
By the end of this article, you'll have a better understanding of Intune's supported configurations. You'll have signed up for the Microsoft Intune's free trial. You'll add end users, define user groups, assign licenses to users, and set up the other needed settings to begin using Microsoft Intune. All of these steps will prepare you to add and manage devices and apps using Intune.

This article applies to:

- Android
- iOS/iPadOS
- macOS
- Windows

## Prerequisites

Before you begin setting up Microsoft Intune, review the [Planning guide](intune-planning-guide.md). Use this guide to plan your move or migration to Intune.  
The planning guide also includes the following:

- Lists and describes some common objectives for device management
- Lists potential licensing needs
- Provides guidance on handling personally owned devices
- Recommends reviewing current policies and infrastructure
- Gives examples of creating a rollout plan
- And more

## 1 - Review the Supported Configurations

Before you begin setting up Microsoft Intune, you should review the device platforms and operating systems that Intune supports. Additionally, review which web browsers are supported when accessing Intune using Microsoft Intune admin center. Also, you should be familiar with the network bandwidth requirements to perform installations and updates using Intune.

✔️ **Get started with supported configurations**

 Need-to-know information before you start. For guidance, go to [Supported configurations](supported-devices-browsers.md).

## 2 - Sign up for Microsoft Intune

Before you sign up for Intune, determine whether you already have a Microsoft Online Services account, Enterprise Agreement, or equivalent volume licensing agreement. A Microsoft volume licensing agreement or other Microsoft cloud services subscription like Microsoft 365 usually includes a work or school account.

If you already have a work or school account, **sign in** with that account and add Intune to your subscription. Otherwise, you can **sign up** for a new account to use Intune for your organization.
Sign in to the Microsoft Intune admin center, and sign up for Intune. If you have an existing subscription, you can also sign in to it.

✔️ **Get started with sign up, or sign in to Intune**

 Sign in to your subscription or create a new Intune subscription. For guidance, go to [Sign in to Intune](account-sign-up.md).

## 3 - Configure a custom domain name for your Intune tenant

When your organization signs up for Microsoft Intune, you're given an initial domain name hosted in Azure Active Directory (Azure AD) that looks like *your-domain.onmicrosoft.com*.
In this example, *your-domain* is the domain name that you chose when you signed up. *onmicrosoft.com* is the suffix assigned to all accounts added to subscriptions.

You can **optionally** configure your organization's custom domain to access Intune, instead of the domain name provided with your subscription. If you are simply evaluating Intune using the free trial, you can skip this step.

✔️ **Get started with configuring a custom domain name for your Intune tenant**

 Set DNS registration to connect your company's domain name with Intune. This gives users a familiar domain when connecting to Intune and using resources. For guidance, go to [Configure domain name](custom-domain-name-configure.md)

## 4 - Add users to Intune

The people in your organization each need a user account before they can sign in and access Microsoft Intune. To create user accounts, you can add users to Intune. Once added, you can grant permissions and assign licenses to users. Then later, you can assign different types of policies to users to help and protect them.

As an administrator, you can add users individually or in bulk to Intune. The easiest way to add user accounts is to add them one at a time in the Microsoft Intune admin center.

You must be an admin (global, license, or a user admin) to add users to Intune. If you set up Intune using the free trial, you are a global admin.

✔️ **Get started with adding users to Intune**

 Add users, or connect Active Directory to sync with Intune. This step is **required** unless your devices are "userless" kiosk devices. For guidance, go to [Add users](users-add.md).

## 5 - Create groups in Intune

Intune uses Azure Active Directory (Azure AD) groups to organize and manage devices and users. As an Intune admin, you can set up groups to suit your organizational needs. For instance, you can create groups to organize users or devices by geographic location, department, or hardware characteristics. Also, you can use groups to manage tasks at scale. For example, you can set policies for many users or deploy apps to a set of devices based on groups.

✔️ **Get started with adding groups to Intune**

 Add groups, to assign apps, settings, and other resources. For some guidance, go to [Add groups](groups-add.md).

## 6 - Manage licenses

Intune is available with different subscriptions, including as a stand-alone service. Determine the licensed services your organization needs and then continue to assign each user an Intune license before users can enroll their devices in Intune.

✔️ **Determine your license needs**
Microsoft Intune is available for different organization sizes and needs, from a simple-to-use management experience for schools and small businesses, to more advanced functionality required by enterprise customers. An admin must have a license assigned to them to administer Intune (unless you have selected to allow unlicensed admins). 
For guidance, go to [Microsoft Intune licensing](licenses.md).

✔️ **Get started with assigning licenses to users**
Whether you added users one at a time or all at once, you must assign each user an Intune license before users can enroll their devices in Intune. The Microsoft Intune free trial provides 25 Intune licenses. For a list of licenses, see Licenses that include Intune.
Give users permission to use Intune. Each user or userless device requires an Intune license to access the service. 
For guidance, go to [Assign licenses](licenses-assign.md).

✔️ **Unlicensed admins**
You can give administrators access to Microsoft Endpoint Manager without them requiring an Intune license. This feature applies to any administrator, including Intune administrators, global administrators, Azure AD administrators, and so on.
For guidance, go to [Unlicensed admins](unlicensed-admins.md).

## 7 - Manage Roles and grant admin permissions for Intune

After you've added users to your Intune tenant, we recommend that you grant a few users administrative permission. Microsoft Intune includes a set of admin roles that you can assign to users in your organization using the Microsoft Intune admin center. Each admin role maps to common business functions and gives people in your organization permissions to do specific tasks in the admin centers.

✔️ **Get started with managing roles**

1. Role-based access control (RBAC) helps you manage who has access to your organization's resources and what they can do with those resources. For guidance, go to [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

2. By assigning roles to your Intune users, you can limit what they can see and change. For guidance, go to [Assign a role to an Intune user](assign-role.md).

3. You can use both the built-in and custom roles. Built-in roles cover some common Intune scenarios. You can create your own custom roles with the exact set of permissions you need. For guidance, go to [Create a custom role in Intune](create-custom-role.md).

4. You can use role-based access control and scope tags to make sure that the right admins have the right access and visibility to the right Intune objects. Roles determine what access admins have to which objects. Scope tags determine which objects admins can see. For guidance, go to [Use role-based access control (RBAC) and scope tags for distributed IT](scope-tags.md)

## 8 - Set the mobile device management authority

The mobile device management (MDM) authority setting determines how you manage your devices. By default, the Intune free trial sets your MDM authority to Intune. As an IT admin, you must set an MDM authority before users can enroll devices for management. With the MDM authority set, you can start enrolling devices.

✔️ **Get started with MDM authority**
If you are changing your tenant to support Intune, you will need to change your MDM authority configuration. 
For guidance, go to [Set the mobile device management authority](mdm-authority-set.md).

## 9 - Customize the Intune company portal

The Company Portal apps, Company Portal website, and Intune app on Android are where users access company data and can do common tasks. Common task may include enrolling devices, installing apps, and locating information (such as for assistance from your IT department).

✔️ **Get started with configuring the company portal**
Customize the Intune Company Portal that users use to enroll devices and install apps. These settings appear in both the Company Portal app and the Intune Company Portal website.
For guidance, go to [Configure the company portal](../apps/company-portal-app.md).


## Follow the minimum recommended baseline policies

1. 🡺 **Set up Microsoft Intune** (*You are here*)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. [Plan for compliance policies](deployment-plan-compliance-policies.md)
4. [Configure device features](deployment-plan-configuration-profile.md)
5. [Enroll devices](deployment-guide-enrollment.md)
