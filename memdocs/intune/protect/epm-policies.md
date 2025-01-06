---
title: Configure policies to manage Endpoint Privilege Management with Microsoft Intune
description: Configure policies that define how Endpoint Privilege Management functions in your tenant, and behaviors when elevating files to run in administrative context.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/27/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

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
- sub-intune-suite
---

# Configure policies for Endpoint Privilege Management

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

With Microsoft Intune **Endpoint Privilege Management (EPM)** your organization’s users can run as a standard user (without administrator rights) and complete tasks that require elevated privileges. Tasks that commonly require administrative privileges are application installs (like Microsoft 365 Applications), updating device drivers, and running certain Windows diagnostics.

Endpoint Privilege Management supports your zero-trust journey by helping your organization achieve a broad user base running with least privilege, while allowing users to still run tasks allowed by your organization to remain productive.

The information in this article can help you to configure the following policies and reusable settings for EPM:

- Windows elevation settings policy.
- Windows elevation rules policy.
- Reusable settings groups, which are optional configurations for your elevation rules.

Applies to:

- Windows 10
- Windows 11

## Get started with EPM policies

Endpoint Privilege Management uses two policy types that you configure to manage how a file elevation request is handled. Together, the policies configure the behavior for file elevations when standard users request to *run with administrative privileges*.

Before you can create Endpoint Privilege Management policies, you must license EPM in your tenant as an Intune add-on. For licensing information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

### About Windows elevation settings policy

Use *Windows elevation settings policy* when you want to:

- **Enable Endpoint Privilege Management** on devices. By default, this policy enables EPM. When first enabled for EPM, a device provisions the components that collect usage data on elevation requests and that enforce elevation rules.

  If a device has EPM disabled, the client components immediately disable. There's a delay of seven days before the EPM component is completely removed. The delay helps to reduce the time it takes to restore EPM should a device accidentally have EPM disabled or its elevation settings policy unassigned.

- **Default elevation response** - Set a default response for an *elevation request* of any file that isn't managed by a *Windows elevation rule policy*. For this setting to have an effect, no rule can exist for the application **AND** an end user must *explicitly request* elevation through the *Run with elevated access* right-click menu. By default, this option isn't configured. If no setting is delivered, the EPM components fall back to their built-in default, which is to **deny all requests**.
  
  Options include:

  - **Deny all requests** - This option blocks the *elevate request* action for files that aren't defined in a Windows elevation rules policy.
  - **Require user confirmation** - When user confirmation is required, you can choose from the same validation options as found for Windows elevation rules policy.
  - **Require support approval** - When support approval is required, an administrator must approve elevation requests without a matching rule prior to the elevation being required.

  > [!NOTE]
  >
  > Default responses are only processed for requests coming through the *Run with elevated access* right-click menu.

- **Validation options** - Set validation options when the default elevation response is defined as *Require user confirmation*.

  Options include:

  - **Business justification** - This option requires the end user to provide a justification before completing an elevation that is facilitated by the default elevation response.
  - **Windows authentication** - This option requires the end user to authenticate before completing an elevation that is facilitated by the default elevation response.

  >[!NOTE]
  > Multiple validation options can be selected to satisfy the needs of the organization. If no options are selected, then the user is only required to select *continue* to complete the elevation.
  
- **Send elevation data for reporting** - This setting controls whether your device shares diagnostic and usage data with Microsoft. When enabled to share data, the type of data is configured by the *Reporting scope* setting.

  Diagnostic data is used by Microsoft to measure the health of the EPM client components. Usage data is used to show you elevations that happen within your tenant. For more information about the types of data and how it's stored, see [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md).

  Options include:

  - **Yes** - This option sends data to Microsoft based on the *Reporting Scope* setting.
  - **No** - This option does not send data to Microsoft.

- **Reporting Scope** - This setting controls the amount of data being sent to Microsoft when *Send elevation data for reporting* is set to *Yes*. By default, *Diagnostic data and all endpoint elevations are selected.

  Options include:

  - **Diagnostic data and managed elevations only** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about elevations being facilitated by Endpoint Privilege Management.
  - **Diagnostic data and all endpoint elevations** - This option sends diagnostic data to Microsoft about the health of the client components **AND** data about *all* elevations happening on the endpoint.
  - **Diagnostic data only** - This option sends only the diagnostic data to Microsoft about the health of the client components.

### About Windows elevation rules policy

Use profiles for *Windows elevation rules policy* to manage the identification of specific files, and how elevation requests for those files are handled. Each *Windows elevation rule policy* includes one or more *elevation rules*. It's with elevation rules that you configure details about the file being managed and requirements for it to be elevated.

The following types of files are supported:

- Executable files with the `.exe` or `.msi` extension.
- PowerShell scripts with the `.ps1` extension.

Each elevation rule instructs EPM on how to:

- **Identify the file using**:

  - *File name (including extension).* The rule also supports optional conditions like a minimum build version, product name, or internal name. Optional conditions are used to further validate the file when elevation is attempted.
  - *Certificate.* Certificates can be added directly to a rule, or by using a reusable settings group. When a certificate is used in a rule, it's also required to be valid. We recommend the use of reusable settings groups as they can be more efficient and simplify a future change to the certificate. For more information, see the next section [Reusable settings groups](#reusable-settings-group).

- **Validate the file**:

  - *File hash.* A file hash is required for automatic rules. For user confirmed rules, you can choose to either use a certificate or a file hash, in which case the file hash becomes optional.
  - *Certificate.* If a certificate is provided Windows API's are used to validate the certificate and revocation status.
  - *Additional Properties.* Any additional properties specified in the rules must match.

- **Configure the files elevation type.** Elevation type identifies what happens when an elevation request is made for the file. By default, this option is set to *User confirmed*, which is our recommendation for elevations.

  - **User confirmed** (Recommended): A user confirmed elevation always requires the user to select on a confirmation prompt to run the file. There are more user confirmations you can add. One requires users to authenticate using their organization credentials. Another option requires the user to enter a business justification. While the text entered for a justification is up to the user, EPM can collect and report it when the device is configured to report elevation data as part of its Windows elevation settings policy.
  - **Automatic**: An automatic elevation happens invisibly to the user. There's no prompt, and no indication that the file is running in an elevated context.
  - **Support approved**: An administrator must approve any [support-required elevation request](../protect/epm-support-approved.md) that doesn't have a matching rule, before the application is allowed to run with elevated privileges.

- **Manage the behavior of child processes.** You can set the elevation behavior that applies to any child processes that the elevated process creates.

  - **Require rule to elevate** - Configure a child processes to require its own rule before that child process can run in an elevated context.
  - **Deny all** - All child processes launch without elevated context.
  - **Allow child processes to run elevated** - Configure a child process to always run elevated.

> [!NOTE]
> For more information about creating *strong rules*, see our [guidance for creating elevation rules with Endpoint Privilege Management](../protect/epm-guidance-for-creating-rules.md).
>
> You can also use the `Get-FileAttributes` PowerShell cmdlet from the [EpmTools PowerShell module](../protect/epm-overview.md#epmtools-powershell-module). This cmdlet can retrieve file attributes for an .exe file and extract its Publisher and CA certificates to a set location that you can use to populate Elevation Rule Properties for a particular application.

> [!CAUTION]
>
> We recommend automatic elevation be used sparingly, and only for trusted files that are business critical. End users automatically elevate these applications at *every* launch of that application.

### Reusable settings group

Endpoint Privilege Management supports using reusable settings groups to manage the certificates in place of adding that certificate directly to an elevation rule. Like all reusable settings groups for Intune, configurations and changes made to a reusable settings group are automatically passed to the policies that reference the group.
We recommend using a reusable settings group when you plan to use the same certificate to validate files in multiple elevation rules. The use of reusable settings groups is more efficient when you use the same certificate in multiple elevation rules:

- Certificates you add directly to an elevation rule: Each certificate that's added directly to a rule is uploaded as a unique instance by Intune, and that certificate instance is then associated with that rule. Adding the same certificate directly to two separate rules results in it uploading twice. Later, if you must change the certificate, you must edit each individual rule that contains it. With each rule change, Intune uploads the updated certificate a single time for each rule.
- Certificates you manage through a reusable settings group: Each time a certificate is added to a reusable settings group, Intune uploads the certificate a single time no matter how many elevation rules include that group. That instance of the certificate is then associated with the file from each rule that uses that group. Later, any change to the certificate you make can be made a single time in the reusable settings group. This change results in Intune uploading the updated file a single time, and then applying that change to each elevation rule that references the group.

## Windows elevation settings policy

To configure the following options on devices, deploy *Windows elevation settings policy* to users or devices:

- Enable Endpoint Privilege Management on a device.
- Set default rules for elevation requests for any file that isn't managed by an Endpoint Privilege Management elevation rule on that device.
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

   - **Send elevation data for reporting**: By default, this behavior is set to **Yes**. When set to yes, you can then configure a *Reporting scope*. When set to **No**, a device doesn’t report diagnostic data or information about file elevations to Intune.
   - **Reporting scope**: Choose what type of information a device reports to Intune:
     - **Diagnostic data and all endpoint elevations** (Default): The device reports diagnostic data and details about all file elevations that EPM facilitates.

       This level of information can help you identify other files that aren't yet managed by an elevation rule that users seek to run in an elevated context.

     - **Diagnostic data and managed elevations only**: The device reports diagnostic data and details about file elevations for only those files that are managed by an elevation rule policy. File requests for unmanaged files, and files that are elevated through the Windows default action of *Run as administrator*, aren't reported as managed elevations.
     - **Diagnostic data only**: Only diagnostic data for the operation of Endpoint Privilege Management is collected. Information about file elevations isn’t reported to Intune.

   When ready, select **Next** to continue.

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md). Select **Next**.

6. For **Review + create**, review your settings and then select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## Windows elevation rules policy

Deploy a *Windows elevation rules policy* to users or devices to deploy one or more rules for files that are managed for elevation by Endpoint Privilege Management. Each rule you add to this policy:

- Identifies a file for which you want to manage elevation requests.
- Can include a certificate to help validate that file’s integrity before it’s run. You can also add a reusable group that contains a certificate that you then use with one or more rules or policies.
- Can include one or more manually added [file arguments or command line switches](#use-file-arguments-for-elevation-rules). When file arguments are added to a rule, EPM only allows file elevation of requests that include one of the defined command lines. If a defined command line isn’t part of the file elevation request, EPM denies that request.
- Specifies if the elevation type of the file is automatic (silently) or if it requires user confirmation. With user confirmation, you can add additional user actions that must be completed before the file is run.

In addition to this policy, a device must also be assigned a Windows elevation settings policy that enables Endpoint Privilege Management.

Use either of the following methods to create new elevation rules, which are added to elevation rules policy:

- [**Automatically configure elevation rules**](#automatically-configure-elevation-rules-for-windows-elevation-rules-policy) – Use this method to save time when creating an elevation rule by autopopulating the file detection details that Intune has already collected. The file details are identified by Intune from either The *[Elevation report](../protect/epm-reports.md#elevation-report)* or from a *[support approved](../protect/epm-support-approved.md)* elevation requests record.

  With this method, you:  

  - Select the file for which you want to create an elevation rule from the Elevation report or *support approved* elevation request.  
  - Choose to add the new elevation rule to an existing elevation rules policy or create a new elevation rules policy that includes the new rule.
    - When added to an existing policy, the new rule is immediately available to that policies list of assigned groups.
    - When a new policy is created, you must edit that policy to assign groups before it becomes available for use.

- [**Manually configure elevation rules**](#manually-configure-elevation-rules-for-windows-elevation-rules-policy) – This method requires you to have identified the file details you want to use for detection and to manually enter them as part of the rule creation workflow. For information about detection criteria, see [Defining rules for use with Endpoint Privilege Management](../protect/epm-guidance-for-creating-rules.md#defining-rules-for-use-with-endpoint-privilege-management).

  With this method, you:

  - Manually determine the file details to use and then add them to the elevation rule for file identification.
  - Configure all aspects of the policy during policy creation, including assigning the policy to groups for use.
  - Can add one or more file arguments that must be part of the elevation request before EPM will allow file elevation.

### Automatically configure elevation rules for Windows elevation rules policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management**. To select a file to use for an elevation rule, choose one of the following starting paths:

   **Start from a Report:**

   1. Select the **Reports** tab and then the **Elevation report** tile. Locate the file you want to create a rule for in the *File* column.
   2. Select the linked name of the file to open that files **Elevation detail** pane.

   **Start from a support approved elevation request:**

   1. Select the **Elevation request** tab.
   2. From the *File* column, select the file that you want to use for the elevation rule, which opens that files **Elevation detail** pane.

      The status of the elevation request doesn’t matter. You can use a pending request or one that was previously approved or denied.

2. On the **Elevation detail** pane, review the file details. This information is used by the elevation rule to identify the correct file. When ready, select **Create a rule with these file details**.

   :::image type="content" source="./media/epm-policies/elevation-detail-pane.png" alt-text="Image from the admin center UI of a file selected from the Elevation report." lightbox="./media/epm-policies/elevation-detail-pane.png":::

3. Select a policy option for the new elevation rule you're creating:

   **Create a new policy:**  
   This option creates a new policy that includes an elevation rule for the file you selected.

   1. For the rule, configure the **Type** and **Child process behavior**, and then select **OK** to create the policy.
   2. When prompted, provide a **Policy name** for the new policy and confirm creation of what will be a new and unassigned elevation rules policy.
   3. After the policy is created, you can edit the policy to assign it and add additional configurations if needed.

   **Add to an existing policy:**  
   With this option, use the drop-down list and select an existing elevation policy to which the new elevation rule is added.

   1. For the rule, configure the elevation **Type** and **Child process behavior**, and then select **OK**. The policy is updated with the new rule.
   2. After the rule is added to the policy, you can edit the policy to gain access to the rule and then modify it to make additional configurations if needed.

   **Require the same file path as this elevation:**  
   When you select this checkbox, the File Path field in the rule is set to the file path as seen in the report. If the checkbox isn’t selected, the path remains empty.

   :::image type="content" source="./media/epm-policies/create-a-rule.png" alt-text="Image from the admin center UI of the create a rule pane." lightbox="./media/epm-policies/create-a-rule.png":::

### Manually configure elevation rules for Windows elevation rules policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows**, *Profile* to **Windows elevation rules policy**, and then select **Create**.

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, add a rule for each file that this policy manages. When you create a new policy, the policy starts includes a blank rule with an elevation type of *User confirmed* and no rule name. Start by configuring this rule, and later you can select **Add** to add more rules to this policy. Each new rule you add has an elevation type of User confirmed, which can be changed when you configure the rule.

   :::image type="content" source="./media/epm-policies/new-elevation-rules-policy.png" alt-text="Image from the admin center UI of a new elevation rules policy." lightbox="./media/epm-policies/new-elevation-rules-policy.png":::

   To configure a rule, select **Edit instance** to open its Rule properties page, and then configure the following:

   :::image type="content" source="./media/epm-policies/elevation-rules.png" alt-text="Image of the elevation rules properties." lightbox="./media/epm-policies/elevation-rules.png":::

   - **Rule name**: Specify a descriptive name for the rule. Name your rules so you can easily identify them later.
   - **Description** (Optional): Enter a description for the profile.

   *Elevation conditions* are conditions that define how a file runs, and user validations that must be met before the file this rule applies to can be run.

   - **Elevation type**: By default, this option is set to *User confirmed*, which is the elevation type we recommend for most files.

     - **User confirmed**: We recommend this option for most rules. When a file is run, the user receives a simple prompt to confirm their intent to run the file. The rule can also include other prompts that are available from the *Validation* drop down:

       - *Business justification*: Require the user to enter a justification for running the file. There's no required format for the entry. The user input is saved and can be reviewed through logs if the *Reporting scope* includes collection of endpoint elevations.
       - *Windows authentication*: This option requires the user to authenticate using their organization credentials.

     - **Automatic**: This elevation type automatically runs the file in question with elevated permissions. Automatic elevation is transparent to the user, without prompting for confirmation or requiring justification or authentication by the user.

       > [!CAUTION]
       >
       > Only use automatic elevation for files you trust. These files will automatically elevate without user interaction. Rules that aren't well defined could allow unapproved applications to elevate. For more information on creating strong rules, see the [guidance for creating rules](../protect/epm-guidance-for-creating-rules.md).

     - **Support approved**: This elevation type requires an administrator to approve a request prior to the elevation being allowed to complete. For more information, see [Support approved elevation requests](../protect/epm-support-approved.md).

       > [!Important]
       >
       > Use of support approved elevation for files requires that Admins with additional permissions review and approve each file elevation request before that file on the device with administrator permissions. For information about using the support approved elevation type, see [Support approved file elevations for Endpoint Privilege Management](../protect/epm-support-approved.md).

   - **Child process behavior**: By default, this option is set to *Require rule to elevate*, which requires the child process to match the same rule as process that creates it. Other options include:
     - *Allow all child processes to run elevated*: This option should be used with caution as it allows applications to create child processes unconditionally.
     - *Deny all*: This configuration prevents any child process from being created.

   *File information* is where you specify the details that identify a file that this rule applies to.

   - **File name**: Specify the file name and its extension. For example: `myapplication.exe`
   - **File path** (Optional): Specify the location of the file. If the file can be run from any location or is unknown, you can leave this blank. You can also use a variable.
   - **Signature source**: Choose one of the following options:

     - **Use a certificate file in reusable settings** (Default): This option uses a certificate file that has been added to a reusable settings group for Endpoint Privilege Management. You must [create a reusable settings group](#reusable-settings-groups) before you can use this option.

       To identify the *Certificate*, select *Add or remove a certificate*, and then select the reusable group that contains the correct certificate. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.

     - **Upload a certificate file**: Add a certificate file directly to the elevation rule. For *File upload*, specify a **.cer** file that can validate the integrity of the file that this rule applies to. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.

     - **Not configured**: Use this option when you don't want to use a certificate to validate the integrity of the file. When no certificate is used, you must provide a *file hash*.

   - **File hash**: The file hash is required when Signature source is set to *Not configured*, and optional when set to use a certificate.
   - **Minimum version**: (Optional) Use **x.x.x.x** format to specify a minimum version of the file that is supported by this rule.
   - **File description**: (Optional) Provide a description of the file.
   - **Product name**: (Optional) Specify the name of the product that the file is from.
   - **Internal name**: (Optional) Specify the internal name of the file.

   Select **Save** to save the rule configuration. You can then **Add** more rules. After adding all the rules this policy requires, select **Next** to continue.

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md). Select **Next**.

6. In **Review + create**, review your settings and then select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

### Use file arguments for elevation rules

When you manually configure or edit a [file elevation rule](#windows-elevation-rules-policy), you can add one or more file command lines or arguments to help you control how that file is used, and what it can be used to do when it's run in an elevated context.

For example, you might have an elevation rule for the troubleshooting tool [**dsregcmd**](/troubleshoot/entra/identity/devices/troubleshoot-device-dsregcmd) that can be useful for investigating the state of a device in Microsoft Entra ID. To help support this files use for investigation, you can configure the rule with a list of arguments for *dsregcmd* that includes the switches for **/status**, **/listaccounts** and more. However, to prevent a destructive action like unregistering a device you choose to not include* a switch like [**/leave**](/troubleshoot/entra/entra-id/dir-dmns-obj/pending-devices#the-state-of-a-registered-device-is-changed-to-pending). With this configuration, the rule then requires the elevation request include one of the defined switches (*/status, or *listaccounts) before it can be run in the elevated context. At the same time, users can’t accidentally (or with intent) use *dsregcmd* with the */leave* switch, to remove the device from Microsoft Entra ID.

To add one or more arguments to an elevation rule, set **Restrict arguments** to **Allow list**.  With this set, you can then select Add and then configure individual  command line options. By adding multiple arguments, you provide multiple command lines that are supported by elevation requests.

:::image type="content" source="./media/epm-policies/add-argument.png" alt-text="Screen capture of the UI for configuring command line arguments.":::

> [!IMPORTANT]
> When an elevation rule includes at least one argument or command line through the argument list, the rule then requires that one of the configured arguments be used. If the file elevation request doesn’t include the exact command line as defined by one of the arguments on the argument list, EPM blocks that rule from running the file in an elevated context.


## Reusable settings groups

Endpoint Privilege Management uses reusable settings groups to manage the certificates that validate the files you manage with Endpoint Privilege Management elevation rules. Like all reusable settings groups for Intune, changes to a reusable group are automatically passed to the policies that reference the group. If you must update the certificate you use for file validation, you only need to update it in the reusable settings group a single time. Intune applies the updated certificate to all your elevation rules that use that group.

To create the reusable settings group for Endpoint Privilege Management:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Reusable settings (preview)** tab > and then select **Add**.

   :::image type="content" source="./media/epm-policies/add-reusable-settings.png" alt-text="Screen capture of the UI to add a reusable settings group." lightbox="./media/epm-policies/add-reusable-settings.png":::

2. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the reusable group. Name groups so you can easily identify each later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. In **Configuration settings**, select the folder icon for *Certificate file*, and browse to a **.CER** file to add it to this reusable group. The *Base 64 value* field fills in based on the certificate selected.

   :::image type="content" source="./media/epm-policies/add-a-certificate.png" alt-text="Screen capture of the UI for browsing to a certificate." lightbox="./media/epm-policies/add-a-certificate.png":::

4. In **Review + create**, review your settings and then select **Add**. When you select *Add*, your configuration is saved, and group is then shown in the reusable settings group list for Endpoint Privilege Management.

## Policy conflict handling for Endpoint Privilege Management

Except for the following situation, conflicting policies for EPM are handled like any other [policy conflict](../configuration/device-profile-troubleshoot.md#conflicts).

**Windows elevation settings policy**:

When a device receives two separate elevation settings policies with conflicting values, the EPM client reverts to the default client behavior until the conflict is resolved.

> [!NOTE]
>
> If *Enable Endpoint Privilege Management* is in conflict, the default behavior of the client is to *Enable* EPM. This means the client components will continue to function until an explicit value is delivered to the device.

**Windows elevation rules policy**:

If a device receives two rules targeting the same application, both rules are consumed on the device. When EPM goes to resolve rules that apply to an elevation, it uses the following logic:

- Rules deployed to a user take precedence over rules deployed to a device.
- Rules with a hash defined are always deemed the most *specific* rule.
- If more than one rule applies (with no hash defined), the rule with the most defined attributes wins (most *specific*).
- If applying the proceeding logic results in more than one rule, the following order determines the elevation behavior: User Confirmed, Support Approved, and then Automatic.

> [!NOTE]
> If a rule does not exist for an elevation and that elevation was requested through the *Run with elevated access* right-click context menu, then the *Default Elevation Behavior* will be used.

## Next steps

- [Guidance for creating Elevation Rules](../protect/epm-guidance-for-creating-rules.md)
- [Reports for Endpoint Privilege Management](../protect/epm-reports.md)
- [Approving elevation requests](../protect/epm-support-approved.md)
- [Data collection and privacy for Endpoint Privilege Management](../protect/epm-data-collection.md)
- [Deployment considerations and frequently asked questions](../protect/epm-deployment-considerations-ki.md)
