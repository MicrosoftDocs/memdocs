---
# required metadata

title: Use Intune to remediate vulnerabilities found by Microsoft Defender for Endpoint
description: Use Microsoft Intune Security Tasks to manage threats and vulnerabilities identified by Microsoft Defender for Endpoint.
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 12/06/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: aanavath

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
---

# Use Microsoft Intune security tasks to remediate device vulnerabilities identified by Microsoft Defender for endpoint

When you [integrate Microsoft Defender for Endpoint with Microsoft Intune](/mem/intune-service/protect/advanced-threat-protection-configure#connect-microsoft-defender-for-endpoint-to-intune), you can leverage Defender's threat and vulnerability management through Intune security tasks. These tasks help Intune admins understand and address current vulnerabilities based on guidance from Defender for Endpoint. This integration enhances the discovery and prioritization of vulnerabilities, improving remediation response times across your environment.

[Threat & Vulnerability Management](/windows/security/threat-protection/windows-defender-atp/next-gen-threat-and-vuln-mgt) is part of [Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint).

## How integration works
 
After you integrate Intune with Microsoft Defender for Endpoint, Defender for Endpoint receives threat and vulnerability details from Intune-managed devices. These details are visible to security admins in the Microsoft Defender Security Center console.

In the Security Center console, [security admins can review endpoint vulnerabilities](/defender-vulnerability-management/defender-vulnerability-management#remediation-and-tracking) and create security tasks managed through Intune. These tasks appear in the Microsoft Intune admin center, where Intune admins can act and remediate issues based on Defender's guidance:

- Vulnerabilities are identified through scans and assessments by Microsoft Defender for Endpoint.
- Not all identified vulnerabilities support remediation through Intune; only those vulnerabilities that are compatible result in security tasks.

Security tasks identify:

- The type of vulnerability
- Priority
- Status
- Steps for remediation

Intune admins can view a security task and then choose to accept or reject it. For accepted tasks, the admin follows the guidance provided to use Intune for remediation. Once the remediation is successful, the admin sets the task to **Complete Task**, which updates its status in both Intune and Defender for Endpoint where security admins can verify the revised status of the vulnerability.

### Types of security tasks

Each security task has a *Remediation Type*:
- Application: For example, Microsoft Defender for Endpoint finds a vulnerability in an app like *Contoso Media Player v4*. An admin creates a task to update the app, which might involve applying a security update or installing a new version.
- Configuration: For instance, if devices lack protection from *Potentially Unwanted Applications* (PUA), an admin creates a task to configure the setting in the Microsoft Defender Antivirus profile.

When Intune doesn’t support implementation of a suitable remediation, Microsoft Defender for Endpoint doesn't create a security task.

### Remediation actions

Common security task remediations include:

- **Block** an application from running.
- **Deploy** an operating system update to mitigate the vulnerability.
- **Deploy** endpoint security policy to mitigate the vulnerability.
- **Modify** a registry value.
- **Disable** or **Enable** a configuration to affect the vulnerability.
- **Require Attention**, which alerts the admin when no suitable recommendation is available.

### Workflow Example

Following is an example of the workflow for discovering and remediating an application vulnerability:

- A Microsoft Defender for Endpoint scan identifies a vulnerability in the app Contoso Media Player v4, which is an unmanaged app that isn't deployed by Intune. An admin creates a security task to update the app.
- The security task appears in the Microsoft Intune admin center with a status of **Pending**. 
- The Intune admin views the task details and selects **Accept**, which changes the status of the task to Accepted in both Intune and Defender for Endpoint.
- The admin follows the remediation guidance provided. For managed apps, Intune might include instructions or links to update the app. For unmanaged apps, Intune can only provide text instructions.
- After addressing the vulnerability, the Intune admin marks the task as **Complete Task*. This action updates the status in both Intune and Defender for Endpoint, where security admins confirm the remediation is successful and complete.

## Prerequisites

**Subscriptions**:

- Microsoft Intune Plan 1
- Microsoft Defender for Endpoint ([Sign up for a free trial](https://www.microsoft.com/WindowsForBusiness/windows-atp?ocid=docs-wdatp-main-abovefoldlink).)

Intune configurations for Defender for Endpoint:
- Configure a [service-to-service connection](/mem/intune-service/protect/advanced-threat-protection-configure#connect-microsoft-defender-for-endpoint-to-intune) with Microsoft Defender for Endpoint.
- Deploy an Intune policy that configures settings for **Microsoft Defender for Endpoint** to devices to assess risk. 


## Work with security tasks

Before you manage security tasks, they must be created within the Defender Security Center. For detailed instructions, see the Defender for Endpoint documentation on [remediating vulnerabilities](/microsoft-365/security/defender-endpoint/tvm-remediation?view=o365-worldwide&preserve-view=true#request-remediation).

To manage security tasks:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security tasks**.
3. Choose a security task to view its details. In the task window, you can select additional links, including:
   - MANAGED APPS - View the app that is vulnerable. When the vulnerability applies to multiple apps, Intune displays a filtered list of apps.
   - DEVICES - View a list of the *Vulnerable devices* from which you can link through to an entry with more details for the vulnerability on that device.
   - REQUESTOR - Use the link to send mail to the admin who submitted this security task.
   - NOTES - Read custom messages submitted by the requestor when opening the security task.

4. Select **Accept** or **Reject** to send notification to Defender for Endpoint for your planned action. When you accept or reject a task, you can submit notes, which are sent to Defender for Endpoint.

5. After accepting a task, reopen the security task (if it closed), and follow the REMEDIATION details to remediate the vulnerability. The instructions provided by Defender for Endpoint in the security task details vary depending on the vulnerability involved.

6. After completing the remediation steps, open the security task and select **Complete Task**. This action updates the security task status in both Intune and Defender for Endpoint.

Successful remediation can reduce the risk exposure score in Defender for Endpoint based on subsequent status updates from the remediated devices.

## Related content

- Learn more about Intune and [Microsoft Defender for Endpoint](advanced-threat-protection.md).
- Review Intune [Mobile Threat Defense](mobile-threat-defense.md).
- Review the [Threat & Vulnerability Management dashboard](/windows/security/threat-protection/windows-defender-atp/tvm-dashboard-insights) in Microsoft Defender for Endpoint.
