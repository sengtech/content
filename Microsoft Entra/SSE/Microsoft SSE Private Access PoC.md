# Microsoft SSE Private Access PoC

## Kick-off

- Walkthrough of high-level requirements
- Deciding on stakeholders
- Use cases
- Agree on timeline

## Scoping

- Running PoC in production or test environment?
- Granular apps or QuickAccess (VPN like)
- Kerberos SSO to AD resources?
- Conditional Access policies
- ⚠️ Existing conflicting DirectAccess (DA) or legacy VPN configurations. In particular NRPT-table entries.
- ⚠️ **SCCM Boundary groups** - Defined by network location. Clients on the intranet evaluate their current network location and then use that information to identify boundary groups to which they belong. Possible solutions - Define every single IP address to a single or handful of boundary groups.

## Prerequisites

### 🪪 Licensing

- Microsoft Entra Suite trial licenses https://aka.ms/EntraSuiteTrial
- ⚠️ You need Global Admin privileges to activate the trial license

### 💻 Client

- [Documentation](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client)
- [Release history](https://learn.microsoft.com/en-us/entra/global-secure-access/reference-windows-client-release-history)
- [AVD/Windows 365](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-install-windows-client#prerequisites)
- [EDR and AV coexistence with Global Secure Access client](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-edr-antivirus-coexistence)
- Windows 10/11 - Hybrid- or Entra joined
- Local administrator credentials are required to install or upgrade the client
- GSA client is optimized to create the tunnel with nearest deployment based on anycast IP ranges
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
    - ⚠️ Disable all deep packet inspection on network traffic
- **Domain join the connector or not?**
    - AD Kerberos SSO - No domain join required
    - Kerberos constraint delegation (KCD) with app proxy - Domain join required [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors#recommendations-for-the-connector-server)
- **Troubleshooting**
    - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/concept-connectors#connector-deployments-on-hardened-environments)
    - Connector installation fail - Windows firewall blocking outbound traffic for scripts?
- Min. Windows Server 2016
- Focus on CPU and Networking for machine sizing
- Azure and AWS Marketplace offering also available
- Line of sight to destination application needed
- [Multi-geo capabilities](https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-enable-multi-geo)

### 🔒 Entra ID

- Group for PoC users
    - Nested groups are not supported 
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

- Documentation and table of Global Secure Access permissions and roles
    - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/reference-role-based-permissions#role-based-permissions)

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

- Complete list of known limitations
    - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/reference-current-known-limitations?tabs=windows-client)
- Disable DNS over HTTPS (Secure DNS)
    - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check#dns-over-https-not-supported)
- Disable QUIC
    - [Link](https://learn.microsoft.com/en-us/entra/global-secure-access/troubleshoot-global-secure-access-client-diagnostics-health-check#quic-disabled-in-microsoft-edge)
- Guidance on disabling IPv6 on Windows
    - [Link](https://learn.microsoft.com/troubleshoot/windows-server/networking/configure-ipv6-in-windows#:~:text=will%20be%20preferred.-,Disable%20IPv6,-Decimal%20255%0AHexadecimal)
- DNS / NRPT Troubleshooting
    - [Link](https://microsoft.github.io/GlobalSecureAccess/Troubleshooting/WindowsClientTroubleshooting#how-does-dns-work-with-gsa)
