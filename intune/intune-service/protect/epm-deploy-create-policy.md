---
title: Guidance for creating elevation rules with Endpoint Privilege Management
description: View guidance on how to create strong file elevation rules with Microsoft Intune Endpoint Privilege Management
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

## Windows elevation settings policy

To configure the following options on devices, deploy *Windows elevation settings policy* to users or devices:

- Enable Endpoint Privilege Management on a device.
- Set default rules for elevation requests for any file that's not managed by an Endpoint Privilege Management elevation rule on that device.
- Configure what information EPM reports back to Intune.

A device must have an elevation settings policy that enables support for EPM before the device can process an elevation rules policy or manage elevation requests. When support is enabled, the `C:\Program Files\Microsoft EPM Agent` folder is added to the device along with the EPM Microsoft Agent, which is responsible for processing the EPM policies.

### Create a Windows elevation settings policy

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
> [Next: Create an elevation rules policy >](epm-deploy-create-rules.md)

## Related content

- [Learn about Endpoint Privilege Management](../protect/epm-overview.md)
- [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
