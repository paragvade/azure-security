- Identity is new security perimeter 

### Need for Identity
- Any service should be able to apply Principle of least prrivilege - it involves granting certain actions (roles) to certain security principle at a defined scope ('Role assignment'). For this, every security princial should be uniquely identifiable. A centeal store of identities is required for this. 

<img width="895" height="986" alt="Entra" src="https://github.com/user-attachments/assets/a697a8a7-0365-4fbc-b337-69d1608457e1" />


### Decentralized Identities
- Puts user in the center instead of IdP. Not a mainstream method but ganing more traction. 
- In traditional identity model, identity provider is centralized. All identities are stored in a central directory (e.g. Active Directory). This creates challenges in scenarios like cross-org collaboration, user privacy, data ownership, etc.
- Decentralized identity model solves this by allowing users to own and control their identities without relying on a central authority. Users can create and manage their own digital identities, which can be verified by multiple parties.
- Decentralized identities use technologies like **blockchain and cryptographic proofs** to ensure security and trustworthiness. Users can share specific attributes of their identity without revealing unnecessary personal information, enhancing privacy and control.
- Use cases- cross org collaboration, supply chain management, education credentials verification, healthcare data sharing, etc.


# Entra ID
- For most use cases today, central IdP is still needed. And Entra ID is most widely used. It stores identities for users, computers, applications, groups. 
- Earlier called Azure AD - not a correct name. Because it was not cloud equivalent of traditional on-prem Active Directory, but had completely different mechanism.
- All Microsoft accounts- Azure, M365, Dynamics 365 MUST have an entra tenant
- Traditional Active Directory (AD) - ADDS (Active Directory Domain Services)
    - Identity services for closed network and its devices
    - Used Kerberos/NTLM/LDAP
    - Had hierarchical structures in the form of OUs (Organization Units) - 
    - ADFS (Active Directory Federation Services)-

- Entra ID
    - Speaks language of cloud for auth- TLS encryption over HTTP (HTTPS), OIDC for authentication, OAuth2 for authorisation, SAML for SSO, Microsoft Graph
    - No OUs. Flat hierarchy. But use..
    - Entra SKUs - Free, P1, P2.

