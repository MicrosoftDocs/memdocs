---
# Required metadata

title: Jamf Managed Device Compliance with Microsoft Entra ID
titleSuffix: Microsoft Intune
description: Integrate Jamf Pro with Microsoft Intune to report device compliance to Microsoft Entra ID. 
author: jeffducasse
ms.author: lanewsad
manager: dougeby
ms.date: 09/12/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:

#audience:

ms.reviewer: jeffducasse
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- conditional-access
- sub-mtd-apps
---

# Integrate Jamf Pro with Microsoft Intune to report device compliance to Microsoft Entra ID

The process to establish integration between Jamf Pro and Microsoft Intune is evolving. The reporting of the compliance status of Jamf managed devices is now able to allow the Jamf Pro environment to determine the status of compliance with Jamf managed policies and report the state of device compliance to Microsoft Entra ID through a connector in Intune. Once the compliance status for devices managed by Jamf are reported to Microsoft Entra ID, those devices are able to meet the Zero-Trust principles that Microsoft Entra Conditional Access policies establish.

> [!IMPORTANT]
>
> **Jamf macOS device support for Conditional Access is being deprecated**.
>
> Beginning on January 31, 2025, the platform that Jamf Pro's Conditional Access feature is built on will no longer be supported.
>
> If you use Jamf Pro's Conditional Access integration for macOS devices, follow Jamf's documented guidelines to migrate your devices to Device Compliance integration at [***Migrating from macOS Conditional Access to macOS Device Compliance – Jamf Pro Documentation***](https://learn.jamf.com/bundle/jamf-pro-documentation-current/page/Conditional_Access.html#ariaid-title6).
>
> If you need help, contact [***Jamf Customer Success***](https://jamf.service-now.com/csm). For more information, see the blog post at [**https://aka.ms/Intune/Jamf-Device-Compliance**](https://aka.ms/Intune/Jamf-Device-Compliance).

**This article can help you with the following tasks**:

- Configure the required components and configurations in Jamf Pro.
- Configure Jamf Pro to deploy the Intune Company Portal app to devices you manage with Jamf.
- Configure a policy to deploy to users through the Jamf self-service portal app to register devices with Microsoft Entra ID.
- Configure the Intune Connector.
- Prepare Microsoft Entra ID required components.

## Account permissions 

To complete the procedures in this article, you must have:

- A Jamf Pro user account with device compliance privileges or a Jamf Pro administrator account. 

- A Microsoft Entra account, assigned a role with sufficient permissions. Available built-in roles include:   

  - Intune Administrator - This role can perform all steps in this article. 

    >[!TIP]
    > The Intune Administrator is a highly privileged role with full access in Microsoft Intune. When you delegate roles to other accounts, consider assigning a built-in role with fewer privileges.
  
  - Groups Administrator - This role can create the required device groups.
    
  - Conditional Access Administrator - This role can create and update the Microsoft Entra Conditional Access policies that enable user-device registration. 
    
  - Application Administrator - This role can create apps that communicate with JAMF about the device compliance state.

  For more information about these roles, see [Microsoft Entra built-in roles](/entra/identity/role-based-access-control/permissions-reference).  

<a name='common-questions-about-jamf-pro-integration-with-entra-id'></a>

## Common questions about Jamf Pro integration with Microsoft Entra ID

**Why would integration with Microsoft Entra ID benefit our Jamf Pro managed devices?**

Microsoft Entra Conditional Access policies are able to require devices to not only meet compliance standards, but also register with Microsoft Entra ID. Organizations are seeking to continually improve their security posture by using Microsoft Entra Conditional Access policies to ensure the following example scenarios:

- Devices are registered with Microsoft Entra ID.
- Devices are using a known trusted location or IP address range.
- Devices are meeting the standards of compliance in order to access corporate resources using Microsoft 365 desktop applications and the browser.

**What's different about Microsoft Entra integration vs the Conditional Access method Jamf previously offered?**

For organizations that utilize Jamf Pro but haven't yet established a connection to Intune, the previous method that utilized the configuration in the Jamf Pro portal's **Settings > Global > Conditional Access** path is no longer able to accept new configurations.

New integrations require configurations under **Settings > Global > Device Compliance** and provide a wizard-based process to walk you through the connection to Intune. The wizard provides a method to create the required Microsoft Entra registered applications. These registered applications can't be precreated in this current design as they were previously.

## Jamf Pro administrative configurations

Jamf Pro configurations require the following *Computer smart groups* and *Computer policy* be created in the Jamf Pro console before establishing the connection to Intune.

### Computer smart groups

Create two computer smart groups using the following examples:

**Applicable**: Create a computer smart group containing criteria, which determines the devices that need access to company resources in the Microsoft tenant.

> **Example:** Go to *Jamf Pro* > *Computers* > *Smart Computer Groups* create a new group:
>
> - Display Name:
>   - In this article, we've named the group **Jamf-Intune Applicable Group**.
> - Criteria:
>   - Application Title, Operator = is, Value = CompanyPortal.app

**Compliance**: Create a second computer smart group containing criteria, which determines if devices are deemed compliant within Jamf and meet your organization's security standards.

> **Example:** Go to *Jamf Pro* > *Computers* > *Smart Computer Groups*, create another group:
>
> - Display Name:
>   - In this article, we've named the group **Jamf-Intune Compliance Group**.
>   - *Option to enable* **Send email notification on membership change**.
> - Criteria:
>   - Last Inventory Update, Operator = Less than x days ago, Value = 2
>   - **and** - Criteria: Application Title, Operator = is, Value = CompanyPortal.app
>   - **and** - *File Vault 2*, Operator = is, Value = All Partitions Encrypted

### Computer policy

Create one computer policy that includes the following configurations:

> **Example:** Go to *Jamf Pro* > *Computers* > *Policy*, create a new policy:
>
> - **Options** tab:
>   - **General**:
>     - Display Name - Give the policy a name. For example, *Register with Microsoft Entra ID(Microsoft Entra)*.
>     - Enabled - Check this box to enable the policy.
>   - **Microsoft Device Compliance**:
>     - Enable **Register computers with Microsoft Entra ID**.
>
> - **Scope** tab: Configure *Selected Deployment Targets* to **Add** the [**Applicable**](#computer-smart-groups) computer smart group created as part of the [*Jamf Pro administrative configurations*](#complete-the-administrative-configuration).
>
> - **Self Service** tab:
>   - Enable **Make the policy available in Self Service**.
>   - Set a display name.
>   - Set a button name.
>   - Provide a description.
>   - Enable **Ensure that users view the description**.
>   - Enable optional *Categories* as desired.
>
> - Select **Save**.

### Mac App

Create an app in **Mac Apps** Jamf App Catalog for the Microsoft Intune Company Portal that deploys to all devices. *Using the Jamf app catalog version makes it easy to keep the application current*.

> - Go to *Computers* > *Mac Apps*, and select **+New**.
> - Select **Jamf App Catalog**, and then select **Next**.
> - Search for *Microsoft Intune Company Portal* and select **add** next to the application.
> - Set *Target Group* to **All Managed Clients**.
> - Set *Distribution Method* to **Install Automatically**.
> - Enable **Install supporting configuration profiles**.
> - Enable the **Deploy** switch at the top right, and then select **Save**.

<a name='entra-id-administrative-configurations'></a>

## Microsoft Entra administrative configurations

The ability to register devices can be blocked due to the Conditional Access Policy configurations your organization has in place to secure corporate resources.

Use the following to create a group, containing users of Jamf managed devices, which will be used to scope the Intune connector in later steps.

1. Sign in to [https://entra.microsoft.com](https://entra.microsoft.com) with an account that has permissions to create groups and to create and edit Conditional Access policy.
1. Expand *Groups* > *All groups* > and select **New Group**.
1. Create a dynamic group with appropriate rules to include the applicable users that will register their Jamf managed devices with Microsoft Entra ID.

   > [!TIP]
   > We recommend use of a dynamic group, but you can also use a static group.

## Connect Jamf Pro to Intune

Jamf pro utilizes connectors in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), found at > *Tenant Administration* > *Connectors and tokens*. The process to connect Jamf Pro to Intune starts in the Jamf Pro administrative portal and utilizes a wizard that prompts for next steps.

1. Sign in to your Jamf Admin portal, example: [https://tenantname.jamfcloud.com](https://tenantname.jamfcloud.com).
1. Proceed to *Settings > Global > Device Compliance*.
1. Select **Edit**, and then enable the Platform macOS by checking the box.
1. In the *Compliance Group* drop down, select the computer smart group you created for [**Compliance**](#computer-smart-groups) in the previous section *Computer-smart-groups* of this article.
1. In the *Applicable Group* drop down, select the computer smart group you created for [**Applicable**](#computer-smart-groups) in the previous section *Computer-smart-groups* of this article.
1. Enable the Slider at the top right, and select **Save**.
1. Two Microsoft Authentication prompts are then presented. Each requires a Microsoft 365 Global Administrator to authenticate the prompt:
   - The first authentication prompt creates the *Cloud Connector for Device Compliance* application in Microsoft Entra ID.
   - The second authentication prompt creates the *User registration app for Device Compliance*.

   :::image type="content" source="./media/jamf-managed-device-compliance-with-entra-id/appregreqs-all.png" alt-text="Image showing prompts for permissions requested in the Microsoft Entra registered applications." lightbox="./media/jamf-managed-device-compliance-with-entra-id/appregreqs-all.png":::

1. A new browser tab opens to a Jamf Portal page with a **Configure Compliance Partner** dialog, and then select the button labeled **Open Microsoft Endpoint Manager**.

   :::image type="content" source="./media/jamf-managed-device-compliance-with-entra-id/jamf-create-connector-3a.png" alt-text="Image of the Jamf Configure Compliance Partner Open Microsoft Endpoint Manager button." lightbox="./media/jamf-managed-device-compliance-with-entra-id/jamf-create-connector-3a.png":::

1. A new browser tab opens the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Proceed to *Tenant administration > Connectors and tokens > Partner compliance management*.
1. At the top of the *Partner compliance management* page, select **Add compliance partner**.
1. In the *Create Compliance Partner* wizard:
   1. Use the *Compliance partner* drop-down to select **Jamf Device Compliance**.
   1. Use the *Platform* drop down to select **macOS**, and then select **Next**.
   1. In *Assignments*, select **Add Groups**, and then select the Microsoft Entra user group created earlier. **Do not** select *Add all users* as this will inhibit the connection.
   1. Select **Next**, and then **Create**.
1. In your browser, open the tab containing the Jamf Portal with the **Configure Compliance Partner** dialog.
1. Select the **Confirm** button.

   :::image type="content" source="./media/jamf-managed-device-compliance-with-entra-id/jamf-confirm-connector-a.png" alt-text="Image of the Jamf Configure Compliance Partner Confirm button." lightbox="./media/jamf-managed-device-compliance-with-entra-id/jamf-confirm-connector-a.png":::

1. Switch to the browser tab showing the Intune Partner compliance management dashboard and select the **Refresh** icon at the top next to the *Add compliance Partner* option.
1. Verify the macOS *Jamf Device Compliance* connector shows a Partner Status of **Active**.

   :::image type="content" source="./media/jamf-managed-device-compliance-with-entra-id/intune-confirm-connection-a.png" alt-text="Image of the Intune Connectors for Device Compliance Partner macOS active connection." lightbox="./media/jamf-managed-device-compliance-with-entra-id/intune-confirm-connection-a.png":::

### Complete the administrative configuration

To ensure users are able to enroll devices, you must be aware of the Microsoft Entra Conditional Access policies that might block them. The **User Registration app for Device Compliance** created when you [connected Jamf Pro to Intune](#connect-jamf-pro-to-intune) must be added as an exclusion in any policy that may prevent users from registering their devices.

For example, consider a Microsoft Entra Conditional Access policy that requires compliant devices:

> - *Assignments* - Assign this policy to all users or include groups of users that have Jamf Managed devices.
> - *Target resources* - Set the following configurations:
>   - Apply to all **Cloud apps**.
>   - Exclude the **User Registration app for Device Compliance** app. This app was created when you [connected Jamf Pro to Intune](#connect-jamf-pro-to-intune).
> - *Conditions* include the following options:
>   - Requires compliance
>   - Requires a registered device

:::image type="content" source="./media/jamf-managed-device-compliance-with-entra-id/entra-ca-user-app-exceptions-resize.png" alt-text="Image of the Microsoft Entra Conditional Access Policy exception for user application" lightbox="./media/jamf-managed-device-compliance-with-entra-id/entra-ca-user-app-exceptions-resize.png":::

## End user notifications

We recommend that you provide ample notification of the end user experience to ensure your users of Jamf managed devices are aware of the process, how it works, and a timeline in which they need to comply with policy. An important reminder that should be included in these notifications is that the Jamf Self-Service app contains the policy that they use to register their device. Users **must not** use the deployed Microsoft Company Portal App to attempt to register. Use of the Company Portal App results in an error indicating *AccountNotOnboarded*.

Devices managed with the Jamf platform don't show in Intune's device list in the following process. After users have registered their devices in Microsoft Entra ID, the initial state of the device shows as **Not Compliant**. Once the Jamf Pro computer smart group configured for **Compliance** is updated, the status is sent to through the Intune Connector to Microsoft Entra ID to update the devices compliance status. The frequency of updates to the Microsoft Entra device information is based on the Compliance computer smart group in Jamf frequency of change.

## Troubleshooting

### Issue

After the policy was launched from the Jamf Self-Service App on the macOS device as instructed, the Microsoft authentication prompt appeared to work normally. However, the status of the device shown in Microsoft Entra ID did not update from *N/A* to the *Compliant* state as expected, even after waiting one hour or more.

In this case, the device record in Microsoft Entra ID was incomplete.

### Resolution

First, Verify the following:

- The device is shown as a member of the Jamf computer smart group for Compliance. This membership indicates the device is compliant.
- The authenticating user is a member of the Microsoft Entra group that is scoped to the Jamf Intune connector.

Second, On the affected device:

- Open the Terminal application and execute the following command:

  `/usr/local/jamf/bin/jamfaad gatherAADInfo`

  - If the command does not result in a prompt, and instead returns Microsoft Entra ID acquired for macOS user $USER, then the registration was good.
  - If the command creates a sign in prompt, and the user is able to complete the sign in without error, there may have been a user error during the initial registration attempt.
  - If the command creates a sign in prompt but there is an error when the user signs in, further troubleshooting is required via a support case.

## Next steps

- [Apply compliance policies to Jamf-managed devices](../protect/conditional-access-assign-jamf.md)
- [Data Jamf sends to Intune](../protect/data-jamf-sends-to-intune.md)
