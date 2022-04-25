---
# required metadata

title: Use Intune compliance and Azure AD Conditional Access policies with Jamf Pro
titleSuffix: Microsoft Intune
description: Create Intune compliance policies and Azure AD Conditional Access to help secure Jamf-managed devices.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/19/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: c87fd2bd-7f53-4f1b-b985-c34f2d85a7bc

# optional metadata

#ROBOTS: 
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Enforce compliance on Macs managed with Jamf Pro

After you integrate Jamf Pro with Intune, configure Intune compliance policies and Azure Active Directory (Azure AD) Conditional Access policies to enforce compliance of macOS devices with your organizational requirements.

This article can help you with the following tasks:

- Create Conditional Access policies.
- Configure Jamf Pro to deploy the Intune Company Portal app to devices you manage with Jamf.
- Configure devices to register with Azure AD when the device user signs in to the Company Portal app they start from within the *Jamf Self Service* app. Device registration establishes an identity in Azure AD that allows the device to be evaluated by Conditional Access policies for access to company resources.

The procedures in this article require access to both the Intune and Jamf Pro consoles. Intune supports two methods to integrate Jamf Pro, which you configure separately from the procedures in this article:

- *Recommended* - [Use the Jamf Cloud Connector to integrate Jamf Pro with Intune](conditional-access-jamf-cloud-connector.md)
- [Manually configure integration of Jamf Pro with Intune](conditional-access-integrate-jamf.md)

After integration is configured, device users learn about Jamf Pro and Intune integration through either a communication from your IT department about how to register a device, or by discovering the Intune Company Portal app that you deploy through *Jamf Pro Self Service*. After device registration completes, inventory data collected by Jamf Pro for that device is shared with Intune. Information is shared for only those Mac devices that have completed.

## Set up device compliance policies in Intune

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Compliance policies**. If you're using a previously created policy, select that policy in the console and then go to the next step of this procedure. To create a new policy, select **Create Policy** and then specify details for a policy with a *Platform* of **macOS**. Configure *Settings* and *Actions for noncompliance* to meet your organizational requirements, and then select **Create** to save the policy.

3. On the policies *Overview* pane, select **Assignments**. Use the available options to configure which Azure Active Directory (Azure AD) users and security groups receive this policy. **Jamf integration with Intune doesn't support compliance policy that targets device groups.**

   > [!NOTE]
   > Jamf integration with Intune only supports Azure AD user groups. Device compliance policies that are targeted to device groups will not apply.

4. When you select **Save**, the policy deploys to the users.

Policies you deploy target the devices that are used by the assigned users. Those devices are evaluated for compliance. Compliant devices are marked as compliant for the setting "*Require device to be marked as compliant*" in Azure AD.  

> [!NOTE]
> Intune requires full disk encryption to be compliant.

## Deploy the Company Portal app for macOS in Jamf Pro

Create a policy in Jamf Pro to deploy the Intune Company Portal. This policy deploys the company portal app so that it's available in Jamf Self Service. Create this policy before you create policy in Jamf Pro for users to register devices with Azure AD.

To complete the following procedure, you need access to a macOS device and the Jamf Pro portal.

### To deploy the company portal app

1. On a macOS device, download but don't install the current version of the [Company Portal app for macOS](https://go.microsoft.com/fwlink/?linkid=862280). You only need a copy of the app so you can upload the app to Jamf Pro.

2. Open Jamf Pro and go to **Computer management** > **Packages**.

3. Create a new package with the Company Portal app for macOS, then select **Save**.

4. Open **Computers** > **Policies**, then select **New**.

5. Use the **General** payload to configure settings for the policy. These settings should be:
   - Trigger: select **Enrollment Complete** and **Recurring Check-in**
   - Execution Frequency: select **Once per computer**

6. Select the **Packages** payload and select **Configure**.

7. Select **Add** to select the package with the Company Portal app.

8. Select **Install** from the **Action** pop-up menu.

9. Configure the settings for the package.

10. Select the **Scope** tab to specify on which computers the Company Portal app should install. Select **Save**. The policy runs on scoped devices the next time the selected trigger occurs on the computer and the criteria in the **General** payload is met.

## Create a policy in Jamf Pro to have users register their devices with Azure Active Directory  

After you [deploy the Company Portal](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) for macOS through Jamf Pro Self-Service, you can create the Jamf Pro policy that registers a user's device with Azure AD.

Device registration requires a device user to manually select the Intune Company Portal app from within Jamf Self Service. We recommend you [contact your end users](../fundamentals/end-user-educate.md) through email, Jamf Pro notifications, or any other method your organization uses to direct them to complete this action to get their devices registered.

> [!WARNING]
> Launching the Company Portal app manually (such as from the Applications or Downloads folders) won't register the device. If device user launches the Company Portal manually, they'll see a warning, **'AccountNotOnboarded'**.

### To create the registration policy

1. In Jamf Pro, go to **Computers** > **Policies**, and then create a new policy for device registration.

2. Configure the **Microsoft Intune Integration** payload, including the trigger and execution frequency.

3. Select the **Scope** tab, and then scope the policy to all targeted devices.

4. Select the **Self Service** tab to make the policy available in Jamf Self Service. Include the policy in the **Device Compliance** category. Select **Save**.

## Validate Intune and Jamf integration

Use the Jamf Pro console to confirm that communication between Jamf Pro and Microsoft Intune is successful.

- In Jamf Pro, go to **Settings** > **Global Management** > **Microsoft Intune Integration**, and then select **Test**.

The console displays a message with the success or failure of the connection. Should the connection test from the Jamf Pro console fail, review the Jamf configuration.

## Removing a Jamf-managed device from Intune

To remove a Jamf-managed device, open the Microsoft Endpoint Manager admin center, and select **Devices** > **All devices**, select the device, and then select **Delete**.  Bulk device deletion can be enabled by selecting multiple devices and clicking **Delete**.

Get information on how to [remove a Jamf-managed device in the Jamf Pro docs](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). You can also file a support ticket with [Jamf support](https://www.jamf.com/support/) for more help.

## Next steps

- [Conditional Access in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)
- [Get started with Conditional Access in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)
