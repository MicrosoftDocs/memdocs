---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 8 of 8 - Create and assign a domain join profile
description: How to - Windows Autopilot hybrid user-driven Azure AD join - Step 8 of 8 - Create and assign a domain join profile.
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
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

2. In the **Home** screen, select **Devices**.

3. In the **Devices | Overview** screen, under **Policy**, select **Configuration profiles**.

4. In the **Devices | Configuration profiles** screen, select **Create profile**.

5. In the **Create profile** screen:

   1. Under **Platform**, select **Windows 10 and later**.

   2. Under **Profile type**, select **Templates**.

   3. Once **Templates** is selected, additional options will appear. Under **Template name**, select **Domain join**, and then select **Create**. If necessary, scroll through the **Template name** list until **Domain join** is visible. The list is in alphabetical order.

6. In the **Basics** page of the **Domain Join*** screen, type a **Name** and optional **Description** for the domain join profile, and then select **Next**.

7. In the **Configuration settings** page:

   1. Next to **computer name prefix**, enter a prefix for computer names. This field is required. This prefix will be used on all computer names. The rest of the computer name after the prefix will be randomly generated up to 15 characters.

        > [!NOTE]
        >
        > This field doesn't support the **%SERIAL%** or **%RAND:x%** variables that can be used with the **Apply device name template** in the Azure AD join scenario.

   2. Next to **Domain name**, enter the FQDN of the domain that the device will be joined to. This field is required. Make sure to specify the FQDN of the domain and not the NETBIOS name of the domain. For example, enter in **contoso.com** and not just **CONTOSO**.

   3. Next to **Organizational unit**, enter the full path to the Organizational Unit (OU) in the domain that the computer accounts should be created in. This field is optional. For example, **OU=OU-Name,DC=contoso,DC=com**. If the OU isn't specified, the computer accounts will be created in the **Computer** container.

        > [!NOTE]
        >
        > The OU specified in this step should be the same OU that permissions were set for and computer account limits increased in the step [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md). Make sure that this step has been followed for the OU specified in this field. Omitting setting permissions correctly on the OU wil result in computers failing to join the domain.

        > [!IMPORTANT]
        >
        > If computers will be joining the **Computers** container, leave this field blank. Don't specify the **Computers** container in this field via **CN=Computers,DC=contoso,DC=com**. The **Computers** container is a container and not an OU. When no OU is specified in this field and it is left blank, devices will automatically join the **Computers** container. If the **Computers** container is specified, it will cause domain joins to fail.

8. Once the settings in the **Configuration settings** page are complete, select **Next**.

9. On the **Assignments** page, under **Included groups**, choose **Add groups**.

10. In the **Select groups to include** page, choose the device group(s) to assign this Autopilot profile to. This device group(s) is normally the device group(s) created in the step [Create device group](hybrid-azure-ad-join-device-group.md). Once done, select **Select**.

    > [!NOTE]
    >
    > Make sure to add the correct device groups under **Included groups** and not under **Excluded groups**. Accidentally adding the desired device groups to assign the Autopilot profile to under **Excluded groups** will result in those devices being excluded and they won't receive the Autopilot profile.

11. In the **Assignments** page, verify the correct device group(s) appear under **Included groups** > **Groups**, and then select **Next**.

12. In the **Applicability Rules** page, select **Next**. No configuration is needed in this page.

13. On the **Review + Create** page, review and verify that all of the settings are set as desired, and then choose **Create** to create the domain join profile.

## More information

For more information on domain join profiles, see the following article(s):

- [Create and assign a Domain Join profile](/mem/autopilot/windows-autopilot-hybrid#create-and-assign-a-domain-join-profile)
