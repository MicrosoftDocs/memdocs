---
# required metadata

title: Set up device-based Conditional Access with Intune
titleSuffix: Microsoft Intune
description: Learn how to create a device-based Conditional Access policy based on Microsoft Intune device compliance and mobile app management.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/10/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create a device-based Conditional Access policy

With Intune, enhance Conditional Access in Azure Active Directory by adding mobile device compliance to the access controls. With Intune compliance policy that defines requirements for devices to be compliant, you can use a device's compliance status to either allow or block access to your apps and services. You can do this by creating a Conditional Access policy that uses the setting **Require device to be marked as compliant**.

A Conditional Access policy specifies the app or services you want to protect, the conditions under which the apps or services can be accessed, and the users the policy applies to. Although Conditional Access is an Azure AD premium feature, the Conditional Access node you access from *Intune* is the same node as accessed from *Azure AD*.

To Create a device-based Conditional Access policy your account must have one of the following permissions in Azure AD:

- Global administrator	
- Intune Service administrator	
- Conditional Access administrator	

> [!IMPORTANT]
> Before you set up Conditional Access, you'll need to set up Intune device compliance policies to evaluate devices based on whether they meet specific requirements. See [Get started with device compliance policies in Intune](device-compliance-get-started.md).

## Create Conditional Access policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Conditional Access** > **Policies** > **New policy**.
:::image type="content" source="./media/create-conditional-access-intune/create-ca.png" alt-text="Create a new Conditional Access policy":::

3. Under **Assignments**, select **Users and groups**.

4. On the **Include** tab, identify the users or groups that this Conditional Access policy applies to. Once you've chosen groups or users to include, use the **Exclude** tab if there are any users, roles, or groups you want to exclude from this policy.

   - **All users**: Select this option to apply the policy to all users and groups, including internal and guest users.

   - **Select users and groups**: Select this option and specify one or more of the following options:
  
     1. **All guest users**: Select this option to include or exclude external guest users (for example, partners, external collaborators)

     2. **Directory roles**: Select one or more Azure AD roles to include or exclude users who are assigned these roles.

     3. **Users and groups**: Select this option to search for and select individual users or groups you want include or exclude.

        > [!TIP]
        > Test the policy against a smaller group of users to make sure it works as expected.

5. Select **Done**.

6. Under **Assignments**, select **Cloud apps or actions**.

7. On the **Include** tab, use available options to identify the apps and services you want to protect with this Conditional Access policy. Then you can use the **Exclude** tab if there are any apps or services you want to exclude from this policy.

   - **All cloud apps**: Select this option to apply the policy to all apps.
     > [!IMPORTANT]
     > The Microsoft Azure Management app for access to the Azure portal, and the Microsoft Intune app are included in this list. Be sure to use the **Exclude** tab either here or in the **Users and groups** options to make sure you (or the users or groups you designate) are able to sign in to the Azure portal or Microsoft Endpoint Manager admin center.

   - **Select apps**: Select this option, choose **Select**, and then use the applications list to search for and select the apps or services you want to protect.

   When ready, select **Done**.

8. Under **Assignments**, select **Conditions**.

   - **Sign-in risk**: Select *Yes* to use Azure AD Identity Protection sign-in risk detection with this policy, and then choose the sign-in risk levels the policy should apply to.

   - **Device platforms**: On the **Include** tab, identify the device platforms you want to this Conditional Access policy to apply to. Use the **Exclude** tab to exclude platforms from this policy.

   - **Client apps**: Select *Yes* to specify if the policy should apply to browser apps, mobile apps, and desktop clients.

   - **Device state**: The Conditional Access policy will apply to all device states unless you choose Yes and specifically exclude the states Device Hybrid Azure AD joined or Device marked as compliant (or both).

     > [!TIP]
     > If you want to protect both **Modern authentication** clients and **Exchange ActiveSync clients**, create two separate Conditional Access policies, one for each client type. Although Exchange ActiveSync supports modern authentication, the only condition that is supported by Exchange ActiveSync is platform. Other conditions, including multi-factor authentication, are not supported. To effectively protect access to Exchange Online from Exchange ActiveSync, create a Conditional Access policy that specifies the cloud app Microsoft 365 Exchange Online and the client app Exchange ActiveSync with Apply policy only to supported platforms selected.

9. Select **Done**.

10. Under **Access controls**, select **Grant**. Configure what happens based on the conditions you've set up.  You can select from the following options:

    - **Block access**: The users specified in this policy will be denied access to the apps under the conditions you've specified.
    - **Grant access**: The users specified in this policy will be granted access, but you can require any of the following further actions:
      - **Require multi-factor authentication**: The user will need to complete additional security requirements, like a phone call or text.
      - **Require device to be marked as compliant**: The device must be Intune compliant. If the device is noncompliant, the user will be given the option to enroll the device in Intune.
      - **Require Hybrid Azure AD joined device**: Devices must be Hybrid Azure AD joined.
      - **Require approved client app**: The device must use approved client apps. 
      - **For multiple controls**: Select **Require all the selected controls** so that all of the requirements are enforced when a device attempts to access the app.
      
      :::image type="content" source="./media/create-conditional-access-intune/create-ca-grant-access-settings.png" alt-text="Access controls Grant settings":::

11. Under **Enable policy**, select **On**.

12. Select **Create**.

## Next steps

[App-based Conditional Access with Intune](app-based-conditional-access-intune.md)

[Troubleshooting Intune Conditional Access](https://support.microsoft.com/help/4456106)
