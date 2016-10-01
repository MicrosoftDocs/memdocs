---
title: "Configuring Endpoint Protection | System Center Configuration Manager"
ms.custom: na
ms.date: 08/05/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: 21
author: NathBarnmanager: angrobe

---
# Configuring Endpoint Protection in System Center Configuration Manager
Before you can use Endpoint Protection to manage security and malware on Configuration Manager client computers, set it up using this topic.  

## How to Configure Endpoint Protection in Configuration Manager  
 Endpoint Protection in Configuration Manager has dependencies within and outside of the product.  

### Configure Endpoint Protection in Configuration Manager  
There are five steps for configuring endpoint protection

|Step|Details|
|---|----|
|Step 1|[Create an Endpoint Protection point site system role](endpoint-protection-site-role.md) - Install the Endpoint Protection point site system role |
|Step 2|[Configure alerts for Endpoint Protection](endpoint-configure-alerts.md) - Configure Endpoint Protection alerts to notify administrators when specific security events occur in your hierarchy|
|Step 3 | [Configure definition update sources for Endpoint Protection clients](endpoint-definition-updates.md) - Choose from available methods to keep antimalware definitions up to date on client computers|
|Step 4|[Configure the default antimalware policy and create custom antimalware policies](endpoint-antimalware-policies.md) - The default antimalware policy is applied when the Endpoint Protection client is installed; custom policies are applied within 60 minutes of deploying the client|
|Step 5|[Configure custom client settings for Endpoint Protection](endpoint-protection-configure-client.md) - Configure custom client settings for Endpoint Protection to deploy to collections of computers|

> [!IMPORTANT]  
>  If you manage endpoint protection for Windows 10 computers, then you must configure Configuration Manager to update and distribute malware definitions for Windows Defender. Windows Defender is included in Windows 10 but SCEPInstall must still be installed and custom client settings for Endpoint Protection (Step 5) are still required.  
