---
# required metadata

title: Setup guide for Microsoft Intune
description: Deployment guide to set up, onboard, or move to Intune. These steps include moving from partner MDM providers, using co-management, moving from on-premises group policy, and moving from Office 365 device management.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/24/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: get-started
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Deployment guide: Setup or move to Microsoft Intune

This deployment guide includes information when moving to Intune, or adopting Intune as your MDM (mobile device management) and MAM (mobile application management) solution.

In this guide, you sign up for Intune, add your domain name, configure Intune as the MDM authority, and more. Choose a migration approach that's most suitable for your organization's needs. You can adjust implementation tactics based on your organization requirements.

> [!TIP]
> [!INCLUDE [tips-guidance-plan-deploy-guides](../includes/tips-guidance-plan-deploy-guides.md)]

## Prerequisites

- **Intune subscription**: Intune is licensed as a stand-alone Azure service, a part of [Enterprise Mobility + Security (EMS)](https://www.microsoft.com/microsoft-365/enterprise-mobility-security), and included with [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise). For more information on how to get Intune, see [Intune licensing](licenses.md).

  In most scenarios, [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise) may be the best option, as it gives you EMS, [Microsoft Endpoint Manager](../../endpoint-manager-overview.md), and Office 365.

  You can also [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).

- Sign in as member of the **Global administrator** Azure AD group. To deploy Intune, sign in as the **Global administrator** or **Intune Service Administrator** Azure AD group.

## Currently don't use anything

If you currently don't use any MDM or MAM provider, then you have some options:

- **Intune + Endpoint Manager**: If you want a cloud solution, then consider going straight to Intune. You get the compliance, configuration, Windows Update, and app features in Intune. You also get the benefits of the Endpoint Manager admin center, which is a web-based console.

  Next, [deploy Intune](#deploy-intune) (in this article).
  
- **Configuration Manager + Endpoint Manager**: If you want the features of Configuration Manager (on-premises) combined with the cloud, then consider [tenant attach](#option-1-add-tenant-attach) or [co-management](#option-2-set-up-co-management). With Configuration Manager, you can:

  - [Manage on-premises devices](../../configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md), including Windows Server or Windows 8.1 devices.
  - [Manage partner or third party software updates](../../configmgr/sum/understand/software-updates-introduction.md).
  - [Create custom task sequences](../../configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks.md) when deploying operating systems.
  - [Deploy and manage many app](../../configmgr/apps/understand/introduction-to-application-management.md) types. 

To help you decide, see [choose a device management solution](../../configmgr/core/plan-design/choose-a-device-management-solution.md).

## Currently use a third party MDM provider

Devices should only have one MDM provider. If you use another MDM provider, such as Workspace ONE (previously called AirWatch), MobileIron, or MaaS360, then you can move to Intune. The biggest challenge is users must unenroll their devices from the current MDM provider, and then enroll in Intune.

> [!IMPORTANT]
> Don't configure Intune and your existing third party MDM solution to apply access controls to resources, including Exchange or SharePoint Online.

Recommendations:

- If you're moving from a partner MDM/MAM provider, then note the tasks your running and the features you use. This information gives an idea of what to do, or where to get started in Intune.
- When devices are unenrolled, they aren't receiving your policies, including policies that provide protection. They're vulnerable until they enroll in Intune. When devices unenroll, we recommend [using conditional access](migration-guide-drive-adoption.md) to block devices until they enroll in Intune.

  Be sure you have specific unenroll and enroll steps. Include guidance from your existing MDM provider on how to unenroll devices. Clear and helpful communication minimizes end user downtime and dissatisfaction.

- Use a phased approach. Start with a small group of pilot users, and add more groups until you reach full scale deployment.
- Monitor the helpdesk load and enrollment success of each phase. Leave time in the schedule to evaluate success criteria for each group before migrating the next group. Your pilot deployment should validate the following tasks:

  - Enrollment success and failure rates are within your expectations.
  - User productivity:

    - Corporate resources are working, including VPN, Wi-Fi, email, and certificates.
    - Deployed apps are accessible.

  - Data security:

    - Review compliance reports, and look for common issues and trends. Communicate issues, resolutions, and trends with your help desk.
    - Mobile app protections are applied.

- When you're satisfied with the first phase of migrations, repeat the migration cycle for the next phase.

  - Repeat the phased cycles until all users are migrated to Intune.
  - Confirm the helpdesk is ready to support end users throughout the migration. Run a voluntary migration until you can estimate the support call workload.
  - Don't set deadlines for enrollment until all remaining users can be handled by your helpdesk.

For enrollment guidance, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

Next, [deploy Intune](#deploy-intune) (in this article).

## Currently use Configuration Manager

Configuration Manager supports Windows and macOS devices, and Windows Servers. If you're using other platforms, you may need to reset the devices, and then enroll them in Intune. Once enrolled, they'll receive the policies and profiles you create. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md) and [cloud attach blog post](https://techcommunity.microsoft.com/t5/configuration-manager-blog/cloud-attach-your-future-part-ii-quot-the-big-3-quot/ba-p/1750664). 

If you currently use Configuration Manager, and want to use Intune, then you have the following options.

### Option 1: Add tenant attach

Tenant attach allows you to upload your Configuration Manager devices to your organization in Intune, also known as a "tenant". After you attach your devices, you use the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to run remote actions, such as sync machine and user policy. You can also see your on-premises servers, and get OS information.

Tenant attach is included with your [Configuration Manager co-management license](../../configmgr/core/understand/product-and-licensing-faq.yml) at no extra cost. It's the easiest way to integrate the cloud (Intune) with your on-premise Configuration Manager setup.

For more information, see [enable tenant attach](../../configmgr/tenant-attach/device-sync-actions.md).

### Option 2: Set up co-management

This option uses Configuration Manager for some workloads, and uses Intune for other workloads.

1. In Configuration Manager, set up [co-management](../../configmgr/comanage/how-to-enable.md).
2. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.

Next, devices are ready to be enrolled, and receive your policies.

Helpful information:

- [What is co-management?](../../configmgr/comanage/overview.md)
- [Co-management workloads](../../configmgr/comanage/workloads.md)
- [Switch Configuration Manager workloads to Intune](../../configmgr/comanage/how-to-switch-workloads.md)
- [Configuration Manager product and licensing FAQ](../../configmgr/core/understand/product-and-licensing-faq.yml)

### Option 3: Move from Configuration Manager to Intune

This scenario is rare. Most existing Configuration Manager customers want to keep using Configuration Manager. Microsoft wants you to continue using Configuration Manager. It includes services that are beneficial for on-premises devices, such as [Desktop Analytics](../../configmgr/desktop-analytics/overview.md), and more.

These steps are an overview, and are only included for those users who want a 100% cloud solution. With this option, you:

- Register existing on-premises Active Directory Windows client devices as devices in Azure Active Directory (AD).
- Move your existing on-premises Configuration Manager workloads to Intune.

This option is more work for administrators, but can create a more seamless experience for existing Windows client devices. For new Windows client devices, it's recommended to [start from scratch with Microsoft 365 and Intune](#option-4-start-from-scratch-with-microsoft-365-and-intune) (in this article).

1. Set up [hybrid Active Directory and Azure AD](/azure/active-directory/devices/hybrid-azuread-join-plan) for your devices. Hybrid Azure AD joined devices are joined to your on-premises Active Directory, and registered with your Azure AD. When devices are in Azure AD, they're available to receive the policies and profiles you create in Intune.

    Hybrid Azure AD support Windows devices. For other prerequisites, including sign-in requirements, see [Plan your hybrid Azure AD join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan).

2. In Configuration Manager, set up [co-management](../../configmgr/comanage/how-to-enable.md).
3. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.
4. In Configuration Manager, [slide all the workloads from Configuration Manager to Intune](../../configmgr/comanage/how-to-switch-workloads.md).
5. On the devices, uninstall the Configuration Manager client. For more information, see [uninstall the client](../../configmgr/core/clients/manage/manage-clients.md#uninstall-the-client).

    Once Intune is set up, you can create an Intune app configuration policy that uninstalls the Configuration Manager client. For example, you could reverse the steps in [Install the Configuration Manager client by using Intune](../../configmgr/core/clients/deploy/deploy-clients-to-windows-computers.md#bkmk_mdm).

Next, devices are ready to be enrolled, and receive your policies.

> [!IMPORTANT]
> Hybrid Azure AD supports only Windows devices. Configuration Manager supports Windows and macOS devices. For macOS devices managed in Configuration Manager, you can:
>
> 1. Uninstall the Configuration Manager client. When you uninstall, the devices aren't receiving your policies, including policies that provide protection. They're vulnerable until they enroll in Intune.
> 2. Enroll the devices in Intune to receive policies.
>
> To help minimize vulnerabilities, move macOS devices after Intune is setup, and your enrollment policies are ready to be deployed.

### Option 4: Start from scratch with Microsoft 365 and Intune

This option applies to Windows client devices. If you use Windows Server OSs, such as Windows Server 2016, then don't use this option. Use Configuration Manager.

1. [Deploy Microsoft 365](/microsoft-365/enterprise/deploy-microsoft-365-enterprise), including creating users and groups.

    Helpful links:

    - [Microsoft 365 Enterprise deployment guide](/microsoft-365/enterprise/deploy-foundation-infrastructure)
    - Set up [Microsoft 365 Business](/microsoft-365/business/set-up)

2. [Deploy Intune](#deploy-intune) (in this article), including setting the MDM Authority to Intune.
3. On existing devices, uninstall the Configuration Manager client. For more information, see [uninstall the client](../../configmgr/core/clients/manage/manage-clients.md#uninstall-the-client).

Next, devices are ready to be enrolled, and receive your policies.

## Currently use on-premises group policy

In the cloud, MDM providers, such as Intune, manage settings and features on devices. Group policies objects (GPO) aren't used. When managing devices, Intune device configuration profiles replace on-premises GPO. These profiles use settings exposed by Apple, Google, and Microsoft. Specifically:

- On Android devices, these profiles use the Android [Management API](https://developers.google.com/android/management/introduction) and [EMM API](https://developers.google.com/android/work/play/emm-api/v1).
- On Apple devices, these profiles use the [Device management payloads](https://developer.apple.com/documentation/devicemanagement).
- On Windows devices, these profiles use the [Windows configuration service providers (CSPs)](/windows/client-management/mdm/configuration-service-provider-reference).

When moving devices from group policy, use [Group policy analytics](../configuration/group-policy-analytics.md). In Endpoint Manager, you import your GPOs, and see which policies are available (and not available) in Intune.

Next, [deploy Intune](#deploy-intune) (in this article).

## Tenant to tenant migration

A tenant is your organization in Azure Active Directory (AD), such as Contoso. It includes a dedicated Azure AD service instance that Contoso receives when it gets a Microsoft cloud service, such as Microsoft Intune or Microsoft 365. Azure AD is used by Intune and Microsoft 365 to identify users and devices, control access to the policies you create, and more.

In Intune, you can export and import some of your policies using [Microsoft Graph](/graph/api/resources/intune-graph-overview) and Windows PowerShell.

For example, you create a Microsoft Intune trial subscription. In this subscription trial tenant, you have policies that configure apps and features, check compliance, and more. You'd like to move these policies to another tenant.

> [!IMPORTANT]
>
> - These steps use the [Intune beta Graph samples](https://github.com/microsoftgraph/powershell-intune-samples) on GitHub. The sample scripts make changes to your tenant. They're available as-is, and should be validated using a non-production or "test" tenant account. Be sure the scripts meet your organization security guidelines.
> - The scripts don't export and import every policy, such as certificate profiles. Expect to do more tasks than what's available in these scripts. You will have to recreate some policies.
> - To migrate a user’s device, the user must unenroll the device from the old tenant, and then re-enroll in the new tenant.

### What you can't do

There are some policy types that can't be exported. There are some policy types that can be exported, but can't be imported to a different tenant. Use the following list as a guide. Know there are other policy types that aren't listed.

| Policy or profile type | Information |
| --- | --- |
| **Applications** | &nbsp; |
| Android line-of-business apps | ❌ Export <br/>❌ Import <br/><br/>To add your LOB app to a new tenant, you also need the original `.apk` application source files.|
| Apple – Volume Purchase Program (VPP) | ❌ Export <br/>❌ Import<br/><br/>These apps are synced with the Apple VPP. In the new tenant, you add your VPP token, which shows your available apps. |
| iOS/iPadOS line-of-business apps | ❌ Export <br/>❌ Import <br/><br/>To add your LOB app to a new tenant, you also need the original `.ipa` application source files.|
| Managed Google Play | ❌ Export <br/>❌ Import<br/><br/>These apps and weblinks are synced with Managed Google Play. In the new tenant, you add your Managed Google Play account, which shows your available apps. |
| Microsoft Store for Business | ❌ Export <br/>❌ Import<br/><br/>These apps are synced with the Microsoft Store for Business. In the new tenant, you add your Microsoft Store for Business account, which shows your available apps.|
| Windows app (Win32) | ❌ Export <br/>❌ Import <br/><br/>To add your LOB app to a new tenant, you also need the original `.intunewin` application source files.|
| **Compliance policies** | &nbsp; |
| Actions for Non-Compliance | ❌ Export <br/>❌ Import<br/><br/>It's possible there could be a link to an e-mail template. When you import a policy that has non-compliance actions, the default actions for non-compliance are added instead. |
| Assignments | ✔️ Export<br/>❌ Import<br/><br/>Assignments are targeted to a group ID. In a new tenant, the group ID is different. |
| **Configuration profiles** | &nbsp; |
| Email |  ✔️ Export <br/> <br/>✔️ If an email profile doesn't use certificates, then the import should work. <br/>❌ If an email profile uses a root certificate, then the profile can't be imported to a new tenant. The root certificate ID is different in a new tenant. |
| SCEP certificate | ✔️ Export<br/><br/>❌ Import <br/><br/>SCEP certificate profiles use a root certificate. The root certificate ID is different in a new tenant. |
| VPN |  ✔️ Export<br/><br/> ✔️ If a VPN profile doesn't use certificates, then the import should work.<br/> ❌ If a VPN profile uses a root certificate, then the profile can't be imported to a new tenant. The root certificate ID is different in a new tenant. |
| Wi-Fi |  ✔️ Export<br/><br/> ✔️ If a Wi-Fi profile doesn't use certificates, then the import should work. <br/>❌ If a Wi-Fi profile uses a root certificate, then the profile can't be imported to a new tenant. The root certificate ID is different in a new tenant. |
| Assignments | ✔️ Export<br/>❌ Import<br/><br/>Assignments are targeted to a group ID. In a new tenant, the group ID is different. |
| **Endpoint Security** | &nbsp; |
| Endpoint detection and response | ❌ Export <br/>❌ Import <br/><br/>This policy is linked to Microsoft Defender for Endpoint. In the new tenant, you configure Microsoft Defender for Endpoint, which automatically includes the **Endpoint detection and response** policy. |

### Download the samples, and run the script

This section includes an overview of the steps. Use these steps as guidance, and know that your specific steps may be different.

1. Download the samples, and use Windows PowerShell to export your policies:

    1. Go to [microsoftgraph/powershell-intune-samples](https://github.com/microsoftgraph/powershell-intune-samples), select **Code** > **Download ZIP**. Extract the contents of the `.zip` file.
    2. Open the Windows PowerShell app as administrator, and change the directory to your folder. For example, enter the following command:

        `cd C:\psscripts\powershell-intune-samples-master`

    3. Install the AzureAD PowerShell module:

        `Install-Module AzureAD`

        Select **Y** to install the module from an untrusted repository. The install can take a few minutes.

    4. Change the directory to the folder with the script you want to run. For example, change the directory to the `CompliancePolicy` folder:

        `cd C:\psscripts\powershell-intune-samples-master\powershell-intune-samples-master\CompliancePolicy`

    5. Run the export script. For example, enter the following command:

        `.\CompliancePolicy_Export.ps1`

        Sign in with your account. When prompted, enter the path to put the policies. For example, enter:

        `C:\psscripts\ExportedIntunePolicies\CompliancePolicies`

    In your folder, the policies are exported.

2. Import your policies in your new tenant:

    1. Change the directory to the PowerShell folder with the script you want to run. For example, change the directory to the `CompliancePolicy` folder:

        `cd C:\psscripts\powershell-intune-samples-master\powershell-intune-samples-master\CompliancePolicy`

    2. Run the import script. For example, enter the following command:

        `.\CompliancePolicy_Import_FromJSON.ps1`

        Sign in with your account. When prompted, enter the path to the policy `.json` file you want to import. For example, enter:

        `C:\psscripts\ExportedIntunePolicies\CompliancePolicies\PolicyName.json`

3. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The policies you imported are shown.

## Deploy Intune

1. Sign in to the [Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), and sign up for Intune. If you have an existing subscription, you can also sign in to it.

    For more information, see [Sign up, or sign in to Intune](account-sign-up.md).

2. Set **Intune Standalone** as the MDM authority. For more information, see [Set the MDM authority](mdm-authority-set.md).

3. Add your domain account, such as `contoso.com`. Otherwise, `your-domain.onmicrosoft.com` is automatically used for the domain. For example, if you don't add your domain account, then `contoso.onmicrosoft.com` may be used.

    If you're moving to Microsoft 365 from an Office 365 subscription, your domain may already be in Azure AD. Intune uses the same Azure AD, and can use your existing domain.

    For more information, see [Add a custom domain name](custom-domain-name-configure.md).

4. Add [users](users-add.md) and [groups](groups-add.md). These users and groups receive the policies you create in Endpoint Manager.

    Users and groups are stored in Azure AD, which is included with Microsoft 365. You may not see the Azure AD branding, but that's what you're using. Azure AD is the backend system that stores users, groups, and devices. It also controls access to resources, and authenticates users and devices. Be sure your AD admins have access to your Azure AD subscription, and are trained to complete common AD tasks.

    If you're moving to Microsoft 365 from an Office 365 subscription, your users and groups are already in Azure AD. Intune uses the same Azure AD, and can use the existing users and groups.

    If you want to move existing users from on-premises Active Directory to Azure AD, then you can set up [hybrid identity](/azure/active-directory/hybrid/whatis-hybrid-identity). Hybrid identities exist in both services - on-premises AD and Azure AD. You can also export Active Directory users using the UI or through script. Do an internet search for your options.

    You can create **device groups** when you need to run administrative tasks based on the device identity, not the user identity. They're useful for managing devices that don't have dedicated users, such as kiosk devices, devices shared by shift workers, or devices assigned to a specific location. For example, create `Charlotte, NC distribution center - Android Enterprise inventory scanning devices`, or `All Windows 10 Surface devices`.

    By configuring device groups before device enrollment, you can use device categories to automatically join devices to groups when they enroll. Then, they receive their group's device policies automatically. For more information, see the [Intune enrollment deployment guide](deployment-guide-enrollment.md).

5. Assign Intune licenses to your users. When license are assigned, user devices can enroll in Intune.

    For more information, see [assign licenses](licenses-assign.md).

6. By default, all device platforms can enroll in Intune. If you want to prevent specific platforms, then create a restriction.

    For more information, see [Create a device platform restriction](../enrollment/create-device-platform-restrictions.md).  

7. Customize the Company Portal app so it includes your organization details. Users will use this app to enroll their devices, install apps, and get IT help desk support.

    For more information, see [Configure the Company Portal app](../apps/company-portal-app.md).

8. Create your administrative team. Intune uses role-based access control to control what users can see and change. As a global administrator, you can assign roles to users, such as Help Desk operator, Application Manager, Intune Role Administrator, and more.

    For more information, see [Role-based access control (RBAC) with Microsoft Intune](role-based-access-control.md).

## Next steps

See the [enrollment deployment guides](deployment-guide-enrollment.md), [device and app management](migration-guide-configure-policies.md), and [app protection](migration-guide-app-protection-policies.md).
