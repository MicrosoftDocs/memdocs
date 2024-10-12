---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/19/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

user-driven/hybrid-azure-ad-join-computer-account-limit.md
pre-provisioning/hybrid-azure-ad-join-computer-account-limit.md

Headings are driven by article context. -->

The purpose of the Intune connector is to join computers to an on-premises domain during the Autopilot process. The Intune connector creates computer objects in a specified Organizational Unit (OU) in Active Directory during the domain join process. For this reason, the server running the Intune connector needs to have permissions to create and delete computer accounts in the OU where the computers are joined to the on-premises domain.

With default permissions in Active Directory, domain joins by the Intune connector might initially work without any permission modifications to the OU in Active Directory. However after the server running the Intune connector attempts to join more than 10 computers to the on-premises domain, it would stop working because by default, Active Directory only allows any single account to join up to 10 computers to the on-premises domain.

The following users aren't restricted by the 10 computer domain join limitation:

- Users in the Administrators or Domain Administrators groups.
- Users with delegated permissions on Organizational Unit (OUs) and containers in Active Directory to create and delete computer accounts.

To fix this limitation, the server running the Intune connector needs to be delegated permissions in the Organizational Unit (OU) where the computers are joined to the on-premises domain to:

- Create computer accounts.
- Delete computer accounts.

Microsoft also recommends to specifically set these permissions in case the server running the Intune connector doesn't have permissions to create computers in the OU, for example, the default permissions are modified.

To increase the computer account limit in the Organizational Unit (OU) that computers are joining to during Autopilot, follow these steps on a computer that has access to the **Active Directory Users and Computers** console:

1. Open the **Active Directory Users and Computers** console by running **DSA.msc**.

1. Expand the desired domain and navigate to the organizational unit (OU) that computers are joining to during Autopilot.

    > [!NOTE]
    >
    > The OU that computers join during the Windows Autopilot deployment is specified later during the **Configure and assign domain join profile** step.

1. Right-click on the OU and select **Delegate Control**.

    > [!NOTE]
    >
    > If an OU isn't being specified and computers instead join the default **Computers** container, right-click on the **Computers** container and select **Delegate Control**.

1. In the **Welcome to the Delegation of Control Wizard** window of the **Delegation of Control Wizard**, select **Next**.

1. In the **Users or Groups** window, under **Selected users and groups**, select **Add**.

1. Next to **Select this object type:** in the **Select Users, Computers, or Groups** window, select **Object Types**.

1. In the **Object Types** window, select the **Computers** check box, and then select **OK**. The other items in this window can be left at their default.

1. In the **Select Users, Computers, or Groups** window, under the **Enter the object names to select** box, enter the name of the computer where the Intune connector was installed during the **Install the Intune Connector** step.

1. Select **Check Names** to validate the entry. Once the entry is validated, select **OK**.

1. In the **Users or Groups** window, verify that the correct computer is shown under **Selected users and groups:**, and then select **Next**.

1. In the **Tasks to Delegate** window, select **Create a custom task to delegate**, and then select **Next**.

1. In the **Active Directory Object Type** window:

    1. Select **Only the following objects in the folder**.

    1. Under **Only the following objects in the folder**, select **Computer objects**.

    1. Select both the **Create selected objects in this folder** and **Delete selected objects in this folder** check boxes.

    1. Select **Next**.

1. In the **Permissions** window, under **Permissions:**, select the **Full Control** check box, and then select **Next**.

    > [!NOTE]
    >
    > After selecting the **Full Control** check box, all other options under **Permissions:** are automatically selected. The automatic selection of the checkboxes is normal and expected. Don't unselect any of the check boxes after they're automatically selected.

1. In the **Completing the Delegation of Control Wizard** window, select **Finish**.
