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

Microsoft Intune Endpoint Privilege Management (EPM) allows your organization’s users to run as a standard user (without administrator rights) and complete tasks that require an elevated privileges. Tasks that commonly require administrative privileges are application installs (such as Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics. Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The information in this article can help you to configure the following policies and reusable settings for EPM:

- Enable your tenant for Endpoint Privilege Management
- Windows elevation settings policy
- Windows elevation rules policy
- Reusable settings groups, which are optional configurations for your elevation rules.

Applies to:

- Windows 10
- Windows 11

## Getting started with EPM policies

EPM uses the two policy types that you configure to manage how a file elevation request is handled. Together, the policies configure how standard users elevate scenarios they request to *run with administrative privileges*:

### Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:
<!-- To enable Endpoint Privilege Management (EPM) on a device, a *Windows elevation settings policy* must be assigned to it. This policy is necessary for EPM to be enabled, and includes the following uses: -->

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device provisions components that collection usage data on elevation requests and enforce elevation rules.

  If a device has EPM disabled, the client components immediately disable. There's a delay of seven days before the EPM component is completely removed. The delay can reduce the time it takes to restore EPM should a device have accidentally had EPM disabled, or its elevation settings policy unassigned accidentally.

- **Default elevation response** - Set a default response for an *elevation request* of any file that’s not managed by a *Windows elevation rule policy*. For this setting to have an effect, no rule can exist for the application **AND** an end user must have *explicity requested* elevation through the *Run with elevated access* right-click menu. By default, this option isn't configured. If no setting is delivered the EPM components will fall back to their built-in default, which is **deny all requests**.
  
    Options include:
  - Deny all requests - This option blocks the *elevate request* action for files that aren't defined in a Windows elevation rules policy.
  - Require user confirmation - When confirmation is required you can choose from the same options as found for Windows elevation rules policy.

    >[!NOTE]
    > Default responses are only processed for requests coming through the *Run with elevated access* right-click menu.  

- **Validation options** - Set validation options when the default elevation response is defined as *Require user confirmation*

    Options include:
  - Business justification - This option requires the end user to provide a justification before completing an elevation that is facilitated by the default elevation response
  - Windows authentication - This option requires the end user to authenticate before completing an elevation that is facilitated by the default elevation response

    >[!NOTE]
    > Multiple validation options can be selected to satisfy needs of the organization. If no options are selected, then the user is only required to click *continue* to complete the elevation
  
- **Send data to Microsoft** - This setting controls whether your device will share both diagnostic and usage data with Microsoft. Diagnostic data is used by Microsoft to measure the health of the EPM client components and usage data is used to show you elevations that happen within your tenant. For more information about the types of data and how it's stored see [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md).

    Options include:
  - Yes - This option sends data to Microsoft based on the *Reporting Scope* setting
  - No - This option does not send data to Microsoft

- **Reporting Scope** - This setting controls the amount of data being sent to Microsoft when *Send data to Microsoft* is set to *Yes*. By default, *Diagnostic data and all endpoint elevations* is selected.

    Options include:
  - Diagnostic data and managed elevations only - This option only sends diagnostic data to Microsoft about the health of the client components **AND** data about elevations being facilitated by Endpoint Privilege Management
  - Diagnostic data and all endpoint elevations - This option only sends diagnostic data to Microsoft about the health of the client components **AND** data about all elevations happening on the endpoint
  - Diagnostic data only - This option only sends diagnostic data to Microsoft about the health of the client components.

### Windows elevation rules policy

Use profiles for *Windows elevation rules policy* to manage the identification of specific files, and how to elevation requests for those files are handled. Each *Windows elevation rule policy* includes one or more *elevation rules*. It's with elevation rules that you configure details about the file being managed and requirements for it to be elevated.

Each elevation rule:

- **Uses the file name (including extension) to identify the file the rule applies to.** The rule also supports optional conditions like a minimum build version, product name, or internal name. Optional conditions are used to do further validation on the file when elevation is attempted.
- **Supports use of a certificate to validate the files integrity before its run on a device.** Certificates can be added directly to a rule, or by using a reusable settings group. We recommend the use of reusable settings groups as they can be more efficient and simplify a future change to the certificate. For more information, see the next section [Reusable settings groups](#reusable-settings-group).
- **Supports use of a file hash to validate the file.** A file hash is required for Automatic rules. For user confirmed rules, you can chose to either use a certificate or a file hash, in which case the file hash becomes optional.
- **Configures the files evaluation type.** Evaluation type identifies what happens when an elevation request is made for the file. By default, this option is set to *User confirmed*, which is our recommendation for elevations.
  - **User confirmed** (Recommended): A user confirmed elevation always requires the user to click on a confirmation prompt to run the file. There are additional user confirmations you can add. One require users to authenticate using their organization credentials. Another option requires the user to enter a business justification. While the text entered for a justification is up to hte user, EPM can collect and report it when the device is configured to report elevation data as part of its Windows elevation settings policy.
  - **Automatic** elevation happens invisibly to the user. There's no prompt, and no indication that the file is running in an elevated context.

    >[!NOTE]
    > For more information about creating *strong rules*, see our [guidance for creating elevation rules with Endpoint Privilege Management](../protect/epm-guidance-for-creating-rules.md)

    >[!CAUTION]  
    > We recommend automatic elevation be used sparingly, and only for trusted files that are business critical. End users will automatically elevation these applications at every launch of that application.

### Reusable settings group

Endpoint Privilege Management supports using reusable settings groups to manage the certificates in place of adding that certificate directly to an elevation rule. Like all reusable settings groups for Intune, configurations and changes made to a reusable settings group are automatically passed to the policies that reference the group.
We recommend using a reusable settings group when you plan to use the same certificate for validating files in multiple elevation rules. This is because use of reusable settings groups is more efficient when you use the same certificate in multiple elevation rules:

- Certificates you add directly to an elevation rule: Each certificate that's added directly to a rule is uploaded as a unique instance by Intune, and that certificate instance is then associated with that rule. Adding the same certificate directly to two separate rules results in it uploading twice. Later, if you must change the certificate, you must edit each individual rule that contains it. This results in Intune uploading the updated certificate a single time for each rule.
- Certificates you manage through a reusable settings group: Each time a certificate is added to a reusable settings group, Intune uploads the certificate a single time no matter how many elevation rules include that group. That instance of the certificate is then associated with the file from each rule that uses that group. Later, any change to the certificate you make can be made a single time in the reusable settings group. This change results in Intune uploading the updated file a single time, and then applying that change to each elevation rule that references the group.

## Enable your tenant for Endpoint Privilege Management

Before you can use EPM to create policies and manage file elevations, you must enable EPM in your tenant.

During the public preview, you can use EPM without acquiring a license or a trial. To enable support for your tenant:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management**.

2. Review the available information for EPM, and when ready, select **Activate**. Intune begins to provision EPM for your tenant, which includes making the EPM component available to be deployed to your devices. These components are enabled on devices when they receive a *Windows elevation settings policy*.

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
     - **Automatic**: This elevation type automatically runs the file in question with elevated permissions. This is transparent to the user, without prompting for confirmation or requiring justification or authentication by the user.
      >[!CAUTION]
      >Only use the automatic elevation for files you trust. These files will automatically elevate without user interaction. Rules that are not well defined could allow unapproved applications to elevate. For more information on creating strong rules, see the [guidance for creating rules](../protect/epm-guidance-for-creating-rules.md).

   *File information* is where you specify the details that identify a file that this rule applies to.

   - **File name**: Specify the file name and its extension. For example: `myapplication.exe`
   - **File path** (Optional): Specify the location of the file. If the file can be run from any location or is unknown, you can leave this blank. You can also use a variable.
   - **Signature source**: Choose one of the following options:

     - **Use a certificate file in reusable settings** (Default): This option uses a certificate file that has been added to a reusable settings group for Endpoint Privilege Management. You must [create a reusable settings group](#reusable-settings-groups) before you can use this option.

        To identify the *Certificate*, select *Add or remove a certificate*, and then select the reusable group that contains the correct certificate. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.

     - **Upload a certificate file**: Add a certificate file directly to the elevation rule. For *File upload*, specify a **.cer** file that can validate the integrity of the file that this rule applies to. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.
     - **Not configured**: Use this option when do not want to use a certificate to validate the integrity of the file. When no certificate is used, you must provide a *file hash*.

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

When a device receives two separate elevation settings policies with conflicting values, the EPM client will revert to the default client behavior until the conflict is resolved.

> [!Note]
> If the *Enable Endpoint Privilege Management* is in conflict the default behavior of the client is to *Enable* EPM. This means the client components will continue to function until an explicit value is delivered to the device.

**Windows elevation rules policy**

If a device receives two rules targeting the same application, both rules are consumed on the device. When EPM goes to resolve rules that apply to an elevation, it used the following logic:

- Rules deployed to a user take precedence over rules deployed to a device
- Rules with a hash defined are always deemed the most *specific* rule
- If more than one rule applies (with no hash defined), the rule with the most defined attributes wins (most *specific*)
- If applying the above logic results in more than one rule, the following order determines the elevation behavior: User Confirmed, Support Approved (once available), Automatic
 
> [!NOTE]
> If a rule does not exist for an elevation and that elevation was requested through the *Run with elevated access* right-click context menu, then the *Default Elevation Behavior* will be used.

## Next steps

[Use reports for Endpoint Privilege Management](../protect/epm-reports.md)