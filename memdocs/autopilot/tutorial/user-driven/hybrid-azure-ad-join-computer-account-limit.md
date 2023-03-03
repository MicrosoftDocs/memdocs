---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 3 of 8 - Increase the computer account limit in the Organizational Unit (OU)
description: How to - Windows Autopilot hybrid user-driven Azure AD join - Step 3 of 8 - Increase the computer account limit in the Organizational Unit (OU).
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

# User-driven hybrid Azure AD join: Increase the computer account limit in the Organizational Unit (OU)

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
- Step 2: [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md)
> [!div class="checklist"]
> - Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)

For an overview of the Windows Autopilot hybrid user-driven Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

## Increase the computer account limit in the Organizational Unit (OU)

The purpose of the Intune connector is to join computers to an on-premise domain during the Autopilot process. The computers would be joined to the on-premise domain by the computer account of the server where the Intune connector is installed. With default permissions in Active Directory, this would initially work without any modifications. However after the server running the Intune connector attempts to join more than 10 computers to the on-premise domain, it would stop working. It would stop working because by default, Active Directory only allows any single account to join up to computers to the on-premise domain. Only accounts that are part of the Administrator or Domain Administrators groups can join more than 10 computers to the on-premise domain.

The following users aren't restricted by this 10 computer domain join limitation:

- Users in the Administrators or Domain Administrators groups.
- Users who have delegated permissions on Organizational Unit (OUs) and containers in Active Directory to create and delete computer accounts.

To fix this limitation, the server running the Intune connector needs to be delegated permissions to create and delete computer accounts in the Organizational Unit (OU) where the computers will be joined to the on-premise domain. It is also recommended to specifically set these permissions in case the server running the Intune connector doesn't have permissions to create computers in the OU, for example the default permissions have been modified.

To increase the computer account limit in the Organizational Unit (OU) that computers will be joining to during Autopilot, follow these steps:

1. Open the **Active Directory Users and Computers** console by running **DSA.msc**.

2. Expand the desired domain and navigate to the organizational unit (OU) that computers will be joining to during Autopilot.

    > [!NOTE]
    >
    > The OU that computers will be joining during Autopilot will be specified later during the [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md) step.

3. Right-click on the OU and select **Delegate Control**.

    > [!NOTE]
    >
    > If computers will be joining the **Computers** container, right click on the **Computers** container and select **Delegate Control**.

4. In the **Welcome to the Delegation of Control Wizard** window of the **Delegation of Control Wizard**, select **Next**.

5. In the **Users or Groups** window, under **Selected users and groups**, select **Add**.

6. Next to **Select this object type:** in the **Select Users, Computers, or Groups** window, select **Object Types**.

7. In the **Object Types** window, select the **Computers** check box, and then select **OK**. The other items in this window can be left at their default.

8. In the **Select Users, Computers, or Groups** window, in the **Enter the object names to select** box, enter the name of the computer where the Intune connector was installed during the [Install the Intune Connector](hybrid-azure-ad-join-intune-connector.md) step.

9. Select **Check Names** to validate your entry. Once the entry is validated, select **OK**.

10. In the **Users or Groups** window, select **Next**.

11. In the **Task to Delegate** window, select **Create a custom task to delegate**, and then select **Next**.

12. In the **Active Directory Object Type** window:

    1. Select **Only the following objects in the folder**.
    2. Under **Only the following objects in the folder**, select **Computer objects**.
    3. Select both the **Create selected objects in this folder** and **Delete selected objects in this folder** check boxes.
    4. Select **Next**.

13. In the **Permissions** window, under **Permissions:**, select the **Full Control** check box, and then select **Next**.

    > [!NOTE]
    >
    > After selecting the **Full Control** check box, all other options under **Permissions:** will be automatically selected. This is normal and expected. Do not unselect any of the check boxes after they have been automatically checked.

14. In the **Completing the Delegation of Control Wizard** window, select **Finish**.

## Next step: Register devices as Autopilot devices

> [!div class="nextstepaction"]
> [Step 4: Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)

## More information

For more information on increasing the computer account limit in an Organizational Unit, see the following article(s):

- [Increase the computer account limit in the Organizational Unit](/mem/autopilot/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit)
- [Default limit to number of workstations a user can join to the domain](/troubleshoot/windows-server/identity/default-workstation-numbers-join-domain)
- [Add workstations to domain](/windows/security/threat-protection/security-policy-settings/add-workstations-to-domain)
