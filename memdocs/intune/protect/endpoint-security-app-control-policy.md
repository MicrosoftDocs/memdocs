---
# required metadata

title: Manage approved apps for Windows devices with App Control for Business policy and Managed Installers in Microsoft Intune | Microsoft Docs
description: Use App Control for Business policies and a managed installer to manage which apps are approved to run on Windows devices that you manage with Microsoft Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: aanavath
---

# Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune

*This feature is in public preview.*

Every day new malicious files and apps appear in the wild. When run on devices in your organization they present a risk, which can be hard to manage or prevent. To help prevent undesired apps from running on your managed Windows devices, you can use Microsoft Intune *App Control for Business policies*.

Intune's App Control for Business policies are part of endpoint security and use the Windows ApplicationControl CSP to manage allowed apps on Windows devices.

Also available through App Control for Business policy, you can use a managed installer policy to add the [*Intune management extension*](../apps/apps-win32-app-management.md) to your Tenant as a [managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer#how-does-a-managed-installer-work). With this extension as a managed installer, the apps you deploy through Intune are automatically tagged by the installer. Tagged apps can be identified by your App Control for Business policies as safe apps that can be allowed to run on your devices.

- The *Intune management extension* is an Intune service that supplements Windows 10 MDM features for Windows 10 and Windows 11 devices. It facilitates the [installation of Win32 apps and PowerShell scripts on managed devices](../apps/apps-win32-app-management.md).

- A *managed installer* uses an AppLocker rule to tag applications you install as trusted by your organization For more information, see [Allow apps installed by a managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer) in the Windows Security documentation.

  Use of a managed installer isn't required to use App Control for Business policies.

The information in this article can help you:

- [Configure the Intune Management Extension as a managed installer](#get-started-with-managed-installers).
- [Configure endpoint security App Control for Business policies](#get-started-with-app-control-for-business-policies).

For related information, see [Windows Defender Application Control](/windows/security/threat-protection/windows-defender-application-control/wdac-and-applocker-overview#windows-defender-application-control) in the Windows Security documentation.

> [!NOTE]
> **App Control for Business policy vs Application control profiles**:
> Intune *App Control for Business policies* use the [ApplicationControl CSP](/windows/client-management/mdm/applicationcontrol-csp). Intune's Attack surface reduction policies use the [AppLocker CSP](/windows/client-management/mdm/applocker-csp) for their *Application control profiles*.
> Windows introduced the **ApplicationControl CSP** to replace the **AppLocker CSP**. Windows continues to support the AppLocker CSP but no longer adds new features to it. Instead, development continues through the ApplicationControl CSP.

Applies to:

- Windows 10
- Windows 11

## Prerequisites

### Devices

The following devices are supported for App Control for Business policies when they are enrolled with Intune:

- **Windows Enterprise or Education**:
  - Windows 10 version 1903 or later
  - Windows 11

- **Windows Professional**:
  - Windows 10 with [KB5019959](https://support.microsoft.com/topic/november-8-2022-kb5019959-os-builds-19042-2251-19043-2251-19044-2251-and-19045-2251-f65e0600-2135-4efd-a979-08d1df34dce8)
  - Windows 11:
    - Version 22H2 with [KB5019980](https://support.microsoft.com/topic/november-8-2022-kb5019980-os-build-22621-819-b503e08b-b850-469a-8de9-74df8aebd5f4)
    - Version 21H2 with [KB5019961](https://support.microsoft.com/topic/november-8-2022-kb5019961-os-build-22000-1219-92b05506-99a5-449f-b3fa-c9bc96b19b67)

- **Windows 11 SE**:
  - Windows 11 SE is supported for Educational tenants only. For more information, see [App Control for Business policies for Education tenants](#app-control-for-business-policies-for-education-tenants) later in this article.

- **Azure Virtual Desktop** (AVD):
  - AVD devices are supported to use App Control for Business policies
  - To target AVD multi session devices, use the App Control for Business node in Endpoint Security. However, App Control for Business is device scope only.

- **Co-managed devices**:
  - To support Application Control for Business Policies on [co-managed](../../configmgr/comanage/workloads.md) devices, set the slider for *Endpoint Protection* slider to *Intune*.

### Windows Defender App Control for Business

See [Windows edition and licensing requirements](/windows/security/threat-protection/windows-defender-application-control#windows-edition-and-licensing-requirements) in *About application control for Windows* in the Windows Security documentation.

### Role based access controls

To manage App Control for Business policies, an account must be assigned an Intune [role-based access control](../fundamentals/role-based-access-control.md) (RBAC) role that includes sufficient permissions and rights to complete a desired task.

The following are the available tasks with their required permissions and rights.

- **Enable use of a managed installer** - Accounts must be assigned the role of **Intune Administrator**. Enabling the installer is a one-time event.

  >[!IMPORTANT]
  >
  > Microsoft recommends that you use roles with the fewest permissions. This helps improve security for your organization. The Intune Administrator and similar accounts are highly privileged roles that should be limited to scenarios that can't use a different role.

- **Manage App Control for Business policy** - Accounts must have the **App Control for Business** permission, which includes rights for *Delete*, *Read*, *Assign*, *Create*, *Update*, and *View Reports*.

- **View reports for App Control for Business policy** - Accounts must have one of the following permissions and rights:

  - The **App Control for Business** permission with *View Reports*.
  - The **Organization** permission with *Read*.

For guidance on assigning the right level of permissions and rights to manage Intune App Control for Business policy, see [Assign-role-based-access-controls-for-endpoint-security-policy](endpoint-security-policy.md#assign-role-based-access-controls-for-endpoint-security-policy).

### Government cloud support

Intune endpoint security Application control policies and configuring a managed installer are supported with the following sovereign cloud environments:

- US Government clouds
- 21Vianet

## Get started with managed installers

With Intune's endpoint security App Control for Business, you can use policy to add the [Intune Management Extension](../apps/apps-win32-app-management.md) as a [managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer#how-does-a-managed-installer-work) on your managed Windows devices.

After you enable a managed installer, all subsequent applications you deploy to Windows devices through Intune are marked with the managed installer tag. The tag identifies that the app was installed by a known source, and can be trusted. The managed installer tagging of apps is then used by App Control for Business policies to automatically identify apps as approved to run on devices in your environment.

App Control for Business policies are an implementation of Windows Defender Application Control (WDAC). To learn more about WDAC and app tagging, see [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) and [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide) in the Windows Defender Application Control documentation.

**Considerations for using a managed installer**:

- Setting a managed installer is a tenant-wide configuration that applies to all your managed Windows devices.

- After you enable the Intune Management extension as a managed installer, all apps you deploy to Windows devices through Intune are tagged with the mark of the managed installer.

- By itself, this tag has no effect on which apps can run on your devices. The tag is used only when you also assign WDAC policies that determine which apps are allowed to run on your managed devices.

- Because there's no retroactive tagging, all apps on your devices that were deployed before enabling the managed installer aren't tagged. If you apply a WDAC policy, you must include explicit configurations to allow these untagged apps to run.

- You can turn off this policy by editing the Managed Installer policy. Turning off the policy prevents subsequent apps from being tagged with the managed installer. Apps that were previously installed and tagged remain tagged. For information about manual clean-up of a managed installer after turning off the policy, see [Remove the Intune Management Extension as a managed installer](#remove-the-intune-management-extension-as-a-managed-installer) later in this article.

[Learn more about how Intune set the managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer) in the Windows Security documentation.

> [!IMPORTANT]
>
> **Potential impact to events collected by any Log Analytics integrations**
>
> Log Analytics is a tool in the Azure Portal which customers may be using to collect data from AppLocker policy events. With this public preview, if you complete the opt-in action, AppLocker policy will begin to deploy to applicable devices in your tenant. Depending on your Log Analytics configuration, especially if you are collecting some of the more verbose logs, [*this will result in an increase in events generated by AppLocker policy*](/windows/security/threat-protection/windows-defender-application-control/applocker/using-event-viewer-with-applocker). If your organization uses Log Analytics, our recommendation is to **review your Log Analytics setup so that you**:
>
> - Understand your Log Analytics setup and ensure there is an appropriate data collection cap in place to avoid unexpected billing costs.
> - Turn off the collection of AppLocker events altogether in Log Analytics (Error, Warning, Information) with the exception of MSI and Script logs.

### Add a managed installer to your tenant

The following procedure guides you through adding the Intune Management Extension as a managed installer for your tenant. Intune supports a single managed installer policy.

1. In the Microsoft Intune admin center, go to **Endpoint security (Preview)**, select the **Managed installer** tab and then select **Add*. The *Add managed installer* pane opens.

   :::image type="content" source="./media/endpoint-security-app-control-policy/add-managed-installer.png" alt-text="Screen shot of the Managed installer page, with the Add managed installer pane on the right side." lightbox="./media/endpoint-security-app-control-policy/add-managed-installer.png" :::

2. Select **Add**, and then **Yes** to confirm the addition of the Intune Management Extension as a managed installer.

3. After adding the Managed installer, in some rare cases, you might need to wait up to 10 minutes before the new policy is added to your tenant. Select **Refresh** to update the admin center periodically, until it's available.

   The policy is ready in the service when Intune displays a managed installer policy with the name **Managed installer – Intune Management Extension** with the status of **Active**. From the client side, you might need to wait up to an hour for the policy to start getting delivered.

   :::image type="content" source="./media/endpoint-security-app-control-policy/managed-installer-policy.png" alt-text="A screenshot of the App Control for Business pane, with the managed installer policy present, and active." lightbox="./media/endpoint-security-app-control-policy/managed-installer-policy.png":::

4. You can now select the policy to edit its configuration. Only the following two policy areas support edits:

   - **Settings**: Editing the policy settings opens the *Opt-out for managed installer* pane, where you can change the value for **Set managed installer** between **On** and **Off**. When you add the installer, the setting *Set managed installer* defaults to *On*. Before changing the configuration, be sure to review the behavior detailed on the pane for *On* and *Off*.

   - **Scope tags**: You can add and modify scope tags that are assigned to this policy. This allows you to specify which admins can view the policy details.

Before the policy has any effect, you must create and deploy an App Control for Business policy to specify rules for which apps can run on your Windows devices.

For more information, see [Allow apps installed by a managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer) in the Windows Security documentation.

> [!IMPORTANT]
>
> **The risk of potential no-boot from AppLocker policy merge**
>
> When enabling managed installer via Intune, an AppLocker policy with a dummy rule is deployed and merged with the existing AppLocker policy on the target device.
> If the existing AppLocker policy includes a RuleCollection defined as **NotConfigured** with an empty rule set, it will be merged as **NotConfigured** with the dummy rule.
> A **NotConfigured** rule collection will default to enforced if there are any rules defined in the collection.
> When the dummy rule is the only rule configured, this implies that anything else will be blocked from being loaded or executed.
> This can cause unexpected problems such as applications failing to start, and failing to boot or logon into Windows.
> To avoid this issue, we recommend removing any RuleCollection defined as **NotConfigured** with an empty rule set from your existing AppLocker policy if it is currently in place.

- Managed Installer can enable stopped or disabled App-Locker Policies (on targeted PCs) enforced from GPO.
  
### Remove the Intune Management Extension as a managed installer

Should you need to, you can stop configuring the Intune Management Extension as a managed installer for your tenant. This requires you to turn off the managed installer policy. After the policy is turned off, you can choose to use additional clean-up actions.

#### Turn off the Intune Management Extension policy (required)

The following configuration is required to stop adding the Intune Management Extension as a managed installer to your devices.

1. In the admin center, go to **Endpoint security (Preview)**, select the **Managed installer** tab, and then select the **Managed installer – Intune Management Extension** policy.

2. Edit the policy, and change **Set managed installer** to **Off**, and save the policy.

New devices won't be configured with the Intune Management Extension as a managed installer. This doesn't remove the Intune Management Extension as managed installer from devices that are already configured to use it.

#### Remove the Intune Management Extension as a managed installer on devices (optional)

As an optional clean-up step, you can run a script to remove the Intune Management Extension as a managed installer on devices that have already installed it. This step is optional as this configuration has no effect on devices unless you also use App Control for Business policies that reference the managed installer.

1. Download the **CatCleanIMEOnly.ps1** PowerShell script. This script is available at [https://aka.ms/intune_WDAC/CatCleanIMEOnly](https://aka.ms/intune_WDAC/CatCleanIMEOnly) from *download.microsoft.com*.

2. Run this script on devices that have the Intune Management Extension set as a managed installer. This script removes only the Intune Management Extension as a managed installer.

3. Restart the Intune Management Extension service for the above changes to take effect.

To run this script, you can use Intune to run [PowerShell scripts](../apps/intune-management-extension.md), or other methods of your choice.

#### Remove all AppLocker policies from a device (optional)

To remove *all* Windows AppLocker policies from a device, you can use the **CatCleanAll.ps1** PowerShell script. This script removes not only the Intune Management Extension as a managed installer, but *all* policies based on Windows AppLocker from a device. Before using this script, be sure you understand your organizations use of AppLocker policies.

1. Download the **CatCleanAll.ps1** PowerShell script. This script is available at [https://aka.ms/intune_WDAC/CatCleanAll]( https://aka.ms/intune_WDAC/CatCleanAll) from *download.microsoft.com*.

2. Run this script on devices that have the Intune Management Extension set as a managed installer. This script removes the Intune Management Extension as a managed installer and AppLocker policies from the device.

3. Restart the Intune Management Extension service for the above changes to take effect.

To run this script, you can use Intune to run [PowerShell scripts](../apps/intune-management-extension.md), or other methods of your choice.

## Get started with App Control for Business policies

With Intune's endpoint security App Control for Business policies, you can manage which apps on your managed Windows devices are allowed to run. Any apps that aren't explicitly allowed to run by a policy are blocked from running unless you've configured the policy to use an Audit mode. With audit mode, the policy allows all apps to run and logs the details about them locally on the client.

To manage which apps are allowed or blocked, Intune uses the Windows ApplicationControl CSP on Windows devices.

When you create an App Control for Business policy, you must choose a **Configuration settings format** to use:

- **Enter xml data** - When you choose to enter xml data, you must provide the policy with a set of custom XML properties that define your App Control for Business policy.

- **Built-in controls** – This option is the simplest path to configure yet remains a powerful choice. With the built-in controls, you can easily approve all apps that are installed by a managed installer, and allow trust of Windows components and store apps.

  More details about these options are available from the UI when creating a policy, and also detailed in the following procedure that walks you through creating a policy.

After you create an [App Control for Business policy](#create-an-app-control-for-business-policy), you can expand the scope of that policy by creating [supplemental policies](#use-supplemental-policy) that add more rules in XML format to that original policy. When you use supplemental policies, the original policy is referred to as the base policy.

> [!NOTE]
>
> If your tenant is an Educational Tenant, see [App Control for Business policies for Education tenants](#app-control-for-business-policies-for-education-tenants) to learn about additional device support and App Control for Business policy for those devices.

### Create an App Control for Business policy

Use the following procedure to help you create a successful App Control for Business policy. This policy is considered a *base* policy if you go on to create [supplemental policies](#use-supplemental-policy) to expand the scope of trust you define with this policy.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **App Control for Business (Preview)** > select the **App Control for Business** tab > and then select **Create Policy**. App Control for Business policies are automatically assigned to a platform type of *Windows 10 and later*.

   :::image type="content" source="./media/endpoint-security-app-control-policy/create-app-control-policy.png" alt-text="Screen capture that shows the path in the admin center to create a new App Control for Business policy." lightbox="./media/endpoint-security-app-control-policy/create-app-control-policy.png":::

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, choose a **Configuration settings format**:

   **Enter xml data** - With this option you must provide custom XML properties to define your App Control for Business policy. If you select this option but don't add XLM properties to the policy, it acts as *Not configured*. An App Control for Business policy that isn't configured results in default behaviors on a device, with no added options from the ApplicationControl CSP.

   **Built-in controls** – With this option the policy doesn't use custom XML. Instead, configure the following settings:

   - **Enable trust of Windows components and store apps** – When this setting is *Enabled* (the default), managed devices can run Windows components and store apps, as well as other apps you might configure as trusted. Apps that aren't defined as trusted by this policy are blocked from running.

     This setting also supports an *Audit only* mode. With audit mode, all events are logged in the local client logs, but apps aren't blocked from running.

   - **Select additional options for trusting apps** – For this setting you can select one or both of the following options:

     - **Trust apps with a good reputation** – This option allows devices to run reputable apps as defined by the Microsoft Intelligent Security Graph. For information on using the *Intelligent Security Graph* (ISG), see [Allow reputable apps with Intelligent Security Graph (ISG)](/windows/security/application-security/application-control/windows-defender-application-control/design/use-wdac-with-intelligent-security-graph) in the Windows Security documentation.

     - **Trust apps from managed installers** – This option allows devices to run the apps that were deployed by an authorized source, which is a managed installer. This applies to apps you deploy through Intune after you configure the Intune Management Extension as a managed installer.

       Behavior for all other apps and files that aren't specified by rules in this policy depend on the configuration of *Enable trust of Windows components and store apps*:

       - If *Enabled*, files and apps are blocked from running on devices.
       - If set to *Audit only*, files and apps are audited only in local client logs.

   :::image type="content" source="./media/endpoint-security-app-control-policy/built-in-controls.png" alt-text="This screen capture shows the default options and settings for App Control for Business policy when you use the built-in-controls." lightbox="./media/endpoint-security-app-control-policy/built-in-controls.png":::

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy, but consider that WDAC policies apply to only the device scope. To continue, select **Next**.

   For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

6. For **Review + create**, review your settings and then select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

### Use supplemental policy

One or more supplemental policies can help you expand on an App Control for Business base policy to increase the circle of trust of that policy. A supplemental policy can expand only one base policy, but multiple supplementals can expand the same base policy. When you add supplemental policies, the applications allowed by the base policy and its supplemental policies are allowed to run on devices.

Supplemental policies must be in XML format, and must reference the Policy ID of the base policy.

The Policy ID of an App Control for Business base policy is determined by the configuration of the base policy:

- Base policies that are created using *custom XML* have a unique PolicyID that's based on that XML configuration.

- Base policies that are created using the *built-in controls* for App Control for Business, have one of four possible PolicyID's that are determined by the possible combinations of the built-in settings. The following table identifies the combinations and the related PolicyID:

  | PolicyID of a base policy | Options in WDAC policy (*Audit* or *Enforce*) |
  |--|--|
  | {A8012CFC-D8AE-493C-B2EA-510F035F1250} | Enable app control policy to trust Windows components and Store apps |
  | {D6D6C2D6-E8B6-4D8F-8223-14BE1DE562FF} | Enable app control policy to trust Windows components and Store apps </br>**And**</br> Trust apps with good reputation |
  | {63D1178A-816A-4AB6-8ECD-127F2DF0CE47} | Enable app control policy to trust Windows components and Store apps </br>**And**</br> Trust apps from managed installers |
  | {2DA0F72D-1688-4097-847D-C42C39E631BC} | Enable app control policy to trust Windows components and Store apps </br>**And**</br> Trust apps with good reputation </br>**And**</br> Trust apps from managed installers |

Even though two App Control for Business policies that use the same configuration of built-in controls have the same PolicyID, you can apply different supplemental policies based on the *assignments* for your policies.

**Consider the following scenario**:

- You create two base policies that use the same configuration and therefore they have the same PolicyID. You deploy one of them to your Executive team, and the second policy deploys to your Help Desk team.

- Next, you create a supplemental policy that allows other apps to run that your Executive team requires. You assign this supplemental policy to that same group, the Executive team.

- Then you create a second supplemental policy that allows various tools required by your Help Desk team to be run. This policy is assigned to the Help Desk group.

As a result of these deployments, both supplemental policies could modify both instances of the base policy. However, due to the distinct and separate assignments, the first supplemental policy modifies only the allowed apps assigned to the Executive team, and the second policy modifies only the allowed apps used by the Help Desk team.

#### Create a supplemental policy

1. Use the Windows Defender Application Control Wizard or PowerShell cmdlets to generate an App Control for Business policy in XML format.

   To learn about the Wizard, see ***aka.ms/wdacWizard*** or [Microsoft WDAC Wizard](https://webapp-wdac-wizard.azurewebsites.net/).

   When you create a policy in XML format, it must reference the *Policy ID* of the base policy.

2. After your App Control for Business supplemental policy has been created in XML format, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **App Control for Business (Preview)** > select the **App Control for Business** tab, and then select **Create Policy**.

3. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.

   - **Description**: Enter a description for the profile. This setting is optional but recommended.

4. On **Configuration settings**, for **Configuration settings format** select **Enter xml data** and upload your XML file.

5. For **Assignments**, select the same groups as assigned to the base policy you want the supplemental policy to apply to, and then select **Next**.

6. For **Review + create**, review your settings and then select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## App Control for Business policies for Education tenants

App Control for Business policies in tenants for Educational organizations also support **Windows 11 SE** in addition to the supported platforms in the [Prerequisites](#prerequisites).

[Windows 11 SE](/intune-education/windows-11-se-overview) is a cloud-first operating system that's optimized for use in classrooms. Much like Intune for Education, Windows SE 11 prioritizes productivity, student privacy, and learning, and only supports features and apps that are essential for education.

To aid this optimization, WDAC policy and the Intune management Extension are configured automatically for Windows 11 SE devices:

- Intune support for Windows 11 SE devices is scoped to [deploying predefined WDAC policies](/intune-education/windows-11-se-overview) with a set list of apps in EDU tenants. These policies are automatically deployed and can't be changed.

- For Intune EDU tenants, the Intune Management Extension is automatically set as a Managed Installer. This configuration is automatic and can't be changed.

## Delete App Control for Business policy

As detailed in [Deploy WDAC policies using Mobile Device Management (MDM) (Windows 10) - Windows security](/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-intune#remove-wdac-policies-on-windows-10-1903) in the Windows Security documentation, policies deleted from the Intune UI are removed from the system, and from devices, but stay in effect until the next reboot of the machine.

**To disable or delete WDAC enforcement**:

1. Replace the existing policy with a new version of the policy that will **`Allow /*`**, like the rules in the example policy found on Windows devices at `%windir%\schemas\CodeIntegrity\ExamplePolicies\AllowAll.xml`

   This configuration removes any blocks that might otherwise be left in place on a device after the policy is removed.

2. After the updated policy is deployed, you can then delete the new policy from the Intune portal.

This sequence prevents anything from being blocked and fully removes the WDAC policy on the next reboot.

## Monitor App Control for Business policies and the managed installer

After devices are assigned App Control for Business and Managed installer policies, you can view policy details within the admin center.

- To view reports, your account must have the *Read* permission for the Intune role-based access control category of **Organization**.

To view reports, sign in to the Intune admin center and navigate to the Account Control node. (**Endpoint security** > **Account Control (Preview)**). Here you can select the tab for the policy details you want to view:

### Managed installer

On the **Managed Installer** tab, you can view the status, success count, and error details for the *Managed installer – Intune Management Extension* policy:

:::image type="content" source="./media/endpoint-security-app-control-policy/view-managed-installer-policy.png" alt-text="This screen capture shows a view of the managed installer policy Overview page." lightbox="./media/endpoint-security-app-control-policy/view-managed-installer-policy.png":::

Select the policy name to open its Overview page, where you can view the following information:
  
- **Device status**, a static count of success vs errors.

- **Device status trend**, a historical chart that displays a timeline and count of devices in each detail category.

Report details include:

- Succeeded - Devices that successfully applied the policy.
- Error - Devices with errors.
- New devices – New devices identifies devices that have recently applied the policy. 

  :::image type="content" source="./media/endpoint-security-app-control-policy/managed-installer-policy-overview.png" alt-text="This screen capture shows the managed installer Overview." lightbox="./media/endpoint-security-app-control-policy/managed-installer-policy-overview.png":::

It can take up to 24 hours for the **Device status** and **Device status trend** sections to update in the Overview.

While viewing the policy details, you can select **Device status** (below *Monitor*), to open a device-based view of the policy details. The *Device status* view displays the following details that you can use to identify problems should a device fail to successfully apply the policy:

- Device name
- User name
- OS version
- Managed installer status (*Succeeded* or *Error*)

It can take several minutes for the device-based view of the policy details to update after the device actually receives the policy. 

### App Control for Business

On the **App Control for Business** tab, you can view the list of your App Control for Business policies and basic details including if its assigned and when it was last modified.

Select a policy to open a view that more report options:

:::image type="content" source="./media/endpoint-security-app-control-policy/application-control-policy-view.png" alt-text="This screen capture shows a per-policy status view, and tiles for two additional reports." lightbox="./media/endpoint-security-app-control-policy/application-control-policy-view.png":::

Report options for the policy include:

- **Device and user check-in status** - A simple chart that displays the count of devices reporting each available status for this policy.

- **View Report** - This opens a view with a list of the devices that received this policy. Here you can select devices to drill in and view their App Control for Business policy settings format.

The policy view also includes the following report tiles:

- **Device assignment status** - This report shows all the devices that are targeted by the policy, including devices in a pending policy assignment state.

  With this report, you can select the *Assignment status* values you want to view, and then select **Generate report** to refresh the report view individual devices that received the policy, their last active user, and the assignment status.

  You can also select devices to drill in and view their App Control for Business policy settings format.

- **Per setting status** - This report displays a count of devices that report status as *Success*, *Error*, or *Conflict* for the settings from this policy.

## Frequently asked Questions

### When should I set the Intune Management Extension as the managed installer?

We recommend configuring the Intune Management Extension as the managed installer at your next available opportunity.

Once set, subsequent apps you deploy to devices are appropriately tagged to support WDAC policies that *Trust apps from managed installers*.

In environments where apps deployed before a managed installer was configured, we recommend you deploy new WDAC policies in *audit-mode* so you can identify the apps were deployed but not tagged as trusted. You can then review the audit results and determine which apps should be trusted. For apps you'll trust and allow to run, you can then create custom WDAC policies to allow those apps.

It can be helpful to explore [Advanced Hunting, which is a feature in Microsoft Defender for Endpoint](/windows/security/threat-protection/windows-defender-application-control/querying-application-control-events-centrally-using-advanced-hunting) that makes it easier to query audit events across the many machines that IT admins manage and help them craft policies.

### What do I do with the old Application Control policy from my Attack surface reduction policy

You might notice instances of the Application Control policy in the Intune UI under **Endpoint Security** > **Attach Surface Reduction** or under **Devices** > **Manage devices** > **Configuration**. These will be deprecated in a future release.

### What if I have multiple base or supplemental policies on the same device?

Prior to Windows 10 1903, App Control for Business only supported a single active policy on a system at any given time. That behavior significantly limits customers in situations where multiple policies with different intents would be useful. Today, multiple base and supplemental policies are supported on the same device. Learn more about [deploying multiple App Control for Business policies](/windows/security/application-security/application-control/windows-defender-application-control/design/deploy-multiple-wdac-policies).

On a related note, there's no longer a limitation of 32 policies active on the same device for App Control for Business. This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows are expected receive this fix in future Windows security updates.

### Does the Managed Installer opt-in capability for my tenant set apps installed from Configuration Manager with the appropriate tag?

No. This release focuses on setting apps installed from Intune, using the Intune Management Extension, as the Managed Installer. It can't set Configuration Manager as the Managed Installer.

If setting Configuration Manager as the Managed Installer is desired, you can allow that behavior from within Configuration Manager. If you already have Configuration Manager set as the Managed Installer, the expected behavior is that the new Intune Management Extension AppLocker policy merges with the existing Configuration Manager policy.

### What considerations should I have for Entra Hybrid Join (HAADJ) devices within my organization that want to use Managed Installer?

Entra hybrid join devices require connectivity to an on-premises Domain Controller (DC) to apply Group Policies including the Managed Installer policy (through AppLocker). Without DC connectivity, especially during Autopilot provisioning, Managed Installer policy won't successfully apply. Consider:

1. Use Autopilot with Entra join instead. See our recommendation for [which Entra join option](../../solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined.md#which-option-is-right-for-your-organization) to choose for more information.

2. For Entra hybrid join, choose one or both of the following:
   - Use device provisioning methods that provide DC connectivity at the time of app install as Autopilot might not work here.
   - Deploy apps after the Autopilot provisioning is complete, so that DC connectivity is established at the time of app install and Managed Installer policy can apply.

## Next Steps

[Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy)
