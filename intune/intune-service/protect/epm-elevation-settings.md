---
title: Managing Endpoint Settings Poilices for Endpoint Privilege Management
description: View guidance on how to manage the Endpoint Privilege Management client, including reporting level and default elevation response. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/30/2025
ms.topic: article
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Creating elevation settings with Endpoint Privilege Management

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

To configure the following options on devices, deploy *Windows elevation settings policy* to users or devices:

- Enable Endpoint Privilege Management on a device.
- Set default rules for elevation requests for any file that's not managed by an Endpoint Privilege Management elevation rule on that device.
- Configure what information EPM reports back to Intune.

A device must have an elevation settings policy that enables support for EPM before the device can process an elevation rules policy or manage elevation requests. When support is enabled, the `C:\Program Files\Microsoft EPM Agent` folder is added to the device along with the EPM Microsoft Agent, which is responsible for processing the EPM policies.

## About Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device provisions the components that collect usage data on elevation requests and that enforce elevation rules.

  If a device has EPM disabled, the client components immediately disable. There's a delay of seven days before the EPM component is completely removed. The delay helps to reduce the time it takes to restore EPM should a device accidentally have EPM disabled or its elevation settings policy unassigned.

- **Default elevation response** - Set a default response for an *elevation request* of any file that isn't managed by a *Windows elevation rule policy*. For this setting to have an effect, no rule can exist for the application **AND** an end user must *explicitly request* elevation through the *Run with elevated access* right-click menu. By default, this option is set to *Not Configured*. If not setting is configured, the EPM components fall back to their built-in default, which is to **deny all requests**.

  Options include:

  - **Deny all requests** - This option blocks the *elevate request* action for files that aren't defined in a *Windows elevation rules policy*.
  - **Require user confirmation** - When user confirmation is required, you can choose from the same validation options as found for Windows elevation rules policy.

    - **Validation options** - Set validation options when the default elevation response is defined as *Require user confirmation*. Options include:
      - **Business justification** - This option requires the end user to provide a justification before completing an elevation that is facilitated by the default elevation response.
      - **Windows authentication** - This option requires the end user to authenticate before completing an elevation that is facilitated by the default elevation response.

     >[!NOTE]
     > Multiple validation options can be selected to satisfy the needs of the organization. If no options are selected, then the user is only required to select *continue* to complete the elevation.

  - **Require support approval** - When support approval is required, an administrator must approve elevation requests without a matching rule prior to the elevation being required.

  > [!TIP]  
  > We [recommend use of *Support Approved*](../protect/epm-plan.md#security-recommendations) as a default elevation response.

  > [!NOTE]  
  > Default responses are only processed for requests coming through the *Run with elevated access* right-click menu.

- **Send elevation data for reporting** - This setting controls whether your device shares diagnostic and usage data with Microsoft. When enabled to share data, the type of data is configured by the *Reporting scope* setting.

  Diagnostic data is used by Microsoft to measure the health of the EPM client components. Usage data is used to show you elevations that happen within your tenant. For more information about the types of data and how it's stored, see [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md).

  Options include:

  - **Yes** - This option sends data to Microsoft based on the *Reporting Scope* setting.
  - **No** - This option doesn't send data to Microsoft.

- **Reporting Scope** - This setting controls the amount of data being sent to Microsoft when *Send elevation data for reporting* is set to *Yes*. By default, *Diagnostic data and all endpoint elevations are selected.

  Options include:

  - **Diagnostic data and managed elevations only** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about elevations being facilitated by Endpoint Privilege Management.
  - **Diagnostic data and all endpoint elevations** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about *all* elevations happening on the endpoint.
  - **Diagnostic data only** - This option sends only the diagnostic data to Microsoft about the health of the client components.

## Create a Windows elevation settings policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows**, *Profile* to **Windows elevation settings policy**, and then select **Create**.

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, configure the following to define default behaviors for elevation requests on a device:

   :::image type="content" source="./media/epm-policies/evaluation-settings-policy.png" alt-text="Image of the evaluation settings configuration page." lightbox="./media/epm-policies/evaluation-settings-policy.png":::

   - **Endpoint Privilege Management**: Set to **Enabled** (default). When Enabled, a device uses Endpoint Privilege Management. When set to Disabled, the device doesn't use Endpoint Privilege Management, and immediately disables EPM if it was previously enabled. After seven days, the device will deprovision the components for Endpoint Privilege Management.
   - **Default elevation response**: Configure how this device manages elevation requests for files that aren't directly managed by a rule:
     - **Not Configured**: This option functions the same as *Deny all requests*.
     - **Deny all requests**: EPM doesn't facilitate the elevation of files and the user is shown a pop-up window with information about the denial. This configuration doesn't prevent users with administrative permissions from using *Run as administrator* to run unmanaged files.
     - **Require support approval**: This behavior instructs EPM to prompt the user to submit a support approved request.
     - **Require user confirmation**: The user receives a simple prompt to confirm their intent to run the file. You can also require more prompts that are available from the *Validation* drop down:
       - **Business justification**: Require the user to enter a justification for running the file. There's no required format for this justification. User input is saved and can be reviewed through logs if the *Reporting scope* includes collection of endpoint elevations.
       - **Windows authentication**: This option requires the user to authenticate using their organization credentials.

   - **Send elevation data for reporting**: By default, this behavior is set to **Yes**. When set to yes, you can then configure a *Reporting scope*. When set to **No**, a device doesn't report diagnostic data or information about file elevations to Intune.
   - **Reporting scope**: Choose what type of information a device reports to Intune:
     - **Diagnostic data and all endpoint elevations** (Default): The device reports diagnostic data and details about all file elevations that EPM facilitates.

       This level of information can help you identify other files that aren't yet managed by an elevation rule that users seek to run in an elevated context.

     - **Diagnostic data and managed elevations only**: The device reports diagnostic data and details about file elevations for only those files that are managed by an elevation rule policy. File requests for unmanaged files, and files that are elevated through the Windows default action of *Run as administrator*, aren't reported as managed elevations.
     - **Diagnostic data only**: Only diagnostic data for the operation of Endpoint Privilege Management is collected. Information about file elevations isn't reported to Intune.

   When ready, select **Next** to continue.

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md). Select **Next**.

6. For **Review + create**, review your settings and then select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## Next Steps

> [!div class="nextstepaction"]
> [Next: Create an elevation rules policy >](epm-elevation-rules.md)
