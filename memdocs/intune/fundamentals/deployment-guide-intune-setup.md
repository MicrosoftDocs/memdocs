---
# required metadata

title: Setup guide for Microsoft Intune - Azure | Microsoft Docs
description: Deployment to set up, onboard, or move to Intune. These steps include moving from partner MDM providers, using co-management, moving from on-premises group policy, and moving from Office 365 device management.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: M365-identity-device-management
---

# Deployment guide: Setup or move to Microsoft Intune

In this guide, you sign up for Intune, add your domain name, configure Intune as the MDM authority, and more.

## Prerequisites

- **Intune subscription**: Intune is available as a stand-alone Azure service, a part of [Enterprise Mobility + Security (EMS)](https://www.microsoft.com/microsoft-365/enterprise-mobility-security), and included with [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise). For more information on how to get Intune, see [Intune licensing](..//fundamentals/licenses.md).

  In most scenarios, [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise) may be the best option, as it gives you EMS, [Microsoft Endpoint Manager](https://docs.microsoft.com/mem/endpoint-manager-overview), and Office 365.

  You can also [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

- Sign in as member of the **Global administrator** Azure AD group. To deploy Intune, sign in as the **Global administrator** or **Intune Service Administrator** Azure AD group.

## Currently use Configuration Manager

Configuration Manager supports Windows and macOS devices. If you're using other platforms, you may need to reset the devices, and then enroll them in Intune. Once enrolled, they'll receive the policies and profiles you create. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

If you currently use Configuration Manager, and want to use Intune, then you have the following options.

### Option 1: Set up co-management

This option continues to use Configuration Manager for some workflows, and uses Intune for other workflows.

1. In Configuration Manager, set up [co-management](https://docs.microsoft.com/configmgr/comanage/how-to-enable).
2. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.

Helpful information:

- [What is co-management?](https://docs.microsoft.com/configmgr/comanage/overview)
- [Co-management workloads](https://docs.microsoft.com/configmgr/comanage/workloads)
- [Switch Configuration Manager workloads to Intune](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)
- [Configuration Manager product and licensing FAQ](https://docs.microsoft.com/configmgr/core/understand/product-and-licensing-faq)

### Option 2: Move from Configuration Manager to Intune

This option:

- Existing Windows 10 devices in on-premises Active Directory are registered as devices in Azure Active Directory (AD).
- Moves your existing on-premises Configuration Manager workflows to Intune.

This option is more work for administrators, but can create a more seamless experience for existing Windows 10 devices. For new Windows 10 devices, it's recommended to [start from scratch with Microsoft 365 and Intune](#option-3-start-from-scratch-with-microsoft-365-and-intune) (in this article).

1. Set up [hybrid Active Directory and Azure AD](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) for your devices. Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. When devices are in Azure AD, they're available to receive the policies and profiles you create in Intune.

    Hybrid Azure AD support Windows devices. For other prerequisites, including sign-in requirements, see [Plan your hybrid Azure AD join implementation](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

2. In Configuration Manager, set up [co-management](https://docs.microsoft.com/configmgr/comanage/how-to-enable).
3. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.
4. In Configuration Manager, [slide all the workflows from Configuration Manager to Intune](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads).
5. On the devices, uninstall the Configuration Manager client. For more information, see [uninstall the client](https://docs.microsoft.com/configmgr/core/clients/manage/manage-clients#BKMK_UninstalClient).

    Once Intune is set up, you can create an Intune app configuration policy that uninstalls the Configuration Manager client. For example, you could reverse the steps in [Install the Configuration Manager client by using Intune](https://docs.microsoft.com/configmgr/core/clients/deploy/deploy-clients-to-windows-computers#bkmk_mdm).

> [!IMPORTANT]
> Hybrid Azure AD supports only Windows devices. Configuration Manager supports macOS devices. For macOS devices managed in Configuration Manager, you can:
>
> 1. Uninstall the Configuration Manager client. When you uninstall, the devices aren't receiving your policies, including policies that provide protection. They're vulnerable until they enroll in Intune.
> 2. Enroll the devices in Intune to receive policies.
>
> To help minimize vulnerabilities, move macOS devices after Intune is setup and your enrollment policies are ready to be deployed.

### Option 3: Start from scratch with Microsoft 365 and Intune

This option applies to

1. [Deploy Microsoft 365](https://docs.microsoft.com/microsoft-365/enterprise/deploy-microsoft-365-enterprise?view=o365-worldwide), including creating users and groups.

    Helpful links:

    - [Microsoft 365 Enterprise deployment guide](https://docs.microsoft.com/microsoft-365/enterprise/deploy-foundation-infrastructure?view=o365-worldwide)
    - Set up [Microsoft 365 Business](https://docs.microsoft.com/microsoft-365/business/set-up?view=o365-worldwide)

2. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.
3. On existing devices, uninstall the Configuration Manager client. For more information, see [uninstall the client](https://docs.microsoft.com/configmgr/core/clients/manage/manage-clients#BKMK_UninstalClient).

## Currently use on-premises group policy

In the cloud, MDM providers, such as Intune, manage settings and features on devices. Group policies objects (GPO) aren't used. When managing devices, Intune device configuration profiles replace on-premises GPO.

When moving devices from group policy, you may want to reset these devices, and enroll them in Intune. Once enrolled, they'll receive the policies and profiles you create.

For more information, see the [Intune device configuration deployment guide](deployment-guide-compliance-configuration.md).

Next, [deploy Intune](#deploy-intune) (in this article).

## Currently use a third party MDM provider

Devices should only have one MDM provider. It's common to switch from another MDM provider, such as AirWatch, MobileIron, or MaaS360, to Intune. The biggest challenge is users must unenroll their devices from the current MDM provider, and then enroll in Intune. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

If you're moving from a partner MDM/MAM provider, note the tasks your running and the features you use. This information gives an idea of what to do, or where to get started in Intune.

Next, [deploy Intune](#deploy-intune) (in this article).

## Currently don't use anything

If you currently don't use any MDM or MAM provider, then go straight to Intune. Next, [deploy Intune](#deploy-intune) (in this article).

## Deploy Intune

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and sign up for Intune. If you have an existing subscription, you can also sign in to it.

    For more information, see [Sign up, or sign in to Intune](account-sign-up.md).

2. Set **Intune Standalone** as the MDM authority. For more information, see [Set the MDM authority](mdm-authority-set.md).

3. Add your domain account, such as `contoso.com`. Otherwise, `your-domain.onmicrosoft.com` is automatically used for the domain. For example, if you don't add your domain account, then `contoso.onmicrosoft.com` may be used.

    If you're moving to Microsoft 365 from an Office 365 subscription, your domain may already be in Azure AD. Intune uses the same Azure AD, and can use your existing domain.

    For more information, see [Add a custom domain name](custom-domain-name-configure.md).

4. Add [users](users-add.md) and [groups](groups-add.md). These users and groups receive the policies you create in Endpoint Manager.

    Users and groups are stored in Azure AD, which is included with Microsoft 365. You may not see the Azure AD branding, but that's what you're using. Azure AD is the backend system that stores users, groups, and devices. It also controls access to resources, and authenticates users and devices. Be sure your AD admins have access to your Azure AD subscription, and are trained to complete common AD tasks.

    If you're moving to Microsoft 365 from an Office 365 subscription, your users and groups are already in Azure AD. Intune uses the same Azure AD, and can use the existing users and groups.

    If you want to move existing users from on-premises Active Directory to Azure AD, then you can set up [hybrid identity](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity). Hybrid identities exist in both services - on-premises AD and Azure AD. You can also export Active Directory users using the UI or through script. Do an internet search for your options.

    You can create **device groups** when you need to run administrative tasks based on the device identity, not the user identity. They're useful for managing devices that don't have dedicated users, such as kiosk devices, devices shared by shift workers, or devices assigned to a specific location. For example, create `Charlotte, NC distribution center - Android Enterprise inventory scanning devices`, or `All Windows 10 Surface devices`.

    By configuring device groups before device enrollment, you can use device categories to automatically join devices to groups when they enroll. Then, they receive their group's device policies automatically. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

5. Assign Intune licenses to your users. When license are assigned, users' devices can enroll in Intune.

    For more information, see [assign licenses](licenses-assign.md).

6. By default, all device platforms can enroll in Intune. If you want to prevent specific platforms, then create a restriction.

    For more information, see [Create a device type restriction](../enrollment/enrollment-restrictions-set.md#create-a-device-type-restriction).

7. Customize the Company Portal app so it includes your organization details. Users will use this app to enroll their devices, install apps, and get IT help desk support.

    For more information, see [Configure the Company Portal app](../apps/company-portal-app.md).

8. Create your administrative team. Intune uses role-based access control to control what users can see and change. As a global administrator, you can assign roles to users, such as Help Desk operator, Application Manager, Intune Role Administrator, and more.

    For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Common issues and resolutions

In this section, add extra information provided by CSS and PFE teams.

## Next steps

[Enrollment deployment guide](deployment-guide-enrollment.md)  
[Compliance and configuration deployment guide](deployment-guide-compliance-configuration.md)  
App deployment guide
