## Passkeys in Microsoft Entra ID

### Required Entra ID roles for configuration

[Link](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-plan-prerequisites-phishing-resistant-passwordless-authentication#required-roles)

### Number of authentication methods

Users should have at least two authentication methods registered. With another method registered, the user has a backup method available if something happens to their primary method, like when a device is lost or stolen. For example, it's a good practice for users to have passkeys registered both on their phone, and locally on their workstation in Windows Hello for Business.

### Passkeys are MFA, Passwordless and Phishing-resistant

They count as something that a user has (physical device or security key) and something the user knows or is, like a biometric or PIN.

### Types of passkeys

- Device bound
    - Cannot leave the issued device, and cannot be synced across devices
    - Pros
        - Higher level of security and assurance (compared to syncable passkeys)
    - Cons
        - A more difficult recovery process
- Syncable
    - Synced between a user's various devices. The passkeys are stored securely with a password or credential manager such as Apple Passwords, Google Password Manager, 1Password, Dashlane or LastPass. Users can access synced passkeys across many of their devices, even new ones, without having to re-enroll every device on every account.
    - Pros
        - Better user exeperience
        - Easy recovery process
    - Cons
        - Synced Passkeys are easy to share (e.g. Airdrop), and could be stored in a private consumer cloud services, which could raise questions regarding work credentials.

### Microsoft Entra ID offers the following phishing-resistant passwordless authentication options

- Windows Hello for Business
- Platform credential for macOS (preview)
- Microsoft Authenticator app passkeys (preview)
- FIDO2 security keys
- Other passkeys and providers, such as iCloud Keychain - [***on roadmap***](https://techcommunity.microsoft.com/t5/microsoft-entra-blog/public-preview-expanding-passkey-support-in-microsoft-entra-id/ba-p/4062702)

### Enable passkeys in Microsoft Authenticator

- [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-authenticator-passkey)
- Settings
    - Allow self-service set up: Yes
    - Enforce attestation: Yes
    - Enforce key restrictions: Yes
    - Restrict specific keys: Allow
        - Add Microsoft Authenticator (Preview), and existing AAGUID

### User Onboarding

- Microsoft recommends that users sign in to Microsoft Authenticator directly to bootstrap a passkey in the app.
- Users can use their TAP to sign into Microsoft Authenticator directly on their iOS or Android device.

### Attestation

- Microsoft Entra ID tries to verify the legitimacy of the passkey being created. When the user is registering a passkey in the Authenticator, attestation verifies that the legitimate Microsoft Authenticator app created the passkey by using Apple and Google service.
- iOS Authentication
    - [iOS App Attest service](https://developer.apple.com/documentation/devicecheck/preparing-to-use-the-app-attest-service)
- Android
    - [Play Integrity API](https://developer.android.com/google/play/integrity/overview)
    - [Key attestation by Android](https://developer.android.com/privacy-and-security/security-key-attestation)

### Find AAGUIDs

- Microsoft Graph PowerShell script | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-authenticator-passkey#find-aaguids)

### Workarounds

- [Authentication strength Conditional Access policy loop | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-support-authenticator-passkey#workarounds-for-an-authentication-strength-conditional-access-policy-loop)
- [Users who can't register passkeys because of Require approved client app or Require app protection policy Conditional Access grant controls](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-support-authenticator-passkey#workarounds-for-users-who-cant-register-passkeys-because-of-require-approved-client-app-or-require-app-protection-policy-conditional-access-grant-controls)

### Upcoming changes

- [MC920300 - Microsoft Entra: Enablement of Passkeys in Authenticator for passkey (FIDO2) organizations with no key restrictions](https://mc.merill.net/message/MC920300)

### Notes

- B2B collaboration users
    - Registration of passkey (FIDO2) credentials isn't supported for B2B collaboration users in the resource tenant | [Link](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#b2b-collaboration-users)

### Links

[Enable passkey (FIDO2) authentication method | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-passkey-fido2#enable-passkey-fido2-authentication-method)

[FIDO2 security keys eligible for attestation with Microsoft Entra ID | Microsoft Learn](https://learn.microsoft.com/en-us/entra/identity/authentication/how-to-enable-passkey-fido2)

[Passkey (FIDO2) authentication matrix with Microsoft Entra ID](https://learn.microsoft.com/en-us/entra/identity/authentication/concept-fido2-compatibility)
