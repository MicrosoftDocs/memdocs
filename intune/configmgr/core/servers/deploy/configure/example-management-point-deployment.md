---
title: Example management point deployment in an untrusted domain
description: Follow a step-by-step example to learn how to install a Configuration Manager management point on a server in an untrusted Active Directory domain.
ms.date: 05/13/2026
ms.subservice: core-infra
ms.topic: install-set-up-deploy
ms.collection: tier3
---

# Step-by-step example deployment of a management point in an untrusted Active Directory domain

*Applies to: Configuration Manager (current branch)*

This step-by-step example shows you how to install a Configuration Manager management point (MP) on a server that resides in an Active Directory domain that has no two-way trust with the domain that contains the site server. This scenario is common when you want to extend management to a perimeter network (DMZ), a partner domain, or any other network segment that you can't fully trust.

Review your organization's network and Active Directory documentation for the procedures and best practices that apply to your environment. The steps in this article are appropriate as a proof-of-concept reference. For production guidance, see [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).

> [!NOTE]
> This scenario applies to a site system connected to a primary site only. Secondary sites require a two-way domain trust between the secondary site's domain and the parent primary site's domain. Installing a secondary site in a domain without the required trust is not supported.

## <a name="BKMK_mp_testenvironment"></a> Test environment

The step-by-step instructions in this article use the following test environment:

- **Trusted domain** (`corp.contoso.com`): Contains the Configuration Manager primary site server (`SiteServer`) and the SQL Server site database (`SQLServer`). The site code is **P01**.

- **Untrusted domain** (`branch.fabrikam.com`): Contains the server that will host the management point (`DMZ-MP`). There's no Active Directory trust of any kind between the two domains.

- Both domains have Windows Server DNS, and DNS conditional forwarders are configured in both directions so that FQDNs from each domain can be resolved from the other domain.

- You can sign in as a domain administrator in both domains to perform all procedures.

## <a name="BKMK_mp_overview"></a> Overview of the deployment steps

The following table summarizes what this example deployment covers and how each piece fits together.

| Step | What you do | Why it's required |
|------|-------------|-------------------|
| [Step 1](#BKMK_mp_step1) | Create service accounts in the untrusted domain | The site system installation account and the MP database connection account must exist in the domain where the MP server resides, or as global accounts resolvable from both domains. |
| [Step 2](#BKMK_mp_step2) | Grant SQL Server database permissions | The MP database connection account must have the permissions to read data in the site database so the management point can query client policy and inventory data. |
| [Step 3](#BKMK_mp_step3) | Configure firewall rules | Normally, all network traffic between the MP and the site server and site database must be explicitly permitted through firewalls. |
| [Step 4](#BKMK_mp_step4) | Install management point prerequisites on the site system server | Ensures that `DMZ-MP` has the Windows features and SQL connectivity components required before Configuration Manager installs the role. |
| [Step 5](#BKMK_mp_step5) | Install the management point role on DMZ-MP | Creates the site system server object and installs the management point role, using the accounts and settings prepared in earlier steps. |
| [Step 6](#BKMK_mp_step6) | Verify the management point installation | Confirms that the management point is healthy and that clients in the untrusted forest can communicate with it. |

## <a name="BKMK_mp_step1"></a> Step 1: Create domain accounts

Two dedicated user accounts are recommended. Configure both accounts with non-expiring passwords. Don't grant them any unnecessary privileges.

| Account | Domain | Purpose | Required permissions |
|---------|--------|---------|----------------------|
| `branch.fabrikam.com\svc-cm-dmzmpinstall` | Untrusted (`branch.fabrikam.com`) | **Site system installation account** — the site server uses this account to connect to `DMZ-MP` and install the management point role. | Member of the local **Administrators** group on `DMZ-MP`. |
| `corp.contoso.com\svc-cm-dmzmpdbconnect` | Trusted (`corp.contoso.com`) | **Management point connection account** — the management point uses this account to read and write data to the site database. | SQL Server login on `SQLServer` instance with the `smsdbrole_MP` and `smsdbrole_MPUserSvc` roles assigned in the SQL database of the site (granted in Step 2). |

### To create the site system installation account in the untrusted domain

1. Sign in to a domain controller in `branch.fabrikam.com` using a domain administrator account.

2. Open **Active Directory Users and Computers**.

3. In the navigation pane, expand **branch.fabrikam.com**, right-click the **Service Accounts** organizational unit (OU), and then choose **New** > **User**.

   > [!TIP]
   > If a dedicated Service Accounts OU doesn't exist, create one first or place the accounts in a suitable OU. Don't place service accounts in the default **Users** container in a production environment.

4. Complete the **New Object – User** wizard with the following settings, and then choose **Finish**:

   - **First name**: `svc-cm-dmzmpinstall`
   - **User logon name**: `svc-cm-dmzmpinstall`
   - **Password**: Use a strong, non-expiring password.
   - Select **Password never expires** and clear **User must change password at next logon**.

5. Close **Active Directory Users and Computers**.

### To create the MP database connection account in the trusted domain

1. Sign in to a domain controller in `corp.contoso.com` using a domain administrator account.

2. Open **Active Directory Users and Computers**.

3. In the navigation pane, expand **corp.contoso.com**, right-click the **Service Accounts** organizational unit (OU), and then choose **New** > **User**.

4. Complete the **New Object – User** wizard with the following settings, and then choose **Finish**:

   - **First name**: `svc-cm-dmzmpdbconnect`
   - **User logon name**: `svc-cm-dmzmpdbconnect`
   - **Password**: Use a strong, non-expiring password.
   - Select **Password never expires** and clear **User must change password at next logon**.

5. Close **Active Directory Users and Computers**.

### To add the installation account to the local Administrators group on DMZ-MP

1. Sign in to `DMZ-MP` using a local or domain administrator account.

2. Open **Computer Management**, expand **Local Users and Groups**, and then choose **Groups**.

3. Right-click **Administrators**, and then choose **Add to Group**.

4. In the **Administrators Properties** dialog box, choose **Add**.

5. In the **Select Users, Computers, Service Accounts or Groups** dialog box, enter `FABRIKAM\svc-cm-dmzmpinstall` in the object name box, choose **Check Names** to validate, and then choose **OK**.

6. Choose **OK** to close **Administrators Properties**.

## <a name="BKMK_mp_step2"></a> Step 2: Grant SQL Server database permissions for the MP connection account

The management point must be able to read and write data in the site database. You grant this access by adding the `svc-cm-dmzmpdbconnect` account as a SQL Server login and assigning it to the correct database roles.

> [!IMPORTANT]
> The MP database connection account must reside in the **trusted domain** (`corp.contoso.com`) because it connects to SQL Server (`SQLServer`) in that domain. Specify the account as a Windows login using the NetBIOS domain name `CORP\svc-cm-dmzmpdbconnect`. If name resolution fails, use the FQDN format `corp.contoso.com\svc-cm-dmzmpdbconnect`. For more information, see [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account).

### To create the SQL Server login and assign database roles

1. Sign in to `SQLServer` using a SQL Server administrator account, and open **SQL Server Management Studio**.

2. In **Object Explorer**, expand **Security**, right-click **Logins**, and then choose **New Login**.

3. In the **Login – New** dialog box, on the **General** page, complete the following settings:

   - **Login name**: Enter `CORP\svc-cm-dmzmpdbconnect`.
   - Select **Windows authentication**.

4. In the left pane of the **Login – New** dialog box, choose **User Mapping**.

5. In the **Users mapped to this login** list, select the check box next to the Configuration Manager site database (for example, **CM_P01**).

6. In the **Database role membership** section at the bottom of the page, select the following roles:

   - **smsdbrole_MP**
   - **smsdbrole_MPUserSvc**

7. Choose **OK** to create the login.

8. Close **SQL Server Management Studio**.

## <a name="BKMK_mp_step3"></a> Step 3: Configure firewall rules

The following table lists the minimum firewall rules required for this deployment. Configure these rules on all firewalls and host-based Windows Firewall profiles that sit between `corp.contoso.com` and `branch.fabrikam.com`.

| Source | Direction | Destination | Protocol | Port | Purpose |
|--------|-----------|-------------|----------|------|---------|
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 135 | RPC endpoint mapper |
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 49152–65535 | RPC dynamic ports |
| `SiteServer` (site server) | ↔ | `DMZ-MP` (management point) | TCP | 445 | SMB (file transfer) |
| `DMZ-MP` (management point) | → | `SQLServer` (site database) | TCP | 1433 | SQL Server (MP database connection) |

The below connections are required for the management point to authenticate to domain controllers in CORP forest and vice versa. The ports required for DNS resolution are not included.

| Source | Direction | Destination | Protocol | Port | Purpose |
|--------|-----------|-------------|----------|------|---------|
| `SiteServer` (site server) | → | `DC.branch.fabrikam.com` (BRANCH Domain Controller) | UDP | 389 | CLDAP |
| `SiteServer` (site server) | → | `DC.branch.fabrikam.com` (BRANCH Domain Controller) | TCP | 88 | Kerberos authentication |
| `DMZ-MP` (management point) | → | `DC.corp.contoso.com` (CORP Domain Controller) | UDP | 389 | CLDAP |
| `DMZ-MP` (management point) | → | `DC.corp.contoso.com` (CORP Domain Controller) | TCP | 88 | Kerberos authentication |

> [!TIP]
> If your SQL Server uses a named instance or a non-default port, update the SQL Server row in the table accordingly. For more information about all ports that Configuration Manager uses, see [Ports used in Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md).

## <a name="BKMK_mp_step4"></a> Step 4: Install management point prerequisites on DMZ-MP

Before you add the management point role, install the required Windows features and supporting components on `DMZ-MP`. For the complete and current list, see [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#management-point).

For this example, prepare `DMZ-MP` with the following components:

- **BITS** and **BITS Server Extensions**
- **Internet Information Services (IIS)** with the management point requirements, including **Windows Authentication**, **ISAPI Extensions**, **IIS 6 Metabase Compatibility**, and **IIS 6 WMI Compatibility**
- **.NET Framework 3.5** Windows feature
- A supported version of **.NET Framework**. Configuration Manager 2403 and later requires .NET Framework 4.8 or later for the management point to function properly. Windows Server 2022 and later have this version already installed.
- **Microsoft ODBC Driver for SQL Server**. Starting in version 2309, Configuration Manager requires this driver as a prerequisite. Use a currently supported version.

### To install the required Windows features on DMZ-MP

1. Sign in to `DMZ-MP` using a local or domain administrator account.

2. Open an elevated Windows PowerShell session.

3. Run the following command:

   ```powershell
   Install-WindowsFeature NET-Framework-Core, BITS, BITS-IIS-Ext, Web-Server, Web-Windows-Auth, Web-ISAPI-Ext, Web-Metabase, Web-WMI -IncludeManagementTools
   ```

4. If the server can't access the Windows installation source for `.NET Framework 3.5`, rerun the command with the `-Source` parameter and specify a valid `SxS` path from the Windows Server installation media.

5. Restart `DMZ-MP` if Windows prompts for a restart.

## <a name="BKMK_mp_step5"></a> Step 5: Install the management point role on DMZ-MP

This procedure installs the management point role on `DMZ-MP` by using the **Create Site System Server** wizard. The wizard lets you specify all the cross-forest accounts and settings that the role requires.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and then choose **Servers and Site System Roles**.

2. On the **Home** tab, in the **Create** group, choose **Create Site System Server**.

3. On the **General** page, complete the following settings, and then choose **Next**:

   - **Name**: Enter the FQDN of the management point server: `DMZ-MP.branch.fabrikam.com`.
   - **Site code**: Select **P01** (or the appropriate site code for your environment).
   - **Site system installation account**: Choose **Specify an account**, and then enter `FABRIKAM\svc-cm-dmzmpinstall`.

     > [!IMPORTANT]
     > You must specify a **Site System Installation Account** when the target server is in an untrusted forest. The site server can't use its own computer account to authenticate to a server in a forest without trust. For more information, see [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

4. On the **General** page, select **Require the site server to initiate connections to this site system**.

   > [!IMPORTANT]
   > `DMZ-MP` lacks permissions to connect back to the site server. With this option selected, all data transfers are initiated by the site server and use the same [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

5. On the **Proxy** page, configure a proxy server if `DMZ-MP` requires one to reach internet endpoints. Otherwise, choose **Next**.

6. On the **System Role Selection** page, select **Management point**, and then choose **Next**.

7. On the **Management Point** page, complete the following settings, and then choose **Next**:

   - **Client connections**: Choose **HTTPS** to require encrypted client communication (this requires a PKI web server certificate bound to the IIS Default Web Site on DMZ-MP) or EHTTP.
   - **Generate alert when the management point is not healthy**: Optionally select this to receive in-console alerts when the management point is unhealthy.
   - Leave other options at their default settings.

8. On the **Management Point Database Connection** page, complete the following settings, and then choose **Next**:

   - **Use the site database**: this is the default configuration. There is no need to specify the SQL Server instance since the site already has this information.
   - **Management point database connection**: Choose **Specify an account**, and then enter `corp.contoso.com\svc-cm-dmzmpdbconnect`. Use the FQDN format to ensure that the management point can resolve the account in the trusted domain and authenticate to SQL Server successfully.
     > [!IMPORTANT]
     > You must specify the **Management point connection account** when the management point is in an untrusted domain or forest because it authenticates directly to SQL Server in trusted domain. Specifying the account in the format `DomainFQDN\UserName` — for example, `corp.contoso.com\svc-cm-dmzmpdbconnect` — facilitates the name resolution for Kerberos authentication flow. For more information, see [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account).

9. Review the summary on the **Summary** page, and then choose **Next** to complete the wizard.

10. Choose **Close** on the **Completion** page.

   > [!NOTE]
   > After you close the wizard, Configuration Manager creates the site system server object and begins the background installation of the management point role on `DMZ-MP`. The installation can take several minutes to complete. Monitor the progress as described in Step 6.

## <a name="BKMK_mp_step6"></a> Step 6: Verify the management point installation

After the wizard finishes, verify that the management point installed successfully and is healthy before directing clients to it.

### To verify the management point status in the Configuration Manager console

1. In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and then choose **Component Status**.

2. Look for the **SMS_MP_CONTROL_MANAGER** component on `DMZ-MP.branch.fabrikam.com`. In the **Status** column, confirm that the status is **OK**.

   > [!NOTE]
   > It can take up to 30 minutes after the wizard closes for the management point to appear as healthy. If the status shows **Warning** or **Critical**, check the log files as described below.

3. In the **Administration** workspace, expand **Site Configuration** > **Servers and Site System Roles**, and then choose **DMZ-MP.branch.fabrikam.com**.

4. In the lower pane, confirm that the **Management point** role is listed and that the **Status** is **OK**.

### To verify the management point installation by reviewing log files

1. Sign in to `DMZ-MP` and locate the `SMS` folder at the root of one of the drives.

2. If the folder doesn't exist, investigate `SiteComp.log` on the site server to confirm that the site server managed to connect to `DMZ-MP` and start the installation under the [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). The absence of the `SMS` folder indicates that the site server can't communicate with `DMZ-MP` or doesn't have permissions to create the folder and install the role.

3. Investigate the following log files on `DMZ-MP` for messages related to the management point installation and configuration:

   | Log file | Location on DMZ-MP | What to look for |
   |----------|------------------|-----------------|
   | `MPSetup.log` | `\SMS\Logs` | High-level prerequisite and MP installation messages: in particular, `CcmSetup`, `msoledbsql.msi` and `mp.msi`. |
   | `MPMSI.log` | `\SMS\Logs` | Details on MP installation and absence of MSI rollback. If installation fails with error 1603, look up this error code in the middle of file to find the detailed error message. |
   | `CCMSetup.log` | `%Windir%\CCMSetup\Logs` | Client binaries installation messages and their own prerequisites (like vcredist and Microsoft Policy Platform). The installation must complete with the return code 0. |
   | `BGBSetup.log` | `\SMS\Logs` | Client Notification Server installation messages: look for successful completion. |

4. Once MP is installed, the `SMS_CCM` folder should appear at the same drive as `SMS`. This may not happen if the client was installed before the management point: in this case, look into `CCM\Logs` folder of the installed client. Investigate the following log files on `DMZ-MP` for messages related to the management point's communication with the site server and site database:

   | Log file | Location on DMZ-MP | What to look for |
   |----------|------------------|-----------------|
   | `MpControl.log` | `\SMS\Logs` | Regular Management Point and User Service availability checks. The successful check resembles `Call to HttpSendRequestSync succeeded for port 443 with status code 200, text: OK`. |
   | `BGBServer.log` | `\SMS\Logs` | Client Notification (fast channel) server reporting. The usual logging lists the number of connected clients, such as `Total online clients: 100 (TCP: 99 HTTP: 1)~~` |
   | `MPFDM.log` | `\SMS\Logs` | This log on MP should have no activity on `DMZ-MP` and display `Remote site is in pull-mode.` message. Contrary, same log on the Site Server should display file moving activity resembling the entries like `~Moved file...`. |
    | `MP_Framework.log` | `\SMS_CCM\Logs` | Database connection messages using the [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account) resembling `Loaded MP settings cache from reg key HKLM\Software\Microsoft\SMS\MP: Database Settings:`. If there are errors, look for messages about failed authentication or connectivity issues with SQL Server. |

### To test client communication with the new management point

1. On a client computer in `branch.fabrikam.com`, copy the client distro to any convenient location. Open an administrative command prompt in it, and run the following command to manually assign the client to the new management point:

   ```cmd
   ccmsetup.exe SMSSITECODE=P01 SMSMP=DMZ-MP.branch.fabrikam.com
   ```

   > [!NOTE]
   > In the case MP is configured to HTTPS, make sure the client has PKI client certificate enrolled and use `/UsePKICert` switch with `ccmsetup.exe`. For more information, see [About client installation properties](../../../clients/deploy/about-client-installation-properties.md).

2. Review `%Windir%\CCMSetup\Logs\CCMSetup.log` to confirm the successful installation.

3. Review `\SMS_CCM\Logs\ClientIDManagerStartup.log` to confirm successful registration of the client. Look for the messages resembling `[RegTask] - Client is registered. Server assigned ClientID is GUID:0B1F5036-9CE1-41A1-B417-063582728464. Approval status 1`.

4. Verify that the client appears in the Configuration Manager console and is displayed with "Online" icon. Add "Management Point" column to the console view to confirm that the client is assigned to `DMZ-MP.branch.fabrikam.com`.

## Next steps

- [Add site system roles](add-site-system-roles.md)
- [Install site system roles](install-site-system-roles.md)
- [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest)
- [Accounts used in Configuration Manager](../../../plan-design/hierarchy/accounts.md)
- [PKI certificate requirements for Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md)
