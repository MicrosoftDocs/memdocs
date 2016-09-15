---
title: "Configuring Endpoint Protection | System Center Configuration Manager"
ms.custom: na
ms.date: 2016-08-05
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0a9dc0fe-a942-40a2-bab1-7eeee4d95380
caps.latest.revision: 21
author: NathBarn
translation.priority.ht:
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# Configuring Endpoint Protection in System Center Configuration Manager
Before you can use Endpoint Protection to manage security and malware on Configuration Manager client computers, you must perform the configuration steps detailed in this topic.

## How to Configure Endpoint Protection in Configuration Manager
 Endpoint Protection in Configuration Manager has external dependencies and dependencies in the product.

### Steps to Configure Endpoint Protection in Configuration Manager
 Use the following table for the steps, details, and more information about how to configure Endpoint Protection.

> [!IMPORTANT]
>  If you manage endpoint protection for Windows 10 computers, then you must configure Configuration Manager to update and distribute malware definitions for Windows Defender. Windows Defender is included in Windows 10 but SCEPInstall must still be installed and custom client settings for Endpoint Protection (**Step 5** below) are still required.

|Steps|Details|
|-----------|-------------|
|**Step 1:** Create an Endpoint Protection point site system role.|The Endpoint Protection point site system role must be installed before you can use Endpoint Protection. It must be installed on one site system server only, and it must be installed at the top of the hierarchy on a central administration site or a stand-alone primary site. See [Step 1: Create an Endpoint Protection Point Site System Role](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_Step1) in this topic.|
|**Step 2:** Configure alerts for Endpoint Protection.|Alerts inform the administrator when specific events have occurred, such as a malware infection. Alerts are displayed in the **Alerts** node of the **Monitoring** workspace, or optionally can be emailed to specified users. See [Step 2: Configure Alerts for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPalerts).|
|**Step 3:** Configure definition update sources for Endpoint Protection clients.|Endpoint Protection can be configured to use various sources to download definition updates. See [Step 3: Configure Definition Updates for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPdefs).|
|**Step 4:** Configure the default antimalware policy and create any custom antimalware policies.|The default antimalware policy is applied when the Endpoint Protection client is installed. Any custom policies you have deployed are applied by default, within 60 minutes of deploying the client. Ensure that you have configured antimalware policies before you deploy the Endpoint Protection client.See [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).|
|**Step 5:** Configure custom client settings for Endpoint Protection.|Use custom client settings to configure Endpoint Protection settings for collections of computers in your hierarchy.<br /><br /> Note: Do not configure the default Endpoint Protection client settings unless you are sure that you want these settings applied to all computers in your hierarchy. See [Step 5: Configure Custom Client Settings for Endpoint Protection](../../protect/deploy-use/configure-endpoint-protection.md#BKMK_EPclient) in this topic.|

# Create an Endpoint Protection Point Site System Role
 The Endpoint Protection point site system role must be installed before you can use Endpoint Protection. It must be installed on one site system server only, and it must be installed at the top of the hierarchy on a central administration site or a stand-alone primary site.

 Use one of the following procedures depending on whether you want to install a new site system server for Endpoint Protection or use an existing site system server.

> [!IMPORTANT]
>  When you install an Endpoint Protection point, an Endpoint Protection client is installed on the server hosting the Endpoint Protection point. Services and scans are disabled on this client to enable it to co-exist with any existing antimalware solution that is installed on the server. If you later enable this server for management by Endpoint Protection and select the option to remove any third-party antimalware solution, the third-party product will not be removed. You must uninstall this product manually.

## New site system server: Endpoint Protection point site system role:

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.

3.  On the **Home** tab, in the **Create** group, click **Create Site System Server**.

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.

    > [!IMPORTANT]
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.

7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.

    > [!NOTE]
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can then configure custom settings for each antimalware policy you create. Join Microsoft Active Protection Service, to help to keep your computers more secure by supplying Microsoft with malware samples that can help Microsoft to keep antimalware definitions more up-to-date. Additionally, when you join Microsoft Active Protection Service, the Endpoint Protection client can use the dynamic signature service to download new definitions before they are published to Windows Update. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).

8.  Complete the wizard.

> [!div class="button"]
[Next step >](endpoint-configure-alerts.md)

## Existing site system server: Endpoint Protection point site system role:

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, expand **Site Configuration**, click **Servers and Site System Roles**, and then select the server that you want to use for Endpoint Protection.

3.  On the **Home** tab, in the **Server** group, click **Add Site System Roles**.

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.

    > [!IMPORTANT]
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.

7.  On the **Microsoft Active Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.

    > [!NOTE]
    >  This option configures the Microsoft Active Protection Service settings that are used by default. You can configure custom settings for each antimalware policy you configure. For more information, see [How to create and deploy antimalware policies for Endpoint Protection in System Center Configuration Manager](../../protect/deploy-use/antimalware-policies-for-endpoint-protection.md).

8.  Complete the wizard.

> [!div class="button"]
[Next step >](endpoint-configure-alerts.md)
