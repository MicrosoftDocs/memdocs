---
title: Windows Autopilot user-driven hybrid Azure AD join with pre-provisioning - Step 8 of 10 - Create and assign a domain join profile
description: How to - Windows Autopilot hybrid user-driven Azure AD join - Step 8 of 10 - Create and assign a domain join profile.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 03/27/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# User-driven hybrid Azure AD join: Create and assign a domain join profile

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
> [!div class="checklist"]
> - **Step 8: Configure and assign domain join profile**

For an overview of the Windows Autopilot user-driven hybrid Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

## Create and assign a domain join profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **Policy**, select **Configuration Profiles**.

1. In the **Devices | Configuration profiles** screen, make sure **Profiles** is selected at the top, and then select **Create profile**.

1. In the **Create profile** window that opens:

   1. Under **Platform**, select **Windows 10 and later**.

   1. Under **Profile type**, select **Templates**.

   1. When the templates appear, under **Template name**, select **Domain join**. If **Domain join** isn't visible, scroll through the **Template name** list until **Domain join** is visible. The list is in alphabetical order.

   1. Select **Create** to close the **Create profile** window.

1. The **Create profile** screen opens. In the **Basics** page:

   1. Next to **Name**, enter a name for the domain join profile.

   1. Next to **Description**, enter a description for the domain join profile.

   1. Select **Next**.

1. In the **Configuration settings** page:

   1. Next to **computer name prefix**, enter a prefix for computer names. This field is required. This prefix is used on all computer names. The rest of the computer name after the prefix is randomly generated up to 15 characters.

        > [!NOTE]
        >
        > This field doesn't support the **%SERIAL%** or **%RAND:x%** variables that can be used with the **Apply device name template** in the Azure AD join scenario.

   1. Next to **Domain name**, enter the FQDN of the domain that the device will join. This field is required. Make sure to specify the FQDN of the domain and not the NETBIOS name of the domain. For example, enter in **contoso.com** and not just **CONTOSO**.

   1. Next to **Organizational unit**, enter the full path to the Organizational Unit (OU) in the domain that the computer accounts should be created in. For example, **OU=OU-Name,DC=contoso,DC=com**. This field is optional. If the OU isn't specified, the computer accounts are created in the **Computer** container.

        > [!NOTE]
        >
        > The OU specified in this step should be the same OU that permissions were set for and computer account limits increased in the step [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md). Make sure that this step has been followed for the OU specified in this field. Skipping the step that sets permissions correctly on the OU wil result in computers failing to join the domain.

        > [!IMPORTANT]
        >
        > If computers will be joining the **Computers** container, leave this field blank. Don't specify the **Computers** container in this field via **CN=Computers,DC=contoso,DC=com**. The **Computers** container is a container and not an OU. When no OU is specified in this field and it is left blank, devices will automatically join the **Computers** container. If the **Computers** container is specified, it will cause domain joins to fail.

   1. Once the settings in the **Configuration settings** page are complete, select **Next**.

1. In the **Assignments** page:

   1. Under **Included groups**, choose **Add groups**.

      > [!NOTE]
      >
      > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups under **Excluded groups** will result in those devices being excluded and they won't receive the configuration profile.

   1. In the **Select groups to include** window that opens, select the groups that the configuration profile should be assigned to. This device group(s) is normally the device group(s) created in the step [Create device group](azure-ad-join-device-group.md). Once done, select **Select**.

   1. Under **Included groups** > **Groups**, ensure the correct group(s) are selected, and then select **Next**.

1. In the **Applicability Rules** page, select **Next**. For this tutorial, applicability rules are being skipped. However if applicability rules are needed, do so at this screen. For more information about scope tags, see [Applicability rules](/mem/intune/configuration/device-profile-create#applicability-rules).

1. In the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the domain join profile.

## More information

For more information on domain join profiles, see the following article(s):

- [Create and assign a Domain Join profile](/mem/autopilot/windows-autopilot-hybrid#create-and-assign-a-domain-join-profile)
