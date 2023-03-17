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

## Getting started with EPM policies

EPM uses the two policy types that you configure to manage how a file elevation request is handled. Together, the policies set the conditions for managed files and unmanaged files. Managed files are identified by elevation rules while unmanaged files are all other files.

**Elevate requests**:  
After EPM is enabled on a device, each file on the device includes a new right-click option for running files in an elevated context: *Elevate request*. *Elevate request* is in addition to the option *Run as administrator*, which remains available.

To run a file managed by EPM in an elevated context, users need only double-click on the file. They can also choose to use the files *Elevate request* option. Both actions result in EPM evaluating the file, and if conditions are met, launching it in an elevated context.

- If EPM can match the file to a rule for *Automatic* elevation, the file runs as elevated with no further user interaction.
- WHen a file requires *User Confirmation* from either an elevation rule or by the devices elevation settings, the user must respond to the prompts before the file runs as elevated.
- When a file can't be matched to a rule and the evaluation settings policy don't support a fallback option on the device, the file doesn't run as elevated and launches as a standard user.

For users that have administrative rights, EPM doesn't facilitate the elevation request, no matter how it'ss initiated. Instead, the Windows process of *Run as administrator* is used. However, based on the devices reporting scope as configured in the elevations setting policy, EPM can report information to Intune about the files elevation.

**File validation**:  
To ensure that only the correct file and version are elevated, you specify file details and can specify a file hash. You can also use certificates to validate the files you configure for elevation, which we recommend as a best practice.

If you use certificates to validate file integrity, you add a certificate directly to each policy that requires it, or add the certificate to a [reusable settings group](../protect/reusable-settings-groups.md) that you then assign to multiple policies. The use of reusable settings groups for the certificate can make it easier to manage certificate changes. If you need to update a certificate that’s in a reusable group, those changes automatically apply to each policy that includes the reusable group. This is more efficient than making separate edits to each policy to update the certificate.

For guidance on how to configure the policies and reusable settings group, see [Configure policies for Endpoint Privilege Management](../protect/epm-policies.md).

### Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:
<!-- To enable Endpoint Privilege Management (EPM) on a device, a *Windows elevation settings policy* must be assigned to it. This policy is necessary for EPM to be enabled, and includes the following uses: -->

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device installs components that monitor elevation requests and enforce elevation rules.

  If a device has EPM disabled, there's a delay of seven days before the EPM component is deprovisioned. The delay can reduce the time it takes to restore EPM should a device have accidentally had EPM disabled, or its elevation settings policy unassigned.

- **Set a default response for an *Elevate request*** of any file that’s not managed by a *Windows elevation rule policy*. By default, this option isn't configured.  <!-- Pending details as to what happens here, does the file elevate, or is it blocked? -->
  
  Options include:
  - Deny all requests - This option blocks the *elevate request* action for files that aren't defined in a Windows elevation rules policy.
  - Require user confirmation - When confirmation is required you can choose from the same options as found for Windows elevation rules policy. 
- **Configure what Endpoint Privilege Management reports to Intune**. You can choose to have a device:
  - Not report any data.
  - Report only diagnostic data.
  - Report diagnostic data and details about elevation requests of files that are identified by an elevation rule.
  - Report diagnostic data and details about all elevations, whether or not the file is identified by an elevation rule. This option also reports on elevation requests made by using *Run as administrator*.

### Windows elevation rules policy

Use profiles for *Windows elevation rules policy* to manage the identification of specific files, and how to elevation requests for those files are handled. Each *Windows elevation rule policy* includes one or more *elevation rules*. It's with elevation rules that you configure details about the file being managed and requirements for it to be elevated.

Each elevation rule:

- **Uses the file name and file extension to identify the file the rule applies to.** The rule also supports optional conditions like a minimum build version, product name, or internal name. Optional conditions aren't used by Intune to identify the file, but can help admins identify which actual file the rule applies to.
- **Supports use of a certificate to validate the files integrity before its run on a device.** Certificates can be added directly to a rule, or by using a reusable settings group. We recommend the use of reusable settings groups as they can be more efficient and simplify a future change to the certificate. For more information, see the next section [Reusable settings groups](#reusable-settings-group).
- **Supports use of a file hash to validate the file.** A file hash is required unless you use a certificate, in which case the file hash becomes optional.
- **Configures the files evaluation type.** Evaluation type identifies what happens when an elevation request is made for the file. By default, this option is set to *User confirmed*, which is our recommendation for most managed files.
  - **User confirmed** (Recommended): A user confirmed elevation always requires the user to click on a confirmation prompt to run the file. There are additional user confirmations you can add. One require users to authenticate using their organization credentials. Another option requires the user to enter a business justification. While the text entered for a justification is up to hte user, EPM can collect and report it when the device is configured to report elevation data as part of its Windows elevation settings policy.
  - **Automatic** elevation happens invisibly to the user. There's no prompt, and no indication that the file is running in an elevated context. 

    >[!CAUTION]  
    > We recommend automatic elevation be used sparingly, and only for trusted files that are business critical. Examples include a common printer-driver which users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

### Reusable settings group

Endpoint Privilege Management supports using reusable settings groups to manage the certificates in place of adding that certificate directly to an elevation rule. Like all reusable settings groups for Intune, configurations and changes made to a reusable settings group are automatically passed to the policies that reference the group.
We recommend using a reusable settings group when you plan to use the same certificate for validating files in multiple elevation rules. This is because use of reusable settings groups is more efficient when you use the same certificate in multiple elevation rules:

- Certificates you add directly to an elevation rule: Each certificate that's added directly to a rule is uploaded as a unique instance by Intune, and that certificate instance is then associated with the file for that rule. Adding the same certificate directly to two separate rules results in it uploading twice. Later, if you must change the certificate, you must edit each individual rule that contains it. This results in Intune uploading the updated certificate a single time for each rule.
- Certificates you manage through a reusable settings group: Each time a certificate is added to a reusable settings group, Intune uploads the certificate a single time no matter how many elevation rules include that group. That instance of the certificate is then associated with the file from each rule that uses that group. Later, any change to the certificate you make can be made a single time in the reusable settings group. This change results in Intune uploading the updated file a single time, and then applying that change to each elevation rule that references the group.

## Enable your tenant for Endpoint Privilege Management

Before you can use EPM to create policies and manage file elevations, you must enable support for EPM in your tenant.

During the public preview, you can use EPM for free. To enable support for your tenant:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management**.

2. Review the available information for EPM, and when ready, select **Activate**. Intune begins to provision EPM for your tenant, which includes making the EPM component available for your devices. These components are enabled on devices when they receive a *Windows elevation settings policy*.

   :::image type="content" source="./media/epm-policies/enable-epm.png" alt-text="Activate EPM for use during the public preview." :::

## Windows elevation settings policy

After you enable Endpoint Privilege Management for your tenant, deploy *Windows elevation settings policy* to users or devices. The policy configures the following on devices:

- Enable Endpoint Privilege Management on a device.
- Set default rules for elevation requests for any file that isn't managed by an Endpoint Privilege Management elevation rule on that device.
- Configure what information EPM reports back to Intune.

A device must have an elevation settings policy that enables support for EPM before the device can process an elevation rules policy or manage elevation requests.

### Create a Windows elevation settings policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows 10 and later**, *Profile* to **Windows elevation settings policy**, and then select **Create**.

   :::image type="content" source="./media/epm-policies/create-epm-policy-1.png" alt-text="Image of the admin center UI for selecting an elevation settings policy." lightbox="./media/epm-policies/create-epm-policy-1.png":::

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, configure the following to define default behaviors for elevation requests on a device:

   :::image type="content" source="./media/epm-policies/evaluation-settings-policy.png" alt-text="Image of the evaluation settings configuration page." lightbox="./media/epm-policies/evaluation-settings-policy.png":::

   - **Endpoint Privilege Management**: Set to **Enabled** (default). When set to Disabled, the device doesn't use Endpoint Privilege Management.
   - **Default elevation response**: Configure how this device manages elevation requests for files that aren't directly managed by a rule:
     - **Not Configured**: This option functions the same as *Deny all requests*.
     - **Deny all requests**: EPM won't facilitate the elevation of files and the user is shown a pop-up window with information about the denial. This configuration doesn't prevent users with administrative permissions from using *Run as administrator* to run unmanaged files.
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

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

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

   :::image type="content" source="./media/epm-policies/create-epm-policy-1.png" alt-text="Image of the admin center UI for selecting an elevation rules policy." lightbox="./media/epm-policies/create-epm-policy-1.png":::

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, add a rule for each file that this policy manages. When you create a new policy, the policy starts includes a blank rule with an elevation type of *User confirmed* and no rule name. Start by configuring this rule, and later you can select **Add** to add additional rules to this policy. Each new rule you add has an elevation type of User confirmed, which can be changed when you configure the rule.

   :::image type="content" source="./media/epm-policies/new-elevation-rules-policy.png" alt-text="Image from the admin center UI of a new elevation rules policy." lightbox="./media/epm-policies/new-elevation-rules-policy.png":::

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

   :::image type="content" source="./media/epm-policies/add-reusable-settings.png" alt-text="Screen capture of the UI to add a reusable settings group." lightbox="./media/epm-policies/add-reusable-settings.png":::

2. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the reusable group. Name groups so you can easily identify each later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. In **Configuration settings**, select the folder icon for *Certificate file*, and browse to a **.CER** file to add it to this reusable group. The *Base 64 value* field fills in based on the certificate selected.

   :::image type="content" source="./media/epm-policies/add-a-certificate.png" alt-text="Screen capture of the UI for browsing to a certificate." lightbox="./media/epm-policies/add-a-certificate.png":::

4. In **Review + create**, review your settings and select **Add**. When you select *Add*, your configuration is saved, and group is then shown in the reusable settings group list for Endpoint Privilege Management.

## Policy conflict handling for Endpoint Privilege Management

Except for the following situation, conflicting policies for EPM are handled like any other [policy conflict](../configuration/device-profile-troubleshoot.md#conflicts).

**Windows elevation settings policy**
If a device receives separate rules for the same file:

- If the settings conflict on enabling or disabling EPM, EPM policy is enabled on the device.

**Windows elevation rules policy**
If a device receives separate rules for the same file:

- If the rules are in conflict, then the policy with the most properties that most explicitly describes the file applies.
- If the rules don't define all the same settings or options, the configurations are merged as a superset for the file on that endpoint.
- If the elevation type for the file is in conflict, settings for *User Confirmed* will apply instead of running as *Automatic*.

## Next steps

[Use reports for Endpoint Privilege Management](../protect/epm-reports.md)