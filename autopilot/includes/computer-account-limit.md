---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: madakeva
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 01/31/2025
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

user-driven/hybrid-azure-ad-join-computer-account-limit.md
pre-provisioning/hybrid-azure-ad-join-computer-account-limit.md

Headings are driven by article context. -->

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Updated Connector**](#tab/updated-connector)

    > [!IMPORTANT]
    >
    > This step is only needed under one of the following conditions:
    >
    > - The administrator that installed and configured the Intune Connector for Active Directory didn't have appropriate rights to set permissions on the **Computer** container or on OUs in the domain.
    > - The `ODJConnectorEnrollmentWiazard.exe.config` XML file wasn't modified to add OUs that the MSA should have permissions for.

Since the purpose of Intune Connector for Active Directory is to join computers to a domain and add them to an OU, the [Managed Service Account (MSA)](/windows-server/identity/ad-ds/manage/understand-service-accounts#standalone-managed-service-accounts) being used for the Intune Connector for Active Directory needs to have permissions to create computer accounts in the OU where the computers are joined to the on-premises domain.

With default permissions in Active Directory, domain joins by the Intune Connector for Active Directory might initially work without any permission modifications to the OU in Active Directory. However after MSA attempts to join more than 10 computers to the on-premises domain, it would stop working because by default, Active Directory only allows any single account to join up to 10 computers to the on-premises domain.

The following users aren't restricted by the 10 computer domain join limitation:

- Users in the Administrators or Domain Administrators groups: In order to comply with the least privilege principles model, it's not recommended to make the MSA an administrator or domain administrator.
- Users with delegated permissions on Organizational Unit (OUs) and containers in Active Directory to create computer accounts: This method is recommended since it follows the least privilege principles model.

To fix this limitation, the MSA needs the **Create computer accounts** permission in the Organizational Unit (OU) where the computers are joined to in the on-premises domain. The Intune Connector for Active Directory will properly set the permissions for the MSAs to the OUs as long as one of the following conditions is met:

- The administrator installing the Intune Connector for Active Directory has the necessary permissions to set permissions on the OUs.
- The administrator configuring the Intune Connector for Active Directory has the necessary permissions to set permissions on the OUs.

If the administrator installing or configuring the Intune Connector for Active Directory doesn't have the necessary permissions to set permissions on the OUs, then the following steps need to be followed by an administrator that has the necessary permissions to set permissions on the OUs:

To increase the computer account limit in the Organizational Unit (OU) that computers are joining to during Autopilot, follow these steps :

1. On a computer that has access to the **Active Directory Users and Computers** console, open the **Active Directory Users and Computers** console by running **DSA.msc**.

1. Expand the desired domain and navigate to the organizational unit (OU) that computers are joining to during Autopilot.

    > [!NOTE]
    >
    > The OU that computers join during the Windows Autopilot deployment is specified later during the **Configure and assign domain join profile** step.

1. Right-click on the OU and select **Properties**.

    > [!NOTE]
    >
    > If computers are joining the default **Computers** container instead of an OU, right-click on the **Computers** container and select **Delegate Control**.

1. In the OU **Properties** windows that opens, select the **Security** tab.

1. In the **Security** tab, select **Advanced**.

1. In the **Advanced Security Settings** window, select **Add**.

1. In the **Permission Entry** windows, next to **Principal**, select the **Select a principal** link.

1. In the **Select User, Computer, Service Account, or Group** window, select the **Object Types...** button.

1. In the **Object Types** window, select the **Service Accounts** check box, and then select **OK**.

1. In the **Select User, Computer, Service Account, or Group** window, under **Enter the object name to select**, enter the name of the MSA being used for the Intune Connector for Active Directory.

    > [!TIP]
    >
    > The MSA was created during the **Install the Intune Connector for Active Directory** step/section and has the name format of `msaODJ#####` where **#####** are five random characters. If the MSA name isn't known, follow these steps to find the MSA name:
    >
    > 1. On the server running the Intune Connector for Active Directory, right-click on the **Start** menu and then select **Computer Management**.
    > 1. In the **Computer Management** window, expand **Services and Applications** and then select **Services**.
    > 1. In the results pane, locate the service with the name **Intune ODJConnector for Active Service**. The name of the MSA is listed in the **Log On As** column.

1. Select **Check Names** to validate the MSA name entry. Once the entry is validated, select **OK**.

1. In the **Permission Entry** windows, select the **Applies to:** drop-down menu and then select **This object only**.

1. Under **Permissions**, unselect all items, and then only select the **Create Computer objects** check box.

1. Select **OK** to close the **Permission Entry** window.

1. In the **Advanced Security Settings** window, select either **Apply** or **OK** to apply the changes.

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Legacy Connector**](#tab/legacy-connector)

Since the purpose of Intune Connector for Active Directory is to join computers to a domain and add them to an OU, the server running the Intune Connector for Active Directory needs to have permissions to create computer accounts in the OU where the computers are joined to the on-premises domain.

With default permissions in Active Directory, domain joins by the Intune Connector for Active Directory might initially work without any permission modifications to the OU in Active Directory. However after the server running the Intune Connector for Active Directory attempts to join more than 10 computers to the on-premises domain, it would stop working because by default, Active Directory only allows any single account to join up to 10 computers to the on-premises domain.

The following users aren't restricted by the 10 computer domain join limitation:

- Users in the Administrators or Domain Administrators groups - in order to comply with the least privilege principles model, it's not recommended to make the computer account running the Intune Connector for Active Directory an administrator or domain administrator.
- Users with delegated permissions on Organizational Unit (OUs) and containers in Active Directory to create computer accounts - this method is recommended since it follows the least privilege principles model.

To fix this limitation, the server running the Intune Connector for Active Directory needs the **Create computer accounts** permission in the Organizational Unit (OU) where the computers are joined to in the on-premises domain:

To increase the computer account limit in the Organizational Unit (OU) that computers are joining to during Autopilot, follow these steps on a computer that has access to the **Active Directory Users and Computers** console:

1. Open the **Active Directory Users and Computers** console by running **DSA.msc**.

1. Expand the desired domain and navigate to the organizational unit (OU) that computers are joining to during Autopilot.

    > [!NOTE]
    >
    > The OU that computers join during the Windows Autopilot deployment is specified later during the **Configure and assign domain join profile** step.

1. Right-click on the OU and select **Delegate Control**.

    > [!NOTE]
    >
    > If computers are joining the default **Computers** container instead of an OU, right-click on the **Computers** container and select **Delegate Control**.

1. In the **Welcome to the Delegation of Control Wizard** window of the **Delegation of Control Wizard**, select **Next**.

1. In the **Users or Groups** window, under **Selected users and groups**, select **Add**.

1. Next to **Select this object type:** in the **Select Users, Computers, or Groups** window, select **Object Types**.

1. In the **Object Types** window, select the **Computers** check box, and then select **OK**. The other items in this window can be left at their default.

1. In the **Select Users, Computers, or Groups** window, under the **Enter the object names to select** box, enter the name of the computer where the Intune Connector for Active Directory was installed during the **Install the Intune Connector** step.

1. Select **Check Names** to validate the entry. Once the entry is validated, select **OK**.

1. In the **Users or Groups** window, verify that the correct computer is shown under **Selected users and groups:**, and then select **Next**.

1. In the **Tasks to Delegate** window, select **Create a custom task to delegate**, and then select **Next**.

1. In the **Active Directory Object Type** window:

    1. Select **Only the following objects in the folder**.

    1. Under **Only the following objects in the folder**, select **Computer objects**.

    1. Select the **Create selected objects in this folder** checkbox.

    1. Select **Next**.

1. In the **Permissions** window, under **Permissions:**, select the **Full Control** check box, and then select **Next**.

    > [!NOTE]
    >
    > After selecting the **Full Control** check box, all other options under **Permissions:** are automatically selected. The automatic selection of the checkboxes is normal and expected. Don't unselect any of the check boxes after they're automatically selected.

1. In the **Completing the Delegation of Control Wizard** window, select **Finish**.

---
