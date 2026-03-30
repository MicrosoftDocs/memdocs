---
title: Use Intune to remediate vulnerabilities found by Microsoft Defender for Endpoint
description: Integrate Microsoft Defender Vulnerability Management with Intune to create security tasks, track remediation, and reduce vulnerability exposure across managed devices.
author: brenduns
ms.author: brenduns
ms.date: 02/13/2026
ms.topic: how-to
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Use Microsoft Intune security tasks to remediate device vulnerabilities identified by Microsoft Defender for Endpoint

When you [integrate Microsoft Defender for Endpoint with Microsoft Intune](/intune/intune-service/protect/microsoft-defender-integrate#connect-microsoft-defender-for-endpoint-to-intune), you can leverage Microsoft Defender Vulnerability Management through Intune security tasks. These tasks help Intune admins understand and address current vulnerabilities based on guidance from Defender for Endpoint. This integration enhances the discovery and prioritization of vulnerabilities, improving remediation response times across your environment.

[Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) is part of [Microsoft Defender for Endpoint](/microsoft-365/security/defender-endpoint/microsoft-defender-endpoint).

## Prerequisites

**Subscriptions**:

- Microsoft Intune Plan 1
- Microsoft Defender for Endpoint ([Sign up for a free trial](https://www.microsoft.com/security/business/endpoint-security/microsoft-defender-endpoint).)

Intune configurations for Defender for Endpoint:

- Configure a service-to-service connection with Microsoft Defender for Endpoint, and enable the **Microsoft Intune connection** in the Microsoft Defender portal. This connection allows security admins to create Intune security tasks when submitting remediation requests. For setup instructions, see [Connect Microsoft Defender for Endpoint to Intune](/intune/intune-service/protect/microsoft-defender-integrate#connect-microsoft-defender-for-endpoint-to-intune).
- Deploy policies to onboard devices to Microsoft Defender for Endpoint and enable risk assessment. See [Configure Microsoft Defender for Endpoint with Intune](/intune/intune-service/protect/microsoft-defender-integrate).

## How integration works

After you integrate Intune with Microsoft Defender for Endpoint, Microsoft Defender Vulnerability Management identifies vulnerabilities on your managed devices.

In the Microsoft Defender portal, [security admins can review endpoint vulnerabilities](/defender-vulnerability-management/defender-vulnerability-management#remediation-and-tracking) and create Intune security tasks for remediation. These tasks appear in the Microsoft Intune admin center, where Intune admins can act and remediate issues based on Defender's guidance:

- Vulnerabilities are identified through scans and assessments by Microsoft Defender for Endpoint.
- Not all identified vulnerabilities support remediation through Intune; only those vulnerabilities that are compatible result in security tasks.

Security tasks identify:

- The type of vulnerability
- Priority
- Status
- Steps for remediation

Intune admins can view a security task and then choose to accept or reject it. For accepted tasks, the admin follows the guidance provided to use Intune for remediation. Once the remediation is successful, the admin sets the task to **Complete Task**, which updates its status in both Intune and Defender for Endpoint where security admins can verify the revised status of the vulnerability.

### Workflow Example

Following is an example of the workflow for discovering and remediating an application vulnerability:

- A Microsoft Defender for Endpoint scan identifies a vulnerability in the app Contoso Media Player v4, which is an unmanaged app that isn't deployed by Intune. A security admin in the Microsoft Defender portal creates an Intune security task to update the app.
- The security task appears in the Microsoft Intune admin center with a status of **Pending**.
- The Intune admin views the task details and selects **Accept**, which changes the status of the task to Accepted in both Intune and Defender for Endpoint.
- The admin follows the remediation guidance provided. For managed apps, Intune might include instructions or links to update the app. For unmanaged apps, Intune can only provide text instructions.
- After addressing the vulnerability, the Intune admin marks the task as **Complete Task**. This action updates the status in both Intune and Defender for Endpoint, where security admins confirm the remediation is successful and complete.

### Types of security tasks

Each security task has a *Remediation Type*:

- **Application**: For example, Microsoft Defender for Endpoint finds a vulnerability in an app like *Contoso Media Player v4*. An admin creates a task to update the app, which might involve applying a security update or installing a new version.
- **Configuration**: For instance, if devices lack protection from *Potentially Unwanted Applications* (PUA), an admin creates a task to configure the setting in the Microsoft Defender Antivirus profile.

When Intune doesn’t support implementation of a suitable remediation, Microsoft Defender for Endpoint doesn't create a security task.

### Remediation actions

Common security task remediations include:

- **Block** an application from running.
- **Deploy** an operating system update to mitigate the vulnerability.
- **Deploy** endpoint security policy to mitigate the vulnerability.
- **Modify** a registry value.
- **Disable** or **Enable** a configuration to affect the vulnerability.
- **Require Attention**, which alerts the admin when no suitable recommendation is available.

## Work with security tasks

Before you manage security tasks, they must be created in the Microsoft Defender portal. For detailed instructions, see the Defender for Endpoint documentation on [remediating vulnerabilities](/defender-vulnerability-management/tvm-remediation#request-remediation).

[!INCLUDE [manage-admin-tasks](../../intune-service/fundamentals/includes/manage-admin-tasks.md)]

To manage security tasks:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Security tasks**.
3. Choose a security task to view its details. In the task window, you can select additional links, including:
   - MANAGED APPS - View the app that's vulnerable. When the vulnerability applies to multiple apps, Intune displays a filtered list of apps.
   - DEVICES - View a list of the *Vulnerable devices* from which you can link through to an entry with more details for the vulnerability on that device.
   - REQUESTOR - Use the link to send mail to the admin who submitted this security task.
   - NOTES - Read custom messages submitted by the requestor when opening the security task.

4. Select **Accept** or **Reject** to send notification to Defender for Endpoint for your planned action. When you accept or reject a task, you can submit notes, which are sent to Defender for Endpoint.

5. After accepting a task, reopen the security task (if it closed), and follow the REMEDIATION details to remediate the vulnerability. The instructions provided by Defender for Endpoint in the security task details vary depending on the vulnerability involved.

6. After completing the remediation steps, open the security task and select **Complete Task**. This action updates the security task status in both Intune and Defender for Endpoint.

Successful remediation can reduce the risk exposure score in Defender for Endpoint based on subsequent status updates from the remediated devices. You can [monitor these risk levels](microsoft-defender-monitor.md) to track compliance improvements over time.

## Troubleshooting

If security tasks aren't appearing in Intune:

- Verify the Microsoft Intune connection is enabled in the Microsoft Defender portal.
- Confirm devices are onboarded to Microsoft Defender for Endpoint.
- Check that security admins are creating tasks for vulnerabilities Intune can remediate.
- Allow up to 15 minutes for task synchronization between portals.

## Next steps

- [Set up the integration](microsoft-defender-with-intune.md) - Complete prerequisites and connect services
- [Monitor compliance for risk levels](microsoft-defender-monitor.md) - Track device risk scores
- [Review Microsoft Defender Vulnerability Management](/defender-vulnerability-management/defender-vulnerability-management) - Understand security recommendations
- [Learn about Mobile Threat Defense](mobile-threat-defense.md) - Explore other threat protection options for Intune
