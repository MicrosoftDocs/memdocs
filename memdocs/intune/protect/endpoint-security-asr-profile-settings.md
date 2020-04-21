---
# required metadata

title: Intune endpoint security Attack surface reduction settings | Microsoft Docs
description: Endpoint security Attack surface reduction policy settings for Windows and macOS in Microsoft Intune 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/17/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha

---
# Attack surface reduction policy settings for endpoint security in Intune

View the settings you can configure in profiles for *Attack surface reduction* policy in the endpoint security node of Intune.

Supported platforms and profiles:

- **Windows 10 and later**:
  - Profile: **App and browser isolation**
  - Profile: **Web protection**
  - Profile: **Application control**
  - Profile: **Attack surface reduction rules**
  - Profile: **Device control**
  - Profile: **Exploit protection**

## App and browser isolation profile

### App and browser isolation

- **Turn on Application Guard for Edge (Options)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Not configured** (*default*)
  - **Enabled for Edge** - Application Guard opens unapproved sites in a Hyper-V virtualized browsing container.

  When set to *Enabled for Edge*, the following settings are available:
  
  - **Clipboard behavior**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    - **Choose what copy and paste actions are allowed from the local PC and an Application Guard virtual browser.
    - **Not configured** (*default*)
    - **Block copy and paste between PC and browser**
    - **Allow copy and paste from browser to PC only**
    - **Allow copy and paste from PC to browser only**
    - **Allow copy and paste between PC and browser**

  - **Block external content from non-enterprise approved sites**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Not configured** (*default*)
    - **Yes** - Block content from unapproved websites from loading.

  - **Collect logs for events that occur within an Application Guard browsing session**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Not configured** (*default*)
    - **Yes** - Collect logs for events that occur within an Application Guard virtual browsing session.

  - **Allow user-generated browser data to be saved**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Not configured** (*default*)
    - **Yes** - Allow user data that is created during an Application Guard virtual browsing session to be saved. Examples of user data include passwords, favorites, and cookies.

  - **Enable hardware graphics acceleration**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Not configured** (*default*)
    - **Yes** - Within the Application Guard virtual browsing session, use a virtual graphics processing unit to load graphics-intensive websites faster.


  - **Allow users to download files onto the host**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Not configured** (*default*)
    - **Yes** - Allow users to download files from the virtualized browser onto the host operating system​.

- **Application guard allow print to local printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing print to local printers.


- **Application guard allow print to network printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing print to network printers.
 

- **Application guard allow print to PDF**  

  - **Not configured** (*default*)
  - **Yes**- Allow printing print to PDF.

- **Application guard allow print to XPS**  

  - **Not configured** (*default*)
  - **Yes** - - Allow printing print to XPS.

- **Windows network isolation policy**  
  
  - **Not configured** (*default*)
  - **Yes** - Configure Windows network isolation policy.  
  
  When set to *Configure*, you can configure the following settings.

  - **IP ranges**  
    Expand the dropdown, select **Add**, and then specify a *lower address* and then an *upper address*.

  - **Cloud resources**  
    Expand the dropdown, select **Add**, and then specify an *IP address or FQDN* and a *Proxy*.

  - **Network domains**  
   Expand the dropdown, select **Add**, and then specify *Network domains*.
 
  - **Proxy servers**  
    Expand the dropdown, select **Add**, and then specify *Proxy servers*.

  - **Internal proxy servers**  
    Expand the dropdown, select **Add**, and then specify *Intenral proxy servers*.

  - **Neutral resources**  
    Expand the dropdown, select **Add**, and then specify *Neutral resources*.

  - **Disable Auto detection of other enterprise proxy servers**  
    - **Not configured** (*default*)
    - **Yes** - Disable Auto detection of other enterprise proxy servers.

  - **Disable Auto detection of other enterprise IP ranges**  
    - **Not configured** (*default*)
    - **Yes** - Disable Auto detection of other enterprise IP ranges.

## Web protection 

  CSP: []()

  - **Not configured** (*default*)
  - **Yes**

## Application control 

  CSP: []()

  - **Not configured** (*default*)
  - **Yes**

## Attack surface reduction rules

  CSP: []()

  - **Not configured** (*default*)
  - **Yes**

## Device control

  CSP: []()

  - **Not configured** (*default*)
  - **Yes**

## Exploit protection


  CSP: []()

  - **Not configured** (*default*)
  - **Yes**


## Next steps

[Endpoint security policy for ASR](../protect/endpoint-security-policy.md#attack-surface-reduction-profiles)
