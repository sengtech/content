# Microsoft SSE Private Access PoC

## Kick-off

- Walkthrough of high-level requirements
- Deciding on stakeholders
- User scenarios in scope
- Agree on timeline

## Scoping

- Running PoC in production or test environment?
- Granular apps or QuickAccess (VPN like)
- Kerberos SSO to AD resources?
- Conditional Access policies

## Prerequisites

### 🪪 Licensing

- Microsoft Entra Suite trial licenses https://aka.ms/EntraSuiteTrial

### 💻 Client Device

- [Documentation](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client)
- Windows 10/11 - Hybrid- or Entra joined
- Azure Virtual Desktop single-session and Windows 365 is supported
- Local administrator credentials are required to install or upgrade the client
- Android - Defender app installed

### 🌐 Microsoft Entra private network connector

- [Documentation](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#install-and-register-a-connector)
- [Allow access to URLs](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#allow-access-to-urls)
- Min. Windows Server 2016
- Focus on CPU and Networking for machine sizing
- Azure and AWS Marketplace offering also available
- Line of sight to destination application needed
- Currently doesn’t support multi-geo connectors. The cloud service instances for your connector are chosen in the same region as your Microsoft Entra tenant (or the closest region to it) even if you have connectors installed in regions different from your default region.

### 🔒 Entra ID

- Group for PoC users
- Break-glass accounts provided

### 👤 Kerberos SSO

- The latest version of the Microsoft Entra Private Access connector is installed on a Windows server that has access to your domain controllers
- All domain controllers will be published through Private Access (see details below)
- Private DNS with suffixes

### 💼 Entra ID roles

- Global Secure Access Administrator
- Application Administrator
- Conditional Access Administrator

## Application Segments

Name of  application:

| IP | FQDN | Port(s) | TCP/UDP |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |

## Domain controllers

Please note all domaincontrollers in your environment

| Hostname | FDQN | IP |
| --- | --- | --- |
|  |  |  |
|  |  |  |

List DNS suffixes to be published:

## **⚠️ Known limitations**

- Disable DNS over HTTPS (Secure DNS)
- Disable QUIC - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check#quic-not-supported-for-internet-access)
