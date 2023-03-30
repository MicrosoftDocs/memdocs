---
title: How to enroll with Autopilot
titleSuffix: Configuration Manager
description: Enable clients to enroll with co-management when they provision with Windows Autopilot.
ms.date: 05/18/2022
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: how-to
ms.localizationpriority: medium
author: gowdhamankarthikeyan
ms.author: gokarthi
ms.reviewer: mstewart,aaroncz 
manager: apoorvseth
ms.collection: tier3
---

# How to enroll with Autopilot

<!-- Intune 11300628 -->

When you use [Windows Autopilot](../../autopilot/windows-autopilot.md) to provision a device, it first enrolls to Azure Active Directory (Azure AD) and Microsoft Intune. If the intended end-state of the device is co-management, previously this experience was difficult because of installation of Configuration Manager client as Win32 app which introduces component timing and policy delays.

Now you can configure co-management settings in Intune, which happens during the Autopilot process. This behavior directs the workload authority in an orchestrated manner between Configuration Manager and Intune.

You no longer need to create and assign an Intune app to install the Configuration Manager client. The Intune co-management settings policy automatically installs the Configuration Manager client as a first-party app. The device gets the client content from the Configuration Manager cloud management gateway (CMG), so you don't need to provide and manage the client content in Intune. You do still specify the command-line parameters. This parameter can optionally include the [PROVISIONTS](../core/clients/deploy/about-client-installation-properties.md#provisionts) property to specify a task sequence.

If the device is targeted with an [Autopilot enrollment status page (ESP) policy](../../intune/enrollment/windows-enrollment-status.md), the device waits for Configuration Manager client to be installed. The Configuration Manager client installs, registers with the site, and applies the production co-management policy. Then the Autopilot ESP continues.

## Scenarios

The following scenarios are several common ones that this feature supports:

- Use the Microsoft Intune family of products to configure devices to your organizational standards. You want to combine modern provisioning with Autopilot, cloud-attached management with co-management, and existing investments in Configuration Manager task sequences and app deployments.

- Install apps in a specific sequence during the Autopilot enrollment status page process.

- Override the co-management policy and use Intune for all workloads. You want devices to get all policies from Intune, but still have the Configuration Manager client for emergency use.

## Process

When you use this policy, the following actions happen on the device during Autopilot provisioning:

1. When the device enrolls into Intune, the service checks if the device is assigned a co-management settings policy.

1. During the **Device preparation** phase of the enrollment status page, the service configures the following information on the device:

    - It provides an enrollment status page policy, which configures Configuration Manager as a policy provider.

    - It sets the management authority on the device based on the co-management settings policy:

        - Intune: The process continues with those policies.

        - Configuration Manager: The service doesn't apply Intune policies. It waits for policy from Configuration Manager to determine the workload configuration.

    - If co-management settings policy is set to automatically install Configuration Manager client, then the device downloads the CCMSetup.msi bootstrap file from the Intune service, which it runs with the specified command-line parameters. These parameters specify the location of the CMG, which it uses to download the client installation content. This content is the site's production client version hosted on the CMG.

        > [!NOTE]
        > This step can take time depending on the network and device performance, while it downloads the content and installs. The enrollment status page will stay on the step for **Preparing your device for mobile management**. For more information, see the [Troubleshooting](#troubleshoot) section.

    - Once it successfully installs, the client's normal behavior begins. It communicates through the CMG, registers with the site, and then requests policy.

1. During the **Device setup** phase of the enrollment status page:

    - If the client installation command line includes the **PROVISIONTS** parameter, the client runs that task sequence.

    - The enrollment status page tracks the task sequence in the **Apps** category.

    - If necessary, the task sequence can restart the device and return to the enrollment status page afterwards.

    - Once the task sequence successfully completes, the Autopilot provisioning process continues on the enrollment status page.

        :::image type="content" source="media/esp-device-setup-complete.png" alt-text="Enrollment status page, Device Setup complete.":::

> [!NOTE]
> There's no integration during the **Account setup** phase of the enrollment status page.

## Requirements

The following components are required to support Autopilot into co-management:

- Windows devices running one of the following versions:

  - Windows 11

> [!NOTE]
  > For Windows 11 devices, if the device has no targeted co-management settings policy, the management authority is set to Intune, during the Autopilot process. Installing Configuration Manager client as Win32 app does not change the respective workload authority as per the co-management workload configuration. To mitigate this, you must create a co-management settings policy and set both the options to **No**

  - At least Windows 10, version 20H2, with the latest cumulative update

- Register the device for Autopilot. For more information, see [Windows Autopilot registration overview](../../autopilot/registration-overview.md).

  - Azure AD-joined only

  - User-driven scenario only

- A device group in Intune to which you'll assign the co-management settings policy. For more information, see [Add groups to organize users and devices](../../intune/fundamentals/groups-add.md).

  You also need to assign the following profiles to the same device group:

  - [Enrollment status page profile](../../intune/enrollment/windows-enrollment-status.md), with the option to **Show app and profile configuration progress**

  - [Windows Autopilot deployment profile](../../autopilot/profiles.md)

- Configuration Manager version 2111 or later, and the following features:

  - Set up a cloud management gateway (CMG). For more information, see [CMG overview](../core/clients/manage/cmg/overview.md).

  - Enable co-management. For more information, see [How to enable co-management](how-to-enable.md).

## Recommendations

Use these recommendations for a more successful deployment:

- When you run a task sequence after client installation, don't include many application installations. Many apps can delay the process, and risk timeout for the enrollment status page. For a better user experience, only include critical apps that are needed immediately. Install other apps through separate deployments or user self-service.

    > [!NOTE]
    > The default timeout for the enrollment status page is 60 minutes. You can adjust this value in that policy, if needed, but a faster process may provide a better user experience.

- Don't use this process with other policy providers like the [Intune management extension](../../intune/apps/intune-management-extension.md), which can cause conflicts. Each provider isn't currently aware of others. Either use the co-management policy for the Configuration Manager provider, or use the Intune management extension provider, not both.

  - If you need to install apps in a specific order, use the co-management policy. Run a task sequence to install the apps.

  - If the installation order of apps doesn't matter to you, you can use either provider.

## Limitations

Autopilot into co-management currently doesn't support the following functionality:

- Hybrid Azure AD-joined devices

> [!NOTE]
  > For Windows 11 devices, if the device has no targeted co-management settings policy, the management authority is set to Intune, during the Autopilot process. Installing Configuration Manager client as Win32 app does not change the respective workload authority as per the co-management workload configuration. To mitigate this, you must create a co-management settings policy and set both the options to **No**

- Autopilot pre-provisioning, also known as _white glove_ provisioning

- Workloads switched to **Pilot Intune** with pilot collections. This functionality is dependent upon collection evaluation, which doesn't happen until after the client is installed and registered. Since the client won't get the correct policy until later in the Autopilot process, it can cause indeterminate behaviors.

- Clients that authenticate with PKI certificates. You can't provision the certificate on the device before the Configuration Manager client installs and needs to authenticate to the CMG. Azure AD is recommended for client authentication. For more information, see [Plan for CMG client authentication: Azure AD](../core/clients/manage/cmg/plan-client-authentication.md#azure-ad).

## Configure

Use the following process to configure the co-management policy in Intune:

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Select the **Devices** menu, select **Enroll devices**, and then select **Windows enrollment**.

1. Select **Co-management settings**, and then select **Create**.

1. On the **Basics** page, specify a **Name** for the policy, and an optional description.

1. On the **Settings** page, select **Yes** to automatically install the Configuration Manager client.

1. Specify the client installation command-line parameters. You can copy these parameters from the **Enablement** tab of the cloud attach properties in the Configuration Manager console. For more information and specific command-line parameters, see [Get the command line from Configuration Manager](how-to-prepare-Win10.md#get-the-command-line-from-configuration-manager).

    :::image type="content" source="media/intune-comanage-settings.png" alt-text="Co-management settings in Microsoft Intune.":::

1. On the **Assignments** page, select a target _device_ group. For more information, see [Assign user and device profiles in Microsoft Intune](../../intune/configuration/device-profile-assign.md).

1. On the **Review + create** page, review the settings and create the policy.

> [!NOTE]
> If you assign more than one policy to a device, Intune pre-computes which policy it serves to the device. The **Co-management authority** pane in the Microsoft Intune admin center lists the policy settings. Set the priority of each setting to help determine which policy a device receives when you assign more than one.

### Advanced settings

By default, the device waits for and uses the workload assignments from the Configuration Manager co-management policy. In the **Advanced** area of this policy, you can select **Yes** to override the co-management policy and use Intune for all workloads. Use this option for devices that are primarily cloud-managed with Intune policies, but you need the Configuration Manager client for certain apps. Even when Intune is the authority for the **Client apps** workload, a co-managed device can still get apps from Configuration Manager. For more information, see [Workloads: Client apps](workloads.md#client-apps) and [Use the Company Portal app on co-managed devices](company-portal.md).

> [!WARNING]
> Don't change this setting after device provisioning. It will apply to existing devices in the assigned group, not just new devices running the Autopilot process. Because of policy synchronization timing, the behavior of the policy change is non-deterministic, thus should be avoided.

## Troubleshoot

The first step when you troubleshoot issues with this process is to make sure that you're using Autopilot into co-management in a supported scenario. For more information, see [Requirements](#requirements).

Next, collect logs. Press **Shift** + **F10** during the Autopilot out-of-box experience (OOBE) to open a command prompt. Then run the MDM diagnostics tool, for example: `%windir%\system32\mdmdiagnosticstool.exe -area Autopilot;DeviceEnrollment -cab %temp%\autopilot-logs.cab`

> [!NOTE]
> This tool doesn't collect Configuration Manager CCMSetup and client logs. Manually gather them from the device. By default, these logs are in the following directories:
>
> - `%windir%\ccmsetup\Logs`
> - `%windir\CCM\Logs`

Investigate how the enrollment status page failed while waiting for Configuration Manager. There are two possible situations:

- The **Device preparation** phase fails while waiting on the client to install. For more information, see [The client installation doesn't complete](#the-client-installation-doesnt-complete).

- The **Device setup** phase fails while waiting on the task sequence to complete. For more information, see [The task sequence doesn't complete](#the-task-sequence-doesnt-complete).

> [!TIP]
> For more information on troubleshooting Autopilot, see [Troubleshooting overview](../../autopilot/troubleshooting.md).

### The client installation doesn't complete

The enrollment status page tracks the client installation during the **Device preparation** phase while **Preparing your device for mobile management**. If you see the error code `0x800705b4` during this phase, it timed out while trying to install the client. The enrollment status page default timeout is 60 minutes.

:::image type="content" source="media/device-preparation-error.png" alt-text="Autopilot enrollment status page, Device Preparation error 800705b4.":::

1. In the `autopilot-logs.cab` file from the diagnostic tool, find the **Shell-Core** logs. You may see an entry similar to the following event:

    ```log
    [ETW] [Microsoft-Windows-Shell-Core] [Informational] - CloudExperienceHost Web App Event 2. Name:
    'CommercialOOBE_ESPDevicePreparation_PolicyProvidersInstallation_TimedOut', Value: '{"message":
    "BootstrapStatus: Timed out waiting for all policy providers to provide a list of policies.","errorCode":2147943860}'.
    ```

1. Check the installation state for the client in the Windows Registry. Use the following Windows PowerShell command to query this state:

    ```powershell
    $key = 'HKLM:\SOFTWARE\Microsoft\Windows\Autopilot\EnrollmentStatusTracking\Device\DevicePreparation\PolicyProviders\ConfigMgr'
    Get-ItemPropertyValue -Path $key -Name InstallationState
    ```

    If this registry value is set, it can be one of the following possible values:

    - `1`: Not installed
    - `2`: Not required
    - `3`: Complete
    - `4`: Error

1. If the installation state isn't complete (`3`), investigate further depending upon the installation state:

    - The default value of the installation state for a registered policy provider is `1`. This state means that the CCMSetup.msi bootstrap installer didn't download from the service or it didn't start installing.

    - If the installation state is `4`, review the client logs to determine why CCMSetup failed.

1. Make sure the device is receiving CCMSetup.msi from Intune and the full client installation content from the CMG.

1. Look in `%windir%\ccmsetup` for the installation and log files.

1. Examine `%windir%\ccmsetup\Logs\ccmsetup.log` for possible failures.

### The task sequence doesn't complete

The enrollment status page tracks the task sequence as an app during the **Device setup** phase. If the task sequence doesn't complete successfully, the **Device setup** section shows an error for **Apps**.

:::image type="content" source="media/device-setup-error.png" alt-text="Autopilot enrollment status page, Device Setup error for Apps.":::

1. In the `autopilot-logs.cab` file from the diagnostic tool, find the **Shell-Core** logs. You may see an entry similar to the following event:

    ```log
    [ETW] [Microsoft-Windows-Shell-Core] [Informational] - CloudExperienceHost Web App Event 2. Name:
    'CommercialOOBE_BootstrapStatusCategory_SubcategoryProcessing_Failed', Value: '{"message":
    "BootstrapStatus: Subcategory ID = DeviceSetup.AppsSubcategory; state = failed.","errorCode":0}'.
    ```

1. Get the task sequence log. By default, this log file is at the following path: `%windir%\CCM\Logs\SMSTS\smsts.log`

1. Check the installation state for the task sequence in the Windows Registry. Use the following Windows PowerShell command to query this state:

    ```powershell
    $key = 'HKLM:\SOFTWARE\Microsoft\Windows\Autopilot\EnrollmentStatusTracking\Device\Setup\Apps\Tracking\ConfigMgr\Provisioning_TS'
    Get-ItemPropertyValue -Path $key -Name InstallationState
    ```

    If this registry value is set, it can be one of the following possible values:

    - `1`: Not installed
    - `2`: In progress
    - `3`: Complete
    - `4`: Error

1. If the installation state isn't complete (`3`), examine the task sequence log for details depending upon the installation state:

    - If the installation state is `1` or `2`, see if the task sequence was still running when the enrollment status page timed out. By default, this timeout is 60 minutes.

      - Look more closely at the steps of the task sequence, if one step took longer than anticipated. Remove long-running steps, or reduce the number of steps in the task sequence.

      - Alternatively, increase the timeout value for the enrollment status page policy.

    - If the installation state is `4`, review the task sequence log to determine why it failed.

## Next steps

[Tutorial: Use Autopilot to enroll Windows devices in Intune](../../intune/enrollment/tutorial-use-autopilot-enroll-devices.md)

[Windows Autopilot user-driven mode](../../autopilot/user-driven.md)
