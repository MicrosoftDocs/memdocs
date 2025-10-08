---
title: Manage approved apps for Windows devices with App Control for Business policy and Managed Installers in Microsoft Intune | Microsoft Docs
description: Use App Control for Business policies and a managed installer to manage which apps are approved to run on Windows devices that you manage with Microsoft Intune.
author: brenduns
ms.author: brenduns
ms.date: 09/17/2025
ms.topic: how-to
ms.collection:
- M365-identity-device-management
- highpri
- sub-secure-endpoints
ms.reviewer: nicolezhao
---

# Manage approved apps for Windows devices with App Control for Business policy and Managed Installers for Microsoft Intune

Every day new malicious files and apps appear in the wild. When run on devices in your organization they present a risk, which can be hard to manage or prevent. To help prevent undesired apps from running on your managed Windows devices, you can use Microsoft Intune *App Control for Business policies*.

Intune's App Control for Business policies are part of endpoint security and use the Windows ApplicationControl Configuration Service Provider (CSP) to manage allowed apps on Windows devices.

Also available through App Control for Business policy, you can use a managed installer policy to add the [*Intune management extension*](../apps/apps-win32-app-management.md) to your Tenant as a [managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer#how-does-a-managed-installer-work). With this extension as a managed installer, the apps you deploy through Intune are automatically tagged by the installer. Tagged apps are identified by your App Control for Business policies as safe apps that are allowed to run on your devices.

- The *Intune management extension* is an Intune service that supplements Windows MDM features for Windows devices. It facilitates the [installation of Win32 apps and PowerShell scripts on managed devices](../apps/apps-win32-app-management.md).

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

- Windows

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]


## Prerequisites

### Devices

> [!IMPORTANT]
> [!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

The following devices are supported for App Control for Business policies when they're enrolled with Intune:

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

With Intune's endpoint security App Control for Business, you can use policies to add the [Intune Management Extension](../apps/apps-win32-app-management.md) as a [managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer#how-does-a-managed-installer-work) on your managed Windows devices.

After you enable a managed installer on a device, all subsequent applications you deploy to Windows devices through Intune are marked with the managed installer tag. The tag identifies that the app was installed by a known source, and can be trusted. The managed installer tagging of apps is then used by App Control for Business policies to automatically identify apps as approved to run on devices in your environment.

App Control for Business policies are an implementation of Windows Defender Application Control (WDAC). To learn more about WDAC and app tagging, see [About application control for Windows](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) and [WDAC Application ID (AppId) Tagging guide](/windows/security/threat-protection/windows-defender-application-control/appidtagging/windows-defender-application-control-appid-tagging-guide) in the Windows Defender Application Control documentation.

**Considerations for using a managed installer**:

- You deploy one or more *App Control for Business* policies for a managed installer to different groups of managed Windows devices.

  > [!TIP]
  > On August 18, 2025, Intune replaced a single tenant-wide policy for adding a managed installer to Windows devices with a new policy design that supports assignment of a managed installer to selected groups. If you had the tenant-wide policy in place prior to August 18, that policy is converted to a policy that targets all devices, which is equivalent to the original configuration. If you prefer to use a more granular deployment of the managed installer, consider deleting the existing policy and then create new policies to target specific groups or use specific scope tags.

- After Windows devices receive a policy that adds the Intune Management extension as a managed installer, all apps you deploy to those devices through Intune are tagged with the mark of the managed installer.

- To prevent new devices from adding a managed installer, you can edit policy to exclude groups of devices, or delete the managed installer policy from Intune. However, exclusion from a policy or deletion of a policy doesn't remove the managed installer from devices that previously added it.

- By itself, this tag has no effect on which apps can run on your devices. The tag is used only when you also assign WDAC policies that determine which apps are allowed to run on your managed devices.

- Because there's no retroactive tagging, all apps on your devices that were deployed before enabling the managed installer aren't tagged. If you apply a WDAC policy, you must include explicit configurations to allow these untagged apps to run.

- You can [disable a policy](#disable-the-intune-management-extension-policy-required) to prevent subsequent apps from being tagged with the managed installer. Apps that were previously installed and tagged remain tagged. For information about manual clean-up of a managed installer after turning off the policy, see [Remove the Intune Management Extension as a managed installer](#remove-the-intune-management-extension-as-a-managed-installer) later in this article.

[Learn more about how Intune set the managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer) in the Windows Security documentation.

> [!IMPORTANT]
>
> **Potential impact to events collected by any Log Analytics integrations**
>
> Log Analytics is a tool in the Azure portal which customers might use to collect data from AppLocker policy events. If you complete the opt-in action, AppLocker policy begins to deploy to applicable devices in your tenant. Depending on your Log Analytics configuration, especially if you're collecting some of the more verbose logs, [*this results in an increase in events generated by AppLocker policy*](/windows/security/threat-protection/windows-defender-application-control/applocker/using-event-viewer-with-applocker). If your organization uses Log Analytics, our recommendation is to **review your Log Analytics setup so that you**:
>
> - Understand your Log Analytics setup and ensure there's an appropriate data collection cap in place to avoid unexpected billing costs.
> - Turn off the collection of AppLocker events altogether in Log Analytics (Error, Warning, Information) except for MSI and Script logs.

### Add a managed installer to your tenant

You can create one or more managed installer policies to add the managed installer to groups of devices. When creating more than one policy, consider the following that apply to devices targeted by more than a single managed installer policy:

- So long as one policy has the setting *Enable Intune Managed Extension as Managed Installer* set to *Enabled*, the device applies the configuration as enabled.
- Scope tags from more than one policy apply to a device as a superset of those scope tags.

The following procedure guides you through adding the Intune Management Extension as a managed installer for your tenant:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Endpoint security** > **App Control for Business** > select the **Managed installer** tab and then select **Create**. The *Create Managed Installer Policy* workflow opens.

   :::image type="content" source="./media/endpoint-security-app-control-policy/add-managed-installer.png" alt-text="Screen shot of the Managed installer page, with the Add managed installer pane on the right side." lightbox="./media/endpoint-security-app-control-policy/add-managed-installer.png" :::

2. On the **Basics** page, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Settings**, set *Enable Intune Managed Extension as Managed Installer* to *Enabled*, the default. When enabled, devices with this policy use the managed installer. When disabled, the device doesn't actively use the managed installer.

   > [!TIP]
   > You can edit a policy at any time to edit the value of *Enable Intune Managed Extension as Managed Installer*.

4. On the **Scope tags**, optionally you can select any desired scope tags to apply.

5. For **Assignments**, you can *Include* and *Exclude* device groups from the policy. To continue, select **Next**.

   > [!TIP]
   > Although you can target security groups that might include users, only the devices in the security group will be targeted and receive the managed installer policy. This is because managed installer policies only apply to the device scope.

6. For **Review + create**, review your settings and then select **Create** to save your changes and deploy the policy to members of the assigned groups. The policy is also shown in the policy list.

After adding the Managed installer, you might need to wait up to 10 minutes before the new policy is added to your tenant. Select **Refresh** to update the admin center periodically, until it's available.

When ready, the policy is listed on the Managed installer tab and a status of **Active**. Devices might see a wait of up to 30 minutes before the policy gets delivered.

:::image type="content" source="./media/endpoint-security-app-control-policy/managed-installer-policy.png" alt-text="A screenshot of the Managed Installer pane, with a managed installer policy present, and active." lightbox="./media/endpoint-security-app-control-policy/managed-installer-policy.png":::

Before the policy has any effect, you must create and deploy an App Control for Business policy to specify rules for which apps can run on your Windows devices.

For more information, see [Allow apps installed by a managed installer](/windows/security/threat-protection/windows-defender-application-control/configure-authorized-apps-deployed-with-a-managed-installer) in the Windows Security documentation.

> [!IMPORTANT]
>
> **The risk of potential no-boot from AppLocker policy merge**
>
> When enabling managed installer via Intune, an AppLocker policy with a dummy rule is deployed and merged with the existing AppLocker policy on the target device.
> If the existing AppLocker policy includes a RuleCollection defined as **NotConfigured** with an empty rule set, it's merged as **NotConfigured** with the dummy rule.
> A **NotConfigured** rule collection defaults to enforced if there are any rules defined in the collection.
> When the dummy rule is the only rule configured, this implies that anything else is blocked from being loaded or executed.
> This can cause unexpected problems such as applications failing to start, and failing to boot or sign-in into Windows.
> To avoid this issue, we recommend removing any RuleCollection defined as **NotConfigured** with an empty rule set from your existing AppLocker policy if it's currently in place.

- Managed installers can enable stopped or disabled App-Locker Policies (on targeted PCs) enforced from GPO.

### Remove the Intune Management Extension as a managed installer

Should you need to, you can stop policies from configuring the Intune Management Extension as a managed installer for your tenant. This requires you to disable each managed installer policy. After a policies are turned off, you can choose to use additional clean-up actions.

#### Disable the Intune Management Extension policy (required)

The following configuration is required to configure a policy to stop adding the Intune Management Extension as a managed installer to devices.

1. In the admin center, go to **Endpoint security** >  **App Control for Business** > select the **Managed installer** tab, and then select the policy you want to edit.

2. Edit the policy, and change **Enable Intune Managed Extension as Managed Installer** to **Disabled**, and save the policy.

New devices aren't configured with the Intune Management Extension as a managed installer. This doesn't remove the Intune Management Extension as managed installer from devices that are already configured to use it.

#### Remove the Intune Management Extension as a managed installer on devices (optional)

As an optional clean-up step, you can run a script to remove the Intune Management Extension as a managed installer on devices that have already installed it. This step is optional as this configuration has no effect on devices unless you also use App Control for Business policies that reference the managed installer.

1. Download the **CatCleanIMEOnly.ps1** PowerShell script. This script is available at [https://aka.ms/intune_WDAC/CatCleanIMEOnly](https://aka.ms/intune_WDAC/CatCleanIMEOnly) from *download.microsoft.com*.

2. Run this script on devices that have the Intune Management Extension set as a managed installer. This script removes only the Intune Management Extension as a managed installer.

3. Restart the Intune Management Extension service for the above changes to take effect.

To run this script, you can use Intune to run [PowerShell scripts](../apps/powershell-scripts.md), or other methods of your choice.

#### Remove all AppLocker policies from a device (optional)

To remove *all* Windows AppLocker policies from a device, you can use the **CatCleanAll.ps1** PowerShell script. This script removes not only the Intune Management Extension as a managed installer, but *all* policies based on Windows AppLocker from a device. Before using this script, be sure you understand your organizations use of AppLocker policies.

1. Download the **CatCleanAll.ps1** PowerShell script. This script is available at [https://aka.ms/intune_WDAC/CatCleanAll]( https://aka.ms/intune_WDAC/CatCleanAll) from *download.microsoft.com*.

2. Run this script on devices that have the Intune Management Extension set as a managed installer. This script removes the Intune Management Extension as a managed installer and AppLocker policies from the device.

3. Restart the Intune Management Extension service for the above changes to take effect.

To run this script, you can use Intune to run [PowerShell scripts](../apps/powershell-scripts.md), or other methods of your choice.

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

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **App Control for Business** > select the **App Control for Business** tab > and then select **Create Policy**. App Control for Business policies are automatically assigned a platform type.

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

2. After your App Control for Business supplemental policy is created in XML format, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **App Control for Business** > select the **App Control for Business** tab, and then select **Create Policy**.

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

- For Intune EDU tenants, the Intune Management Extension is automatically set as a managed installer. This configuration is automatic and can't be changed.

## Delete App Control for Business policy

As detailed in [Deploy WDAC policies using Mobile Device Management (MDM) - Windows security](/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-intune) in the Windows Security documentation, policies deleted from the Intune UI are removed from the system, and from devices, but stay in effect until the next reboot of the machine.

**To disable or delete WDAC enforcement**:

1. Replace the existing policy with a new version of the policy that will **`Allow /*`**, like the rules in the example policy found on Windows devices at `%windir%\schemas\CodeIntegrity\ExamplePolicies\AllowAll.xml`

   This configuration removes any blocks that might otherwise be left in place on a device after the policy is removed.

2. After the updated policy is deployed, you can then delete the new policy from the Intune portal.

This sequence prevents anything from being blocked and fully removes the WDAC policy on the next reboot.

> [!WARNING]
> Before unenrolling a device from Intune that received App Control for Business policies, or removing app control policies from that device, see [Remove App Control policies causing boot stop failures](/windows/security/application-security/application-control/app-control-for-business/deployment/disable-appcontrol-policies#remove-app-control-policies-causing-boot-stop-failures) in the Windows Security article **Remove App Control for Business policies**. This article provides important steps to follow to prevent potential boot stop failures.

## Monitor App Control for Business policies and the managed installer

After devices are assigned App Control for Business and Managed installer policies, you can view policy details within the admin center.

- To view reports, your account must have the *Read* permission for the Intune role-based access control category of **Organization**.

To view reports, sign in to the Intune admin center and go to **Endpoint security** > **App Control for Business**. Select the **Policies** tab for *App Control for Business* policies, and **Managed installer** for managed installer policies:

### App Control for Business

On the **App Control for Business** tab, select a policy to open a view with the following report options:

- **Device and user check-in status** - A simple chart that displays the count of devices reporting each available status for this policy.

- **View Report** - This opens a view with a list of the devices that received this policy. Here you can select devices to drill in and view their App Control for Business policy settings format.

The policy view also includes the following report tiles:

- **Device assignment status** - This report shows all the devices that are targeted by the policy, including devices in a pending policy assignment state.

  With this report, you can select the *Assignment status* values you want to view, and then select **Generate report** to refresh the report view individual devices that received the policy, their last active user, and the assignment status.

  You can also select devices to drill in and view their App Control for Business policy settings format.

- **Per setting status** - This report displays a count of devices that report status as *Success*, *Error*, or *Conflict* for the settings from this policy.

### Managed installer

On the **Managed Installer** tab, select a policy to open its Overview page, where you can view the following information:

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

## Frequently asked Questions

### When should I set the Intune Management Extension as the managed installer?

We recommend configuring the Intune Management Extension as the managed installer at your next available opportunity.

Once set, subsequent apps you deploy to devices are appropriately tagged to support WDAC policies that *Trust apps from managed installers*.

In environments where apps deployed before a managed installer was configured, we recommend you deploy new WDAC policies in *audit-mode* so you can identify the apps were deployed but not tagged as trusted. You can then review the audit results and determine which apps should be trusted. For apps you'll trust and allow to run, you can then create custom WDAC policies to allow those apps.

It can be helpful to explore [Advanced Hunting, which is a feature in Microsoft Defender for Endpoint](/windows/security/threat-protection/windows-defender-application-control/querying-application-control-events-centrally-using-advanced-hunting) that makes it easier to query audit events across the many machines that IT admins manage and help them craft policies.

### What do I do with the old Application Control policy from my Attack surface reduction policy

You might notice instances of the Application Control policy in the Intune UI under **Endpoint Security** > **Attack Surface Reduction** or under **Devices** > **Manage devices** > **Configuration**. These will be deprecated in a future release.

### What if I have multiple base or supplemental policies on the same device?

Prior to Windows 10 1903, App Control for Business only supported a single active policy on a system at any given time. That behavior significantly limits customers in situations where multiple policies with different intents would be useful. Today, multiple base and supplemental policies are supported on the same device. Learn more about [deploying multiple App Control for Business policies](/windows/security/application-security/application-control/windows-defender-application-control/design/deploy-multiple-wdac-policies).

On a related note, there's no longer a limitation of 32 policies active on the same device for App Control for Business. This issue is resolved for devices that run Windows 10 1903 or later with a Windows security update released on or after March 12, 2024. Older versions of Windows are expected to receive this fix in future Windows security updates.

### Does the Managed Installer opt-in capability for my tenant set apps installed from Configuration Manager with the appropriate tag?

No. This release focuses on setting apps installed from Intune, using the Intune Management Extension, as the managed installer. It can't set Configuration Manager as the managed installer.

If setting Configuration Manager as the managed installer is desired, you can allow that behavior from within Configuration Manager. If you already have Configuration Manager set as the managed installer, the expected behavior is that the new Intune Management Extension AppLocker policy merges with the existing Configuration Manager policy.

### What considerations should I have for Microsoft Entra Hybrid Join (HAADJ) devices within my organization that want to use Managed Installer?

Microsoft Entra hybrid-join devices require connectivity to an on-premises Domain Controller (DC) to apply Group Policies including the managed installer policy (through AppLocker). Without DC connectivity, especially during Windows Autopilot provisioning, managed installer policy won't successfully apply. Consider:

1. Use Windows Autopilot with Microsoft Entra join instead. See our recommendation for [which Microsoft Entra join option](../../solutions/cloud-native-endpoints/azure-ad-joined-hybrid-azure-ad-joined.md#which-option-is-right-for-your-organization) to choose for more information.

2. For Microsoft Entra hybrid-join, choose one or both of the following:
   - Use device provisioning methods that provide DC connectivity at the time of app install as Windows Autopilot might not work here.
   - Deploy apps after the Windows Autopilot provisioning is complete, so that DC connectivity is established at the time of app install and managed installer policy can apply.

## Next Steps

[Configure Endpoint security policies](endpoint-security-policy.md#create-an-endpoint-security-policy)
