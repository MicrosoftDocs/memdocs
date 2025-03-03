---
title: Remediations
description: Learn about how to use Remediations
ms.date: 06/20/2024
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.topic: how-to
author: smritib17
ms.author: smbhardwaj
manager: dougeby
# Customer intent: As a Microsoft Intune administrator, I want to enable and use remediations so that I can fix common support issues before end-users notice issues.
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jon callahan
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- highpri
- M365-identity-device-management
---

# Remediations

> [!IMPORTANT]
> **Proactive Remediations** is renamed to **Remediations** and is now available from **Devices** > **Manage devices** > **Scripts and remediations**. All references to Proactive Remediations in this documentation are replaced with **Remediations**. However, the term Proactive Remediations might still appear in some blogs and other articles.

Remediations helps you fix common support issues before end-users notice issues.

In this article, you learn how to:  

> [!div class="checklist"]
>
> * Review prerequisites for Remediations
> * Deploy a built-in script package
> * Deploy a custom script package
> * Run a Remediation script on-demand (preview)
> * Client policy retrieval and client reporting
> * Monitor the script packages
> * Export script output
> * Monitor remediation status for a device  

## About Remediations

Remediations are script packages that can detect and fix common support issues on a user's device before they even realize there's a problem. Remediations can help reduce support calls. You can create your own script package, or deploy one of the script packages we've written and used in our environment for reducing support tickets.

Each script package consists of a detection script, a remediation script, and metadata. Through Intune, you can deploy these script packages and see reports on their effectiveness.

## Prerequisites

Whether enrolling devices via Intune or Configuration Manager, Remediation scripting has the following requirements:

- Devices must be Microsoft Entra joined or Microsoft Entra hybrid joined and meet one of the following conditions:

  - Is managed by Intune and runs an Enterprise, Professional, or Education edition of Windows 10 or later.
  - A [co-managed](../../configmgr/comanage/overview.md) device running Windows 10, version 1903 or later. Co-managed devices on preceding versions of Windows 10 will need the [Client apps workload](../../configmgr/comanage/workloads.md#client-apps) pointed to Intune (only applicable up to version 1607).

### Licensing

Remediations requires users of the devices to have one of the following licenses:

- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)

- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)

- Windows 10/11 Virtual Desktop Access (VDA) per user

### Permissions

- For Remediations, the user needs permissions appropriate to their role under the **Device configurations** category. For more information, see [Role-based access control for Microsoft Intune](role-based-access-control.md).

- An [Intune Service Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-service-administrator-permissions) is required to confirm licensing requirements before using Remediations for the first time.

### Script requirements

- You can have up to 200 script packages.
- A script package can contain a detection script only or both a detection script and a remediation script. 
  - A remediation script only runs if the detection script uses exit code `exit 1`, meaning the issue was detected.
- Ensure the scripts are encoded in UTF-8.
  - If the option **Enforce script signature check** is enabled in the [Settings](#deploy-built-in-script-packages) page of creating a script package, then make sure that the scripts are encoded in UTF-8 not UTF-8 BOM.
- The maximum allowed output size limit is 2048 characters.
- If the option **Enforce script signature check** is enabled in the [Settings](#deploy-built-in-script-packages) page of creating a script package, the script runs using the device's PowerShell execution policy. The default execution policy for Windows client computers is **Restricted**. The default execution for Windows Server devices is **RemoteSigned**. For more information, see [PowerShell execution policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies#powershell-execution-policies).
  - Scripts built into Remediations are signed and the certificate is added to the **Trusted Publishers** certificate store of the device.
  - When using third-party scripts that are signed, make sure the certificate is in the **Trusted Publishers** certificate store. As with any certificate, the certificate authority must be trusted by the device.
  - Scripts without **Enforce script signature check** use the **Bypass** execution policy.
- Don't put reboot commands in detection or remediations scripts. <!--13957089-->
- Do not include any type of sensitive information in scripts (such as passwords)
- Do not include Personally Identifiable Information (PII) in scripts
- Do not use scripts to collect PII from devices
- Always follow privacy best practices

## Deploy built-in script packages

There are built-in script packages you can use to get started with Remediations. The **Microsoft Intune Management Extension** service gets the scripts from Intune and runs them. The following built-in script packages just need to be assigned:

- **Update stale Group Policies** – Stale Group Policies can lead to helpdesk tickets related to connectivity and internal resource access.
- **Restart Office Click-to-run service** – When the Click-to-run service is stopped, Office apps fail to start leading to helpdesk calls.

To assign the script package:

1. From the **Devices** > **Manage devices** > **Scripts and remediations** node, select one of the built-in script packages.
1. Select **Properties**, then next the **Assignments** heading, select **Edit**.
1. Choose the groups you want to **Assign to** and any **Excluded groups** for the script package.
1. To change the **Scope tags**, select **Edit** then **Select scope tags**.
1. If you would like to change the schedule, select the ellipses and choose **Edit** to specify your settings then **Apply** to save them.
1. When you're done, select **Review + save**.  

## Create and deploy custom script packages

The **Microsoft Intune Management Extension** service gets the scripts from Intune and runs them. The scripts are rerun every 24 hours. You can copy the provided scripts and deploy them, or you can create your own script packages. To deploy script packages, follow the instructions in the next section.

### Copy the provided detection and remediation scripts

1. Copy the scripts from the [PowerShell scripts](powershell-scripts-remediation.md#powershell-scripts-for-remediations) article.
   - Script files whose names start with `Detect` are detection scripts. Remediation scripts start with `Remediate`.
   - For a description of the scripts, see the [Script descriptions](powershell-scripts-remediation.md#script-descriptions).
1. Save each script using the provided name. The name is also in the comments at the top of each script. Ensure the saved scripts are encoded in UTF-8.
   - You can use a different script name, but it won't match the name listed in the [Script descriptions](powershell-scripts-remediation.md#script-descriptions).

### Deploy the script packages

Remediation scripts need to be encoded in UTF-8. Uploading these scripts rather than editing them directly in your browser helps ensure that the script encoding is correct so your devices can execute them.

1. In the Intune admin center, go to **Devices** > **Manage devices** > **Scripts and remediations**.
1. Choose **Create script package** button to create a script package.
     [![Remediations page. Select the create link.](media/remediations/remediations-create.png)](media/remediations/remediations-create.png#lightbox)
1. In the **Basics** step, give the script package a **Name** and optionally, a **Description**. The **Publisher** field can be edited, but defaults to your name. **Version** can't be edited.
1. On the **Settings** step, upload both the **Detection script file** and the **Remediation script file** by doing the following steps:
   1. Select the folder icon.
   1. Browse to the `.ps1` file.
   1. Choose the file and select **Open** to upload it.

    The detection script must use exit code `exit 1` if the target issue is detected. If there's any other exit code, the remediation script won't run. Including an empty output, since it results in an *issue is not found* state. Review the [Sample detection script](powershell-scripts-remediation.md#script-descriptions) for an example of exit code usage.

   You need the corresponding detection and remediation script to be in the same package. For example, the `Detect_Expired_User_Certificates.ps1` detection script corresponds with the `Remediate_Expired_User_Certificates.ps1` remediation script.
       [![Remediations script settings page.](media/remediations/remediations-script-settings.png)](media/remediations/remediations-script-settings.png#lightbox)
1. Finish the options on the **Settings** page with the following recommended configurations:
   - **Run this script using the logged-on credentials**: This setting is dependent on the script. For more information, see the [Script descriptions](powershell-scripts-remediation.md#script-descriptions).
   - **Enforce script signature check**: No
   - **Run script in 64-bit PowerShell**: No

   For information about enforcing script signature checks, see [Script requirements](#script-requirements).
1. Select **Next** then assign any **Scope tags** you need.
1. In the **Assignments** step, select the device groups to which you want to deploy the script package. When you're ready to deploy the packages to your users or devices, you can also use filters. For more information, see [Create filters in Microsoft Intune](filters.md).
 
   >[!NOTE]
   > Don't mix user and device groups across include and exclude assignments.

1. Complete the **Review + Create** step for your deployment.

## Run a remediation script on-demand (preview)

You can use the **Run remediation** device action to run a remediation script on-demand to a single Windows device.

### Prerequisites for running a remediation script on-demand

- Remediations must already be configured before a remediation script can be used on-demand.

- The built-in or custom script packages must be available for users to run a remediation on-demand, however they don't need to be assigned to a user or device. You can use **Scope tags** to limit which remediation script packages a user can see.

- Users must be Global Admins, Intune Admins, or have a role with the **Run remediation** permission (available under  **Remote tasks**). During the public preview, the user must also have Organization: Read.

- Devices are online and able to communicate with Intune and [Windows Push Notification Service (WNS)](intune-endpoints.md#windows-push-notification-services-wns-dependencies) during the remote action.

- The [Intune Management Extension](../apps/intune-management-extension.md) must be installed on devices. The installation is done automatically when a Win32 app, PowerShell script, or Remediation is assigned to a user or device.

### How to run a Remediation script on-demand

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to **Devices** > **By platform** > **Windows** > select a supported device.
3. On the device's  **Overview**  page, select  **…** > **Run remediation (preview).**
4. In the **Run remediation (preview)** pane, select the **Script package** you want to run from the list. Select **View details** to see properties of the script package like detection and remediation script contents, description, and configured settings.
5. To run the remediation on-demand, select **Run remediation**.

> [!NOTE]
> Only a single **Run remediation** device action can be issued at a time for the same device. If you run multiple **Run remediation** device actions in a short period of time to a device, they may overwrite each other.
> [!NOTE]
> The device might not receive the **Run remediation** device action if it is not online or able to successfully communicate with Intune or Windows Push Notification Service (WNS) when the device action is sent.

## Client policy retrieval and client reporting

The client retrieves policy for Remediation scripts at the following times:

- After a restart of the device or Intune management extension service

- After a user signs into the client

- Once every 8 hours

  - The 8 hour script retrieval schedule is fixed based on when the Intune management extension service starts. User sign ins do not alter the schedule.

The client reports Remediation information at the following times:

- When a script is set to run once, the results are reported after the script runs.

- Recurring scripts follow a seven day reporting cycle:

  - Within the first six days, the client reports only if a change occurs. The first time the script runs would be considered a change.

  - Every seven days the client sends a report even if there wasn't a change.

## Monitor your script packages

1. In the Intune admin center, go to **Devices** > **Manage devices** > **Scripts and remediations**, you can see an overview of your detection and remediation status.
       [![Remediations report, overview page.](media/remediations/remediations-report-overview.png)](media/remediations/remediations-report-overview.png#lightbox)

1. Select **Device status** to get status details for each device in your deployment.
       [![Remediations device status.](media/remediations/remediations-device-status.png)](media/remediations/remediations-device-status.png#lightbox)

## Export script output
<!-- 10198545 -->
To help you easily analyze returned outputs, use the **Export** option to save the output as a `.csv` file. Exporting the output to a `.csv` file allows you to analyze the returned outputs when Remediations run on devices with issues. Exporting also allows you to share the results with others for more analysis.  

## Monitor remediation status for a device

You can view the status of Remediations that are assigned or run on-demand to a device.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to **Devices** > **By platform** > **Windows** > select a supported device.
3. Select **Remediations** in the **Monitor** section.

## Next steps

- Get the [PowerShell scripts](powershell-scripts-remediation.md) for Remediations.

- Learn more about [PowerShell script security](../../configmgr/apps/deploy-use/learn-script-security.md).
