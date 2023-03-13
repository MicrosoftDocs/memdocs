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

Endpoint Privilege Management (EPM) is a solution you can integrate with Microsoft Intune. EPM policies empower your organizations non-administrative users to run files that require elevated permissions, and does so with zero or limited disruptions to the users workflow. Through integration with Microsoft Intune, EPM can help you to secure your organization by removing administrative permissions for most users.

The information in this article can help you to configure the following policies and reusable settings groups for EPM:

- Windows elevation settings policy
- Windows elevation rules policy
- Reusable settings groups, which are optional configurations for your elevation rules.

Applies to:

- Windows 10
- Windows 11

## Windows elevation settings policy

Deploy a Windows elevation settings policy to users or devices to configure the following on devices:

- Enable Endpoint Privilege Management on the device.
- Set default rules for elevation requests for any file that’s not managed by an Endpoint Privilege Management elevation rule policy on that device.
- Configure what information elevation requests and activity are reported back to Intune.

To create the policy:

## Windows elevation rules policy

Deploy a *Windows elevation rules policy* to users or devices to deploy one or more rules for files that are managed for elevation by Endpoint Privilege Management. Each rule you add to this policy:

- Identifies a file tor which you manage elevation requests.
- Can include a certificate to help validate that file’s integrity before it’s run. You can also add a reusable group that contains a certificate that you then use with one or more rules or policies.
- Specifies if the elevation type of the file as automatic (silently) or requiring user confirmation. With user confirmation, you can add additional user actions that must be completed before the file is run.
In addition to this policy, a device must also be assigned a Windows elevation settings policy that enables Endpoint Privilege Management.

### Create a Windows elevation rules policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Policies** tab > and then select **Create Policy**.
   Set the *Platform* to **Windows 10 and later**, *Profile* to **Windows elevation rules policy**, and then select **Create**.

2. On **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the profile. Name profiles so you can easily identify them later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. On **Configuration settings**, add a rule for each file that this policy will manage. When you create a new policy, you’ll find a blank rule with an elevation type of *User confirmed* and no rule name. Start by configuring this rule, and later you can select **Add** to add additional rules to this policy. Each new rule you add has an elevation type of User confirmed, which can be changed when you configure the rule.

   To configure a rule, select **Edit instance** to open its *Rule properties* page and then configure the following:

   - **Rule name**: Like a policy name, enter a descriptive name for the rule. Name your rules so you can easily identify them later.
   - **Description** (Optional): Enter a description for the profile.

   *Elevation conditions* are conditions that define how a file runs, and user validations that must be met before the file this rule applies to can be run.

   - **Elevation type**: By default, this is set to *User confirmed*, which is the elevation type we recommend for most files.

     - **User confirmed**: We recommend this option for most rules. When a file is run, the user receives a simple prompt to confirm their intent to run the file. The rule can also include additional requirements that are available from the *Validation* drop down:
       - *Business justification*: Require the user to enter a justification for running the file. There is no required format for this, however the user input is saved and can be reviewed through logs if the *Reporting scope* includes collection of endpoint elevations. 
       - *Windows authentication*: This option requires the user to authenticate using their organization credentials.
     - **Automatic**: This elevation type automatically runs the file in question with elevated permissions. This is done invisibly to the user, without prompting for confirmation or requiring justification or authentication by the user. 

       Use this type of elevation for only files you trust. Examples include a common and well-known printer-driver that users are expected to install, or a productivity app like the setup file for Microsoft Office 365.

   *File information* is where you specify the details that identify a file and file instance that this rule applies to.

   - **File name**: Specify the file name and its extension. For example: `notepad.exe`
   - **File path** (Optional): Specify the location of the file in relation to the local device where the file is to be run. If the file can be run from any location or is unknown, you can leave this blank. You can also use a variable.
   - **Signature source**: Choose one of the following options:

     - **Use a certificate file in reusable settings** (Default): This option uses a certificate file that has been added to a reusable settings group for Endpoint Privilege Management. You must [create a reusable settings group](#reusable-settings-groups) before you can use this option.

        To identify the *Certificate*, select *Add or remove a certificate* and then select the reusable group that contains the correct certificate. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*. 

     - **Upload a certificate file**: With this option you add a certificate file directly to the elevation rule. For *File upload*, specify a **.cer** file that can validate the integrity of the file that this rule applies to. Then, specify the *Certificate type* of *Publisher* or *Certificate authority*.

   - **File hash**: The file hash is required when Signature source is set to Not configured, and optional when set to use a certificate.
   - **Minimum version**: (Optional) Use the **x.x.x.x** format to specify a minimum version of the file that is supported by this rule.
   - **File description**: (Optional) Provide a description of the file.
   - **Product name**: (Optional) Specify the name of the product that the file is from.
   - **Internal name**: (Optional) Specify the internal name of the file.

   When you are done adding rules to this policy, select **Next**.

4. On the **Scope tags** page, select any desired scope tags to apply, then select **Next**.

5. For **Assignments**, select the groups that will receive the policy. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).
   Select **Next**.

6. In **Review + create**, review your settings and select **Create**. When you select *Create*, your changes are saved, and the profile is assigned. The policy is also shown in the policy list.

## Reusable settings groups

Endpoint Privilege Management uses reusable settings groups to manage the certificates that validate the files you manage with Endpoint Privilege Management elevation rules. Like all reusable settings groups for Intune, changes to a reusable group are automatically passed to the policies that reference the group. For Endpoint Privilege Management, this means if you must update the certificate you use for file validation, you would only need to update it in the reusable settings group a single time to have that updated certificate applied to all your elevation rules that use that group.

To create the reusable settings group for Endpoint Privilege Management:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Endpoint security** > **Endpoint Privilege Management** > select the **Reusable settings (preview)** tab > and then select **Add**.

2. On **Basics**, enter the following properties:
   - **Name**: Enter a descriptive name for the reusable group. Name groups so you can easily identify each later.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

3. In **Configuration settings**, select the folder icon for *Certificate file*, and browse to a **.CER** file to add it to this reusable group. The *Base 64 value* field fills in based on the certificate selected.

4. In **Review + create**, review your settings and select **Add**. When you select *Add*, your configuration is saved, and group is then shown in the reusable settings group list for Endpoint Privilege Management.

## Next steps

[Use reports for Endpoint Privilege Management](../protect/epm-reports.md)