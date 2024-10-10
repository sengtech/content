# Entra ID External Authentication Methods

### Links
[Microsoft Entra multifactor authentication external method provider reference (Preview)](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-external-method-provider#configure-a-new-external-authentication-provider-with-microsoft-entra-id)<br>
[Manage an external authentication method in Microsoft Entra ID (Preview)](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-authentication-external-method-manage)
[Discovery of provider metadata](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-authentication-external-method-provider#discovery-of-provider-metadata)

> An external identity provider needs to provide an OIDC Discovery endpoint. This endpoint is used to get more configuration data. The full URL, including .well-known/oidc-configuration, must be included in the Discovery URL configured when the EAM is created.
<br>

Discovery of Microsoft Entra ID metadata
Providers also need to retrieve the public keys of Microsoft Entra ID to validate the tokens issued by Microsoft Entra ID.

## Microsoft Entra ID metadata discovery endpoints:

Global Azure<br>
`https://login.microsoftonline.com/common/v2.0/.well-known/openid-configuration`
<br>

## EAMs are implemented on top of Open ID Connect (OIDC). This implementation requires at least three publicly facing endpoints:

- An OIDC Discovery endpoint, as described in Discovery of provider metadata
- A valid OIDC authentication endpoint
- A URL where the public certificates of the provider are published
