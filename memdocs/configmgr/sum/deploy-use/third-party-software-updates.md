---
title: Enable third-party updates
titleSuffix: Configuration Manager
description: Enable third-party updates in Configuration Manager
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Enable third-party updates

*Applies to: Configuration Manager (current branch)*

The **Third-Party Software Update Catalogs** node in the Configuration Manager console allows you to subscribe to third-party catalogs, publish their updates to your software update point (SUP), and then deploy them to clients.  <!--1357605, 1352101, 1358714-->

> [!Note]  
> In version 2006 and earlier, Configuration Manager doesn't enable this feature by default. Before using it, enable the optional feature **Enable third party update support on clients**. For more information, see [Enable optional features from updates](../../core/servers/manage/optional-features.md).

## Prerequisites

- Sufficient disk space on the top-level software update point's `WSUSContent` directory to store the source binary content for third-party software updates.
    - The amount of required storage varies based on the vendor, types of updates, and specific updates that you publish for deployment.
    - If you need to move the `WSUSContent` directory to another drive with more free space, see the [How to change the location where WSUS stores updates locally](/archive/blogs/sus/wsus-how-to-change-the-location-where-wsus-stores-updates-locally) blog post.
- The third-party software update synchronization service requires internet access.
    - For the partner catalogs list, download.microsoft.com over HTTPS port 443 is needed. 
    -  Internet access to any third-party catalogs and update content files. Additional ports other than 443 may be needed.
    - Third-party updates use the same proxy settings as the SUP.

## Additional requirements when the SUP is remote from the top-level site server 

1. SSL should be enabled on the SUP when it's remote. This requires a server authentication certificate generated from an internal certificate authority or via a public provider.
    - [Configure SSL on WSUS](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol)
        - When you configure SSL on WSUS, note some of the web services and the virtual directories are always HTTP and not HTTPS. 
        - Configuration Manager downloads third-party content for software update packages from your WSUS content directory over HTTP.   
    - [Configure SSL on the SUP](../get-started/install-a-software-update-point.md#configure-ssl-communications-to-wsus)

2. When setting the third-party updates WSUS signing certificate configuration to **Configuration Manager manages the certificate** in the Software Update Point Component Properties, the following configurations are required to allow the creation of the self-signed WSUS signing certificate: 
   - Remote registry should be enabled on the SUP server.
   - The **WSUS server connection account** should have remote registry permissions on the SUP/WSUS server.

3. Create the following registry key on the Configuration Manager site server:
    - `HKLM\Software\Microsoft\Update Services\Server\Setup`, create a new DWORD named **EnableSelfSignedCertificates** with a value of `1`.

4. To enable installing the self-signed WSUS signing certificate to the Trusted Publishers and Trusted Root stores on the remote SUP server:
   - The **WSUS server connection account** should have remote administration permissions on the SUP server.

     If this item isn't possible, export the certificate from the local computer's WSUS store into the Trusted Publisher and Trusted Root stores.

> [!NOTE]
> The **WSUS server connection account** can be identified by viewing the **Proxy and Account Settings** tab on the Site System role properties of the SUP. If an account is not specified, the site server's computer account is used.

## Enable third-party updates on the SUP

If you enable this option, you can subscribe to third-party update catalogs in the Configuration Manager console. You can then publish those updates to WSUS and deploy them to clients. The following steps should be run once per hierarchy to enable and set up the feature for use. The steps may need to be rerun if you ever replace the top-level SUP's WSUS server.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
2. Select the top-level site in the hierarchy. In the ribbon, select **Configure Site Components**, and select **Software Update Point**.
3. Switch to the **Third-Party Updates** tab. Select the option **Enable third-party software updates**.

    ![Third-party updates SUP properties screenshot](media/third-party-sup-properties.PNG)

## Configure the WSUS signing certificate

You'll need to decide if you want Configuration Manager to automatically manage the third-party WSUS signing certificate using a self-signed certificate, or if you need to manually configure the certificate.

### Automatically manage the WSUS signing certificate

If you don't have a requirement to use PKI certificates, you can choose to automatically manage the signing certificates for third-party updates. The WSUS certificate management is done as part of the sync cycle and gets logged in the `wsyncmgr.log`.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
2. Select the top-level site in the hierarchy. In the ribbon, select **Configure Site Components**, and select **Software Update Point**.
3. Switch to the **Third-Party Updates** tab. Select the option **Configuration Manager manages the certificate**.
4. A new certificate of type **Third-party WSUS Signing** is created in the **Certificates** node under **Security** in the **Administration** workspace.

### Manually manage the WSUS signing certificate

If you need to manually configure the certificate, such as needing to use a PKI certificate, you'll need to use either [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server) or another tool to do so.

1. Configure the signing certificate using [System Center Updates Publisher](../tools/updates-publisher-options.md#update-server).
2. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Sites** node.
3. Select the top-level site in the hierarchy. In the ribbon, select **Configure Site Components**, and select **Software Update Point**.
4. Switch to the **Third-Party Updates** tab. Select the option for **Manually manage the certificate**.

## Enable third-party updates on the clients

Enable third-party updates on the clients in the client settings. The setting sets the Windows Update agent policy for [Allow signed updates for an intranet Microsoft update service location](/windows-server/administration/windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates#allow-signed-updates-from-an-intranet-microsoft-update-service-location). This client setting also installs the WSUS signing certificate to the Trusted Publisher store on the client. The certificate management logging is seen in `updatesdeployment.log` on the clients. Run these steps for each custom client setting you want to use for third-party updates. For more information, see the [About client settings](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) article.

1. In the Configuration Manager console, go to the **Administration** workspace and select the **Client Settings** node.
2. Select an existing custom client setting or create a new one.
3. Select the **Software Updates** tab on the left-hand side. If you don't have this tab, make sure that the **Software Updates** box is enabled.
4. Set **Enable third-party software updates** to **Yes**.

## Add a custom catalog

*Partner catalogs* are software vendor catalogs that have their information already registered with Microsoft. With partner catalogs, you can subscribe to them without having to specify any additional information. Catalogs that you add are called *custom catalogs*. You can add a custom catalog from a third-party update vendor to Configuration Manager. Custom catalogs must use https and the updates must be digitally signed.

1. Go to the **Software Updates Library** workspace, expand **Software updates**, and select the **Third-Party Software Update Catalogs** node.

     ![Third-party updates node screenshot](media/third-party-updates-node.PNG)
1. select **Add Custom Catalog** in the ribbon.

     ![Third-party updates add custom catalog](media/third-party-updates-custom-catalog.png)
1. On the **General** page, specify the following items:
    - **Download URL**: A valid HTTPS address of the custom catalog.
    - **Publisher**: The name of the organization that publishes the catalog.
    - **Name**: The name of the catalog to display in the Configuration Manager Console.
    - **Description**: A description of the catalog.
    - **Support URL** (optional): A valid HTTPS address of a website to get help with the catalog.
    - **Support Contact** (optional): Contact information to get help with the catalog.
1. Select **Next** to review the catalog summary and to continue with completing the **Third-party Software Updates Custom Catalog Wizard**.

## Subscribe to a third-party catalog and sync updates

When you subscribe to a third-party catalog in the Configuration Manager console, the metadata for every update in the catalog are synced into the WSUS servers for your SUPs. The sync of the metadata allows the clients to determine if any of the updates are applicable. Perform the following steps for each third-party catalog to which you want to subscribe:

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Software Updates** and select the **Third-Party Software Update Catalogs** node.
1. Select the catalog to subscribe and then select **Subscribe to Catalog** in the ribbon.
    ![Third-party updates subscribe to catalog](media/third-party-updates-subscribe.png)
1. Review and approve the catalog certificate on the **Review and approve** page of the wizard.
   > [!NOTE]
   > 
   > When you subscribe to a third-party software update catalog, the certificate that you review and approve in the wizard is added to the site. This certificate is of type **Third-party Software Updates Catalog**. You can manage it from the **Certificates** node under **Security** in the **Administration** workspace.
1. If the third-party catalog is v3, you'll be offered pages to **Select Categories** and **Stage Content**. For more information about configuring these options, see the [Third-party v3 catalog options](#bkmk_v3) section.
1. Choose your options on the **Schedule** page:
   - **Simple schedule**:  Choose the hour, day, or month interval. The default is a simple schedule that synchronizes every 7 days.
   - **Custom schedule**: Set a complex schedule.
1. Review your settings on the **Summary** page and complete the wizard.
1. After the catalog is downloaded, the product metadata needs to be synchronized from the WSUS database into the Configuration Manager database. [Manually start the software updates synchronization](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) to synchronize the product information.
1. Once the product information is synchronized, [Configure the SUP to synchronize the desired product](../get-started/configure-classifications-and-products.md#to-configure-classifications-and-products-to-synchronize) into Configuration Manager.
1. [Manually start the software updates synchronization](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) to synchronize the new product's updates into Configuration Manager.
1. When the synchronization completes, you can see the third-party updates in the **All Updates** node. These updates are published as **metadata-only** updates until you choose to publish them.
     - The icon with the blue arrow represents a metadata-only software update. ![Metadata only software update icon](media/MetadataOnly.png)

## Publish and deploy third-party software updates

Once the third-party updates are in the **All Updates** node, you can choose which updates should be published for deployment. When you publish an update, the binary files are downloaded from the vendor and placed into the `WSUSContent` directory on the top-level SUP.

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Software Updates** and select the **All Software Updates** node.
1. Select **Add Criteria** to filter the list of updates. For example, add **Vendor** for **HP**. to view all updates from HP.
1. Select the updates that are required by your organization. Select **Publish Third-Party Software Update Content**.
    - This action downloads the update binaries from the vendor then stores them in the `WSUSContent` directory on the top-level software update point.
1. [Manually start the software updates synchronization](../get-started/synchronize-software-updates.md#manually-start-software-updates-synchronization) to change the state of the published updates from metadata-only to deployable updates with content.
    > [!NOTE]
    > When you publish third-party software update content, any certificates used to sign the content are added to the site. These certificates are of type **Third-party Software Updates Content**. You can manage them from the **Certificates** node under **Security** in the **Administration** workspace.

1. Review the progress in the `SMS_ISVUPDATES_SYNCAGENT.log`. The log is located on the  top-level software update point in the site system Logs folder.
1. Deploy the updates using the [Deploy software updates](../deploy-use/deploy-software-updates.md) process.
1. On the **Download Locations** page of the **Deploy Software Updates Wizard**, select the default option to **Download software updates from the internet**. In this scenario, the content is already published to the software update point, which is used to download the content for the deployment package.
1. Clients will need to run a scan and evaluate updates before you can see compliance results.  You can manually trigger this cycle from the Configuration Manager control panel on a client by running the **Software Updates Scan Cycle** action.

## <a name="bkmk_v3"></a> Third-party v3 catalog options

V3 catalogs allow for categorized updates. When using catalogs that include categorized updates, you can configure synchronization to include only specific categories of updates to avoid synchronizing the entire catalog. With categorized catalogs, when you're confident you'll deploy a category, you can configure it to automatically download and publish to WSUS.

> [!IMPORTANT]
> This option is only available for v3 third-party update catalogs, which support categories for updates. These options are disabled for catalogs that aren't published in the v3 format. <!--4469002-->

1. In the Configuration Manager console, go to the **Software Library** workspace. Expand **Software Updates** and select the **Third-Party Software Update Catalogs** node.
1. Select the catalog to subscribe and select **Subscribe to Catalog** in the ribbon.
1. Choose your options on the **Select Categories** page:

   - **Synchronize all update categories** (default)
       - Synchronizes all updates in the third-party update catalog into Configuration Manager.
   -  **Select categories for synchronization**
       - Choose which categories and child categories to synchronize into Configuration Manager.

      ![Select update categories to synchronize into Configuration Manager](./media/4469002-select-categories-for-sync.png)

1. Choose if you want to **Stage update content** for the catalog. When you stage the content, all updates in the selected categories are automatically downloaded to your top-level software update point meaning you don't need to ensure they're already downloaded before deploying. You should only automatically stage content for updates you are likely to deploy to avoid excessive bandwidth and storage requirements.

   - **Do not stage content, synchronize for scanning only (recommended)**
     - Don't download any content for updates in the third-party catalog
   - **Stage the content for selected categories automatically**
     - Choose the update categories that will automatically download content.
     - The content for updates in selected categories will be downloaded to the top-level software update point's WSUS content directory.
      ![Select update categories to stage content](./media/4469002-stage-content.png)
1. Set your **Schedule** for catalog synchronization, then complete the wizard.

## Edit an existing subscription

You can edit an existing subscription by selecting **Properties** from the ribbon or the right-click menu.

> [!IMPORTANT]
> Some options are only available for v3 third-party update catalogs, which support categories for updates. These options are disabled for catalogs that aren't published in the  v3 format.<!--4469002-->

1. In the **Third-Party Software Update Catalogs** node, right-click on the catalog and select **Properties** or select **Properties** from the ribbon.
1. You can view the following information from the **General tab**, but not edit the information.:
    > [!NOTE]
    > If you need to change any of the information here, you have to add a new custom catalog.  
    > Provided the download URL is unchanged, the existing catalog must be removed before one with the same download URL can be added.

    - **Download URL**: The HTTPS address of the custom catalog.
    - **Publisher**: The name of the organization that publishes the catalog.
    - **Name**: The name of the catalog to display in the Configuration Manager Console.
    - **Description**: A description of the catalog.
    - **Support URL**: A valid HTTPS address of a website to get help with the catalog.
    - **Support Contact**: Contact information to get help with the catalog.
1. Choose your options on the **Select Categories** tab.
   - **Synchronize all update categories** (default)
       - Synchronizes all updates in the third-party update catalog into Configuration Manager.
   -  **Select categories for synchronization**
       - Choose which categories and child categories to synchronize into Configuration Manager.
1. Choose your options for the **Stage update content** tab.
   - **Do not stage content, synchronize for scanning only (recommended)**
     - Don't download any content for updates in the third-party catalog
   - **Stage the content for selected categories automatically**
     - Choose the update categories that will automatically download content.
     - The content for updates in selected categories will be downloaded to the top-level software update point's WSUS content directory.
1. Select how often to synchronize the catalog on the **Schedule** tab.
   - **Simple schedule**:  Choose the hour, day, or month interval.
   - **Custom schedule**: Set a complex schedule.

## Unsubscribe from catalog and delete custom catalogs

In the **Third-Party Software Update Catalogs** node, right-click on the catalog and select **Unsubscribe** to stop synchronizing the catalog.  
You can also use the **Unsubscribe** option from the ribbon. When you unsubscribe from a catalog, the approval for catalog signing and update content certificates are removed. Existing updates aren't removed, but you may not be able to deploy them. With custom catalogs, you also have the option of deleting it after you've unsubscribed. Select **Delete Custom Catalog** from either the ribbon or the right-click menu for the catalog. Deleting the custom catalog removes it from view in the **Third-Party Software Update Catalogs** node.

## Monitoring progress of third-party software updates

Synchronization of third-party software updates is handled by the SMS_ISVUPDATES_SYNCAGENT component on the top-level default software update point. You can view status messages from this component, or see more detailed status in the `SMS_ISVUPDATES_SYNCAGENT.log`. This log is on the top-level software update point in the site system Logs folder. By default this path is C:\Program Files\Microsoft Configuration Manager\Logs. For more information on monitoring the general software update management process, see [Monitor software updates](../deploy-use/monitor-software-updates.md).

## <a name="bkmk_list-catalogs"></a> List additional third-party updates catalogs
<!--9989251-->

To help you find custom catalogs that you can import for third-party software updates, there's a documentation page with links to catalog providers. Starting in Configuration Manager 2107, you can also choose **More Catalogs** from the ribbon in the **Third-party software update catalogs** node. Right-clicking on **Third-Party Software Update Catalogs** node displays a **More Catalogs** menu item. Selecting **More Catalogs** opens a link to a documentation page containing a [list of additional third-party software update catalog providers](third-party-software-update-catalogs.md).

:::image type="content" source="./media/9989251-more-catalogs.png" alt-text="Screenshot of the Third-Party Software Update Catalogs node with the More Catalogs icon in the ribbon":::

## Known issues

- The machine where the console is running is used to download the updates from WSUS and add it to the updates package. The WSUS signing certificate must be trusted on the console machine. If it isn't, you may see issues with the signature check during the download of third-party updates.
- The third-party software update synchronization service can't publish content to metadata-only updates that were added to WSUS by another application, tool, or script, such as SCUP. The **Publish third-party software update content** action fails on these updates. If you need to deploy third-party updates that this feature doesn't yet support, use your existing process in full for deploying those updates.
- Configuration Manager has a new version for the catalog cab file format. The new version includes the certificates for the vendor's binary files. These certificates are added to the **Certificates** node under **Security** in the **Administration** workspace once you approve and trust the catalog.
     - You can still use the older catalog cab file version as long as the download URL is https and the updates are signed. The content will fail to publish because the certificates for the binaries aren't in the cab file and already approved. You can work around this issue by finding the certificate in the **Certificates** node, unblocking it, then publish the update again. If you're publishing multiple updates signed with different certificates, you'll need to unblock each certificate that is used.
     - For more information, see status messages 11523 and 11524 in the below status message table.
- When the third-party software update synchronization service on the top-level software update point requires a proxy server for internet access, digital signature checks may fail. To mitigate this issue, configure the WinHTTP proxy settings on the site system. For more information, see [Netsh commands for WinHTTP](/windows-server/networking/technologies/netsh/netsh-http).
- When using a CMG for content storage, the content for third-party updates won't download to clients if the **Download delta content when available** [client setting](../../core/clients/deploy/about-client-settings.md#allow-clients-to-download-delta-content-when-available) is enabled. <!--6598587-->
- If the catalog provider has changed the catalog's signing certificate since you last approved it or subscribed, the catalog sync will fail until the certification is approved in the **Certificates** node. For more information, see MessageID 11508 in [status messages](#status-messages) table.

## Status messages

| MessageID       | Severity           | Description | Possible cause| Possible solution
| ------------- |-------------| -----|----|----|
| 11508 | Error | Failure when checking signature for catalog &lt;catalog name> to WSUS. Make sure the catalog is subscribed and the catalog certificate &lt;certificate&gt; is not blocked. See `SMS_ISVUPDATES_SYNCAGENT.log` for further details. | The signing certification on the catalog may have changed since it was originally subscribed or last approved. | Make sure to review and approve the certificate in the **Certificates** node to allow the catalog to synchronize. |
| 11516 | Error | Failed to publish content for update "Update ID" because the content is unsigned. Only content with valid signatures can be published. | Configuration Manager doesn't allow unsigned updates to be published. | Publish the update in an alternate way. </br></br> See if a signed update is available from the vendor. |
| 11523 | Warning | Catalog "X" does not include content signing certificates, attempts to publish update content for updates from this catalog may be unsuccessful until content signing certificates are added and approved. | This message can occur when you import a catalog that is using an older version of the cab file format. | Contact the catalog provider to obtain an updated catalog that includes the content signing certificates. </br> </br> The certificates for the binaries aren't included in the cab file so the content will fail to publish. You can work around this issue by finding the certificate in the **Certificates** node, unblocking it, then publish the update again. If you're publishing multiple updates signed with different certificates, you'll need to unblock each certificate that is used. |
| 11524 | Error | Failed to publish update "ID" due to missing update metadata. | The update may have been synchronized to WSUS outside of Configuration Manager. | Synchronize the update with Configuration Manager before attempting to publish it's content. </br></br> If an external tool was used to publish the update as **Metadata only**, then use the same tool to publish the update content. |

## Working with third-party updates video
<iframe width="560" height="315" src="https://www.youtube.com/embed/ai8rLCLtuTI?rel=0" frameborder="0" allowfullscreen></iframe>

## PowerShell

You can use the following PowerShell cmdlets to automate the management of third-party updates in Configuration Manager:

- [Get-CMThirdPartyUpdateCatalog](/powershell/module/configurationmanager/get-cmthirdpartyupdatecatalog)
- [New-CMThirdPartyUpdateCatalog](/powershell/module/configurationmanager/new-cmthirdpartyupdatecatalog)
- [Remove-CMThirdPartyUpdateCatalog](/powershell/module/configurationmanager/remove-cmthirdpartyupdatecatalog)
- [Set-CMThirdPartyUpdateCatalog](/powershell/module/configurationmanager/set-cmthirdpartyupdatecatalog)
- [Publish-CMThirdPartySoftwareUpdateContent](/powershell/module/configurationmanager/publish-cmthirdpartysoftwareupdatecontent)
- [Get-CMThirdPartyUpdateCategory](/powershell/module/configurationmanager/get-cmthirdpartyupdatecategory)
- [Set-CMThirdPartyUpdateCategory](/powershell/module/configurationmanager/set-cmthirdpartyupdatecategory)

## Next step
> [!div class="nextstepaction"]
> [Deploy software updates](./deploy-software-updates.md)
