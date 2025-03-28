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
- ⚠️ Existing conflicting DirectAccess (DA) or legacy VPN configurations. In particular NRPT-table entries.

## Prerequisites

### 🪪 Licensing

- Microsoft Entra Suite trial licenses https://aka.ms/EntraSuiteTrial

### 💻 Client Device

- [Documentation](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client)
- [Release history](https://learn.microsoft.com/en-us/entra/global-secure-access/reference-windows-client-release-history)
- [AVD/Windows 365](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client#prerequisites)
- Windows 10/11 - Hybrid- or Entra joined
- Local administrator credentials are required to install or upgrade the client
- Android - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-android-client?tabs=device-administrator)
- iOS/iPadOS - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-ios-client)
- Hardening - [Link](https://microsoft.github.io/GlobalSecureAccess/How-To/HardenWinGSA)

### 🌐 Microsoft Entra private network connector

- [Documentation](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#install-and-register-a-connector)
- **High availability and load balancing**
    - [High availability and load balancing of your private network connectors and applications](https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-high-availability-load-balancing)
    - [Optimize traffic flow with Microsoft Entra application proxy](https://learn.microsoft.com/en-us/entra/identity/app-proxy/application-proxy-network-topology)
- **Networking**
    - [Allow access to URLs](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#allow-access-to-urls)
- **Domain join the connector or not?**
    - AD Kerberos SSO - No domain join required
    - Kerberos constraint delegation (KCD) with app proxy - Domain join required [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#recommendations-for-the-connector-server)
- Min. Windows Server 2016
- Focus on CPU and Networking for machine sizing
- Azure and AWS Marketplace offering also available
- Line of sight to destination application needed
- Currently doesn’t support multi-geo connectors. The cloud service instances for your connector are chosen in the same region as your Microsoft Entra tenant (or the closest region to it) even if you have connectors installed in regions different from your default region.

### 🔒 Entra ID

- Group for PoC users
- Break-glass accounts provided

### 👤 AD Kerberos SSO

- [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-kerberos-sso)
- The latest version of the Microsoft Entra Private Access connector is installed on a Windows server that has access to your domain controllers
- All domain controllers will be published through Private Access (see details below)
- Private DNS with suffixes
- How does the users login to Windows? 
    - Using password? No extra steps are needed
    - Windows Hello for Business - Deploy Cloud Kerberos Trust

### 💼 Entra ID roles

- Global Secure Access Administrator
- Application Administrator
- Conditional Access Administrator
- For installing Private Network Connector: At least Application Administrator

## Application Segments

Name of  application:

| IP | FQDN | Port(s) | TCP/UDP |
| --- | --- | --- | --- |
|  |  |  |  |
|  |  |  |  |

## Domain controllers

Please note all domain controllers in your environment

| Hostname | FDQN | IP |
| --- | --- | --- |
|  |  |  |
|  |  |  |

List DNS suffixes to be published:

## **⚠️ Known limitations**

- Disable DNS over HTTPS (Secure DNS) | [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check#dns-over-https-not-supported)
- Disable QUIC | [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check#quic-disabled-in-microsoft-edge)
- Guidance on disabling IPv6 on Windows | [Link](https://learn.microsoft.com/troubleshoot/windows-server/networking/configure-ipv6-in-windows#:~:text=will%20be%20preferred.-,Disable%20IPv6,-Decimal%20255%0AHexadecimal)
- DNS / NRPT Troubleshooting | [Link](https://microsoft.github.io/GlobalSecureAccess/Troubleshooting/WindowsClientTroubleshooting#how-does-dns-work-with-gsa)
