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

Because there's no single method to deploy site system roles across trust boundaries, review your organization's network and Active Directory documentation for the procedures and best practices that apply to your environment. The steps in this article are appropriate as a proof-of-concept reference. For production guidance, see [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).

> [!NOTE]
> This scenario applies to a site system connected to a primary site only. Secondary sites require a two-way domain trust between the secondary site's domain and the parent primary site's domain. Installing a secondary site in a domain without the required trust is not supported.

## <a name="BKMK_mp_testnetwork"></a> Test network requirements

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
| [Step 2](#BKMK_mp_step2) | Grant SQL Server database permissions | The MP database connection account must have the `db_datareader` role in the site database so the management point can query client policy and inventory data. |
| [Step 3](#BKMK_mp_step3) | Configure firewall rules | When there's no forest trust, all network traffic between the MP and the site server and site database must be explicitly permitted through firewalls. |
| [Step 4](#BKMK_mp_step4) | Install the management point from the Configuration Manager console | Creates the site system server object and installs the management point role, using the accounts and settings prepared in earlier steps. |
| [Step 5](#BKMK_mp_step5) | Verify the management point installation | Confirms that the management point is healthy and that clients in the untrusted forest can communicate with it. |

## <a name="BKMK_mp_step1"></a> Step 1: Create domain accounts

Two dedicated user accounts are recommended. Configure both accounts with non-expiring passwords. Don't grant them any unnecessary privileges.

| Account | Domain | Purpose | Required permissions |
|---------|--------|---------|----------------------|
| `branch.fabrikam.com\svc-cm-dmzmpinstall` | Untrusted (`branch.fabrikam.com`) | **Site system installation account** — the site server uses this account to connect to `DMZ-MP` and install the management point role. | Member of the local **Administrators** group on `DMZ-MP`. |
| `corp.contoso.com\svc-cm-dmzmpdbconnect` | Trusted (`corp.contoso.com`) | **Management point connection account** — the management point uses this account to read and write data to the site database. | SQL Server login on `SQLServer` with the `db_datareader`  roles in the site database (granted in Step 2). |

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

   - **db_datareader**

   > [!NOTE]
   > Configuration Manager also adds the account to the `smsschm_users` role automatically when the management point role is first installed. If the role isn't added automatically, you can add it manually by expanding **Databases** > **CM_P01** > **Security** > **Roles** > **Database Roles** > **smsschm_users**, and then adding `CORP\svc-cm-dmzmpdbconnect` as a member.

7. Choose **OK** to create the login.

8. Close **SQL Server Management Studio**.

## <a name="BKMK_mp_step3"></a> Step 3: Configure firewall rules

When a management point is in an untrusted forest, all communication between the site server and the management point must be explicitly permitted. Configuration Manager requires the site server to initiate all connections to the management point when there's no forest trust, so firewall rules must allow inbound traffic to the management point from the site server's IP address.

The following table lists the minimum firewall rules required for this deployment. Configure these rules on all firewalls and host-based Windows Firewall profiles that sit between `corp.contoso.com` and `branch.fabrikam.com`.

| Source | Direction | Destination | Protocol | Port | Purpose |
|--------|-----------|-------------|----------|------|---------|
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 135 | RPC endpoint mapper (site server-initiated transfers) |
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 49152–65535 | RPC dynamic ports (site server-initiated) |
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

## <a name="BKMK_mp_step4"></a> Step 4: Install the management point

This procedure installs the management point role on `DMZ-MP` by using the **Create Site System Server** wizard. The wizard lets you specify all the cross-forest accounts and settings that the role requires.

### To install the management point role on DMZ-MP

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
   > This setting prevents `DMZ-MP` from initiating connections back to the site server, which would be blocked by the forest boundary and firewall. With this option selected, all data transfers are initiated by the site server. This is required for management points in untrusted forests.

5. On the **Proxy** page, configure a proxy server if `DMZ-MP` requires one to reach internet endpoints. Otherwise, choose **Next**.

6. On the **System Role Selection** page, select **Management point**, and then choose **Next**.

7. On the **Management Point** page, complete the following settings, and then choose **Next**:

   - **Client connections**: Choose **HTTPS** to require encrypted client communication. (This requires a PKI web server certificate bound to the IIS Default Web Site on DMZ-MP.)
   - **Allow mobile devices and Mac computers to use this management point**: Select this option only if you manage those device types.
   - **Management point database connection**: Choose **Specify an account**, and then enter `CORP\svc-cm-dmzmpdbconnect`.

     > [!IMPORTANT]
     > You must specify the **Management point connection account** when the management point is in an untrusted domain or forest. This account must reside in the **trusted domain** (`corp.contoso.com`) because it authenticates directly to SQL Server in that domain. Specify the account in the format `DomainFQDN\UserName`—for example, `corp.contoso.com\svc-cm-dmzmpdbconnect`—to ensure Kerberos authentication succeeds across the domain boundary. For more information, see [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account).

8. Review the summary on the **Summary** page, and then choose **Next** to complete the wizard.

9. Choose **Close** on the **Completion** page.

   > [!NOTE]
   > After you close the wizard, Configuration Manager creates the site system server object and begins the background installation of the management point role on `DMZ-MP`. The installation can take several minutes to complete. Monitor the progress as described in Step 5.

## <a name="BKMK_mp_step5"></a> Step 5: Verify the management point installation

After the wizard finishes, verify that the management point installed successfully and is healthy before directing clients to it.

### To verify the management point status in the Configuration Manager console

1. In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and then choose **Component Status**.

2. Look for the **SMS_MP_CONTROL_MANAGER** component. In the **Status** column, confirm that the status is **OK**.

   > [!NOTE]
   > It can take up to 30 minutes after the wizard closes for the management point to appear as healthy. If the status shows **Warning** or **Critical**, check the log files as described below.

3. In the **Administration** workspace, expand **Site Configuration** > **Servers and Site System Roles**, and then choose **DMZ-MP.branch.fabrikam.com**.

4. In the lower pane, confirm that the **Management point** role is listed and that the **Status** is **OK**.

### To verify the management point installation by reviewing log files

1. Sign in to `DMZ-MP`.

2. Open the following log files in **CMTrace** (located at `C:\Program Files\Microsoft Configuration Manager\tools\CMTrace.exe` on the site server, or copy it to `DMZ-MP`):

   | Log file | Location on DMZ-MP | What to look for |
   |----------|------------------|-----------------|
   | `MPSetup.log` | `C:\Program Files\SMS_CCM\Logs` | Successful MP installation messages; look for `Installation was successful`. |
   | `MPControl.log` | `C:\Program Files\SMS_CCM\Logs` | Management point control manager status; confirm no recurring errors. |
   | `CcmMessaging.log` | `C:\Program Files\SMS_CCM\Logs` | Communication between the MP and the site server. |

3. On the site server (`SiteServer`), review `sitecomp.log` in `C:\Program Files\Microsoft Configuration Manager\Logs` to confirm that the site component manager successfully installed the management point role on `DMZ-MP`.

### To test client communication with the new management point

1. On a client computer in `branch.fabrikam.com`, open a command prompt and run the following command to manually assign the client to the new management point:

   ```cmd
   "C:\Program Files\Microsoft Policy Platform\policyhost.exe"
   ```

   Or trigger a machine policy retrieval cycle:

   - Open the **Configuration Manager** item in **Control Panel**.
   - On the **Actions** tab, choose **Machine Policy Retrieval & Evaluation Cycle**, and then choose **Run Now**.

2. Review `C:\Windows\CCM\Logs\LocationServices.log` on the client to confirm that the client resolves and contacts `DMZ-MP.branch.fabrikam.com`.

3. Review `C:\Windows\CCM\Logs\ClientLocation.log` on the client to confirm that the management point assignment is successful.

> [!TIP]
> If clients in `branch.fabrikam.com` can't locate the management point automatically, configure the client installation property `SMSMP=DMZ-MP.branch.fabrikam.com` to directly assign clients to the new management point. For more information, see [About client installation properties](../../../clients/deploy/about-client-installation-properties.md).

## Next steps

- [Add site system roles](add-site-system-roles.md)
- [Install site system roles](install-site-system-roles.md)
- [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest)
- [Accounts used in Configuration Manager](../../../plan-design/hierarchy/accounts.md)
- [PKI certificate requirements for Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md)
