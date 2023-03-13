---
title: Configure policies to manage Endpoint Privilege Management with Microsoft Intune
description: Configure policies that define how Endpoint Privilege Management functions in your tenant, and behaviors when elevating files to run in administrative context.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mattcall
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
---

# Configure policies for Endpoint Privilege Management

<!-- [!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)] -->
> [!NOTE]  
> This capability is in public preview, and free to try and use. After public preview, it will be available as an Intune add-on. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Endpoint Privilege Management (EPM) is a solution you can integrate with Microsoft Intune. EPM policies empower your organizations non-administrative users to run files that require elevated permissions, and does so with zero or limited disruptions to the user's workflow. Through integration with Microsoft Intune, EPM can help you to secure your organization by removing administrative permissions for most users.

The information in this article can help you to configure the following policies and reusable settings groups for EPM:

- Enable your tenant for Endpoint Privilege Management
- Windows elevation settings policy
- Windows elevation rules policy
- Reusable settings groups, which are optional configurations for your elevation rules.

Applies to:

- Windows 10
- Windows 11

## Enable your tenant for Endpoint Privilege Management

Before you can use EPM to create policies and manage file elevations, you must enable support for EPM in your tenant.

During the public preview, you can use EPM for free. To enable support for your tenant:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management**.

2. Review the available information for EPM, and when ready, select **Activate**. Intune begins to provision EPM for your tenant, which includes making the EPM component available for your devices. These components are enabled on devices when they receive a *Windows elevation settings policy*.

   :::image type="content" source="./media/epm-policy/enable-epm.png" alt-text="Activate EPM for use during the public preview.":::


## Windows elevation settings policy

After you enable Endpoint Privilege Management for your tenant, deploy *Windows elevation settings policy* to users or devices. The policy configures the following on devices:

- Enable Endpoint Privilege Management on a device.
- Set default rules for elevation requests for any file that isn't managed by an Endpoint Privilege Management elevation rule on that device.
- Configure what information EPM reports back to Intune.

A device must have an elevation settings policy that enables support for EPM before the device can process an elevation rules policy or manage elevation requests.

### Create a Windows elevation settings policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows 10 and later**, *Profile* to **Windows elevation settings policy**, and then select **Create**.

   :::image type="content" source="./media/epm-policies/create-epm-policy-1.png" alt-text="Image of the admin center UI for selecting an elevation settings policy.":::

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, configure the following to define default behaviors for elevation requests on a device:

   :::image type="content" source="./media/epm-policies/evaluation-settings-policy.png" alt-text="Image of the evaluation settings configuration page.":::

   - **Endpoint Privilege Management**: Set to **Enabled** (default). When set to Disabled, the device doesn't use Endpoint Privilege Management.
   - **Default elevation response**: Configure how this device manages elevation requests for files that aren't directly managed by a rule:
     - **Not Configured**: No default elevation behavior applies to the device.
     - **Deny all requests**: EPM doesn't facilitate the elevation of files that aren't managed by an elevation rule policy. This doesn't prevent users with administrative permissions from using *Run as administrator* to run unmanaged files.
     - **Require user confirmation**: This applies to elevation requests for files that aren't managed by an elevation rule policy. The user receives a simple prompt to confirm their intent to run the file. You can also require additional prompts that are available from the *Validation* drop down:
       - **Business justification**: Require the user to enter a justification for running the file. There's no required format for this justification. User input is saved and can be reviewed through logs if the *Reporting scope* includes collection of endpoint elevations.
       - **Windows authentication**: This option requires the user to authenticate using their organization credentials.

   - **Send data to Microsoft**: By default, this is set to **Yes**. When set to yes, you can then configure a *Reporting scope*. When set to **No**, a device doesn’t report diagnostic data or information about file elevations to Intune.
   - **Reporting scope**: Choose what type of information a device reports to Intune:
     - **Diagnostic data and all endpoint elevations** (Default): The device reports diagnostic data and details about all file elevations that are facilitated by EPM.

       This level of information can help you identify additional files that aren't yet managed by an elevation rule that users seek to run in an elevated context.

     - **Diagnostic data and managed elevations only**: The device reports diagnostic data and details about file elevations for only those files that are managed by an elevation rule policy. File requests for unmanaged files, and files that are elevated through the Windows default action of *Run as administrator*, aren't reported as managed elevations.
     - **Diagnostic data only**: Only diagnostic data for the operation of Endpoint Privilege Management is collected. Information about file elevations isn’t reported to Intune.

   When ready, select **Next** to continue.

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

   Select **Next**.

6. For **Review + create**, review your settings and select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## Windows elevation rules policy

Deploy a *Windows elevation rules policy* to users or devices to deploy one or more rules for files that are managed for elevation by Endpoint Privilege Management. Each rule you add to this policy:

- Identifies a file for which yo want to manage elevation requests.
- Can include a certificate to help validate that file’s integrity before it’s run. You can also add a reusable group that contains a certificate that you then use with one or more rules or policies.
- Specifies if the elevation type of the file as automatic (silently) or requiring user confirmation. With user confirmation, you can add additional user actions that must be completed before the file is run.
In addition to this policy, a device must also be assigned a Windows elevation settings policy that enables Endpoint Privilege Management.

### Create a Windows elevation rules policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows 10 and later**, *Profile* to **Windows elevation rules policy**, and then select **Create**.

   :::image type="content" source="./media/epm-policies/create-epm-policy-1.png" alt-text="Image of the admin center UI for selecting an elevation rules policy.":::

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, add a rule for each file that this policy manages. When you create a new policy, the policy starts includes a blank rule with an elevation type of *User confirmed* and no rule name. Start by configuring this rule, and later you can select **Add** to add additional rules to this policy. Each new rule you add has an elevation type of User confirmed, which can be changed when you configure the rule.

   :::image type="content" source="./media/epm-policies/new-elevation-rules-policy.png" alt-text="Image of the admin center UI for selecting an elevation rules policy.":::

   To configure a rule, select **Edit instance** to open its Rule properties page, and then configure the following:

   :::image type="content" source="./media/epm-policies/elevation-rules.png" alt-text="Image of the elevation rules properties." lightbox="./media/epm-policies/elevation-rules.png":::

   - **Rule name**: Like a policy name, enter a descriptive name for the rule. Name your rules so you can easily identify them later.
   - **Description** (Optional): Enter a description for the profile.

   *Elevation conditions* are conditions that define how a file runs, and user validations that must be met before the file this rule applies to can be run.

   - **Elevation type**: By default, this is set to *User confirmed*, which is the elevation type we recommend for most files.

     - **User confirmed**: We recommend this option for most rules. When a file is run, the user receives a simple prompt to confirm their intent to run the file. The rule can also include additional prompts that are available from the *Validation* drop down:
       - *Business justification*: Require the user to enter a justification for running the file. There's no required format for this, however the user input is saved and can be reviewed through logs if the *Reporting scope* includes collection of endpoint elevations.
       - *Windows authentication*: This option requires the user to authenticate using their organization credentials.
     - **Automatic**: This elevation type automatically runs the file in question with elevated permissions. This is done invisibly to the user, without prompting for confirmation or requiring justification or authentication by the user. 

       Use this type of elevation for only files you trust. Examples include a common and well-known printer-driver that users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

   *File information* is where you specify the details that identify a file and file instance that this rule applies to.

   - **File name**: Specify the file name and its extension. For example: `notepad.exe`
   - **File path** (Optional): Specify the location of the file in relation to the local device where the file is to be run. If the file can be run from any location or is unknown, you can leave this blank. You can also use a variable.
   - **Signature source**: Choose one of the following options:

     - **Use a certificate file in reusable settings** (Default): This option uses a certificate file that has been added to a reusable settings group for Endpoint Privilege Management. You must [create a reusable settings group](#reusable-settings-groups) before you can use this option.

        To identify the *Certificate*, select *Add or remove a certificate*, and then select the reusable group that contains the correct certificate. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.

     - **Upload a certificate file**: Add a certificate file directly to the elevation rule. For *File upload*, specify a **.cer** file that can validate the integrity of the file that this rule applies to. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.
     - **Not configured**: Use this option when you can't use a certificate to validate the integrity of the file. When no certificate is used, you must provide a *file hash*.

   - **File hash**: The file hash is required when Signature source is set to *Not configured*, and optional when set to use a certificate.
   - **Minimum version**: (Optional) Use the **x.x.x.x** format to specify a minimum version of the file that is supported by this rule.
   - **File description**: (Optional) Provide a description of the file.
   - **Product name**: (Optional) Specify the name of the product that the file is from.
   - **Internal name**: (Optional) Specify the internal name of the file.

   Select **Save** to save the rule configuration. You can then **Add** additional rules, and when you've added all the rules this policy will include, select **Next** to continue.  

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).
   Select **Next**.

6. In **Review + create**, review your settings and select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## Reusable settings groups

Endpoint Privilege Management uses reusable settings groups to manage the certificates that validate the files you manage with Endpoint Privilege Management elevation rules. Like all reusable settings groups for Intune, changes to a reusable group are automatically passed to the policies that reference the group. For Endpoint Privilege Management, this means if you must update the certificate you use for file validation, you would only need to update it in the reusable settings group a single time to have that updated certificate applied to all your elevation rules that use that group.

To create the reusable settings group for Endpoint Privilege Management:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Reusable settings (preview)** tab > and then select **Add**.

   :::image type="content" source="./media/epm-policies/add-reusable-settings.png" alt-text="Screen capture of the UI to add a reusable settings group.":::

2. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the reusable group. Name groups so you can easily identify each later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. In **Configuration settings**, select the folder icon for *Certificate file*, and browse to a **.CER** file to add it to this reusable group. The *Base 64 value* field fills in based on the certificate selected.

   :::image type="content" source="./media/epm-policies/add-a-certificate.png" alt-text="{alt-text}":::

4. In **Review + create**, review your settings and select **Add**. When you select *Add*, your configuration is saved, and group is then shown in the reusable settings group list for Endpoint Privilege Management.

## Next steps

[Use reports for Endpoint Privilege Management](../protect/epm-reports.md)