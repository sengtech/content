# Microsoft Entra Password Protection - Deployment Guide

### Reference material

[Enforce on-premises Microsoft Entra Password Protection for Active Directory Domain Services](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-password-ban-bad-on-premises)

[Plan and deploy on-premises Microsoft Entra Password Protection](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-deploy)

---

### Prerequisites

[Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-deploy#deployment-requirements)

- All machines, including domain controllers, that have Microsoft Entra Password Protection components installed must have the Universal C Runtime installed.
- An account that has Active Directory domain administrator privileges in the forest root domain to register the Windows Server Active Directory forest with Microsoft Entra ID.
- Network connectivity must exist between at least one domain controller in each domain and at least one server that hosts the proxy service for Microsoft Entra Password Protection. This connectivity must allow the domain controller to access RPC endpoint mapper port 135 and the RPC server port on the proxy service.
    - By default, the RPC server port is a dynamic RPC port from the range (49152 - 65535), but it can be configured to use a static port.
- **DC Agent**
    - .NET 4.7.2
    - Must use Distributed File System Replication (DFSR) for sysvol replication.

---

### Deployment steps

- Download required software | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-deploy#download-required-software)
- Install and configure the proxy service | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-deploy#install-and-configure-the-proxy-service)
- Install the DC agent service | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-deploy#install-the-dc-agent-service)
- Enable on-premises Microsoft Entra Password Protection | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/howto-password-ban-bad-on-premises-operations)
- Configure custom banned passwords for Microsoft Entra password protection | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/tutorial-configure-custom-password-protection)

---

### Modes

- **Audit**
- **Enforce**

Audit mode is the default initial setting, where passwords can continue to be set. Passwords that would be blocked are recorded in the event log. After you deploy the proxy servers and DC agents in audit mode, monitor the impact that the password policy will have on users when the policy is enforced.

---

### HA

- The main concern for password protection is the availability of Microsoft Entra Password Protection proxy servers when the DCs in a forest try to download new policies or other data from Azure. Each Microsoft Entra Password Protection DC agent uses a simple round-robin-style algorithm when deciding which proxy server to call. The agent skips proxy servers that aren't responding.
- For most fully connected Active Directory deployments that have healthy replication of both directory and sysvol folder state, two Microsoft Entra Password Protection proxy servers is enough to ensure availability.

---

### Incremental deployment

- Microsoft Entra Password Protection supports partial deployment. The DC agent software on a given DC actively validates passwords even when other DCs in the domain don't have the DC agent software installed. Partial deployments of this type aren't secure and aren't recommended other than for testing purposes.

---

### Notes

- **Important -** Microsoft Entra Password Protection can only validate passwords during password change or set operations. Passwords that were accepted and stored in Active Directory prior to the deployment of Microsoft Entra Password Protection will never be validated and will continue working as-is.
- **Multiple forest considerations** - There are ***no*** additional requirements to deploy Microsoft Entra Password Protection across multiple forests.
- **RODS -** You don't have to install the Microsoft Entra Password Protection DC agent software on RODCs.
