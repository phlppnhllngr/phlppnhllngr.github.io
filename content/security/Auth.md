---
title: 'Auth'
parent: Security
---

# Auth
- <https://techblog.bozho.net/simple-things-that-are-actually-hard-user-authentication/>

## Auth Methods
- <https://testdriven.io/blog/web-authentication-methods/>

### Single Sign On (SSO)
- *allows a user to log in with a single ID and password to any of several related, yet independent, software systems*
- <https://www.onelogin.com/learn/how-single-sign-on-works>
- <https://auth0.com/blog/what-is-and-how-does-single-sign-on-work/>
- <https://www.baeldung.com/java-sso-solutions>
  - *Implementing an SSO solution can be performed using either of the two protocols: SAML 2.0, OpenID Connect*
  - *OIDC is the successor to SAML 2.0. Also, it is an extension to OAuth 2.0 protocol used for authentication.*
  - *OIDC is simpler to configure than SAML 2.0.*

### Terminologie
- Service Provider: Applikation
- Identity Provider: Google, ...
- Token: *In SSO, this identity data takes the form of tokens which contain identifying bits of information about the user like a user’s email address or a username.*

### **OAuth(2)**
- *a standardized authorization protocol*
- *a protocol that allows a user to grant limited access to their resources on one site, to another site, without having to expose their credentials.*
- <https://www.csoonline.com/article/3216404/what-is-oauth-how-the-open-authorization-framework-works.html>
  - *an open-standard authorization protocol or framework that describes how unrelated servers and services can safely allow authenticated access to their assets without actually sharing the initial, related, single logon credential. In authentication parlance, this is known as secure, third-party, user-agent, delegated authorization.*
  - *OAuth scenarios almost always represent two unrelated sites or services trying to accomplish something on behalf of users or their software. All three have to work together involving multiple approvals for the completed transaction to get authorized.*
  - *OAuth essentially allows the user, via an authentication provider that they have previously successfully authenticated with, to give another website/service a limited access authentication token for authorization to additional resources.*
  - *Additionally, OAuth 2.0 is a framework, not a protocol (like version 1.0).*
- <https://hackernoon.com/oauth-20-for-dummies>
  - <img loading="lazy" src="https://hackernoon.com/_next/image?url=https%3A%2F%2Fcdn.hackernoon.com%2Fimages%2FBlBIttNGqzO1aF2OOzYkWig7w1V2-3ve2gzk.png&w=828&q=75"/> 
  - *a security standard where you give one application permission to access your data in another application. The steps to grant permission, or consent, are often referred to as authorization or even delegated authorization.*
- <https://darutk.medium.com/the-simplest-guide-to-oauth-2-0-8c71bd9a15bb>

### OpenID Connect
- <https://dexidp.io/docs/openid-connect/>
  - *a flavor of OAuth2* 
  - *OpenID Connect's primary extension of OAuth2 is an additional token returned in the token response called the ID Token. This token is a JSON Web Token signed by the OpenID Connect server, with well known fields for user ID, name, email, etc.*
  - ```
    {
     "access_token": "SlAV32hkKG",
     "token_type": "Bearer",
     "refresh_token": "8xLOxBtZp8",
     "expires_in": 3600,
     "id_token": "eyJhbGciOiJSUzI1NiIsImtpZCI6IjFlOWdkazcifQ.ewogImlzcyI6ICJodHRwOi8vc2VydmVyLmV4YW1wbGUuY29tIiwKICJzdWIiOiAiMjQ4Mjg5NzYxMDAxIiwKICJhdWQiOiAiczZCaGRSa3F0MyIsCiAibm9uY2UiOiAibi0wUzZfV3pBMk1qIiwKICJleHAiOiAxMzExMjgxOTcwLAogImlhdCI6IDEzMTEyODA5NzAKfQ.ggW8hZ1EuVLuxNuuIJKX_V8a_OMXzR0EHR9R6jgdqrOOF4daGU96Sr_P6qJp6IcmD3HP99Obi1PRs-cwh3LO-p146waJ8IhehcwL7F09JdijmBqkvPeB2T9CJNqeGpe-gccMg4vfKjkM8FcGvnzZUN4_KSP0aAp1tOJ1zZwgjxqGByKHiOtX7TpdQyHE5lcMiKPXfEIQILVq0pc_E2DzL7emopWoaoZTF_m0_N0YzFC6g6EJbOEoRoSK5hoDalrcvRYLSrQAZZKflyuVCyixEoV9GfNQC3_osjzw2PAithfubEEBLuVVk4XUVrWOLrLl0nx7RkKU8NXNHq-rvKMzqg"
    }
  ```

  - *Discovery: OpenID Connect servers have a discovery mechanism for OAuth2 endpoints, scopes supported, and indications of various other OpenID Connect features*

## Tools
- **Keycloak**
  - *The Keycloak Server is effectively a large JAX-RS web application deployed in an application server platform that is either Wildfly (Keycloak Community) or JBoss EAP (Red Hat SSO). The web application is served via the embedded Undertow HTTP server.*
  - <https://www.keycloak.org>
  - <https://github.com/thomasdarimont/awesome-keycloak>
  - <https://github.com/keycloak/keycloak-quickstarts>
  - <https://news.ycombinator.com/item?id=31258469>
  - Deployment
    - *Keycloak is a standalone server based in Wildfly. It is not possible to deploy it in other application servers.*
    - es ist/war wohl doch möglich, Keycloak auch auf anderen Servern zu installieren, allerdings schwierig und nicht offiziell dokumentiert: <https://reachmnadeem.wordpress.com/2015/01/14/deploying-keycloak-in-tomcat>
  - <u>Keycloak.X</u>
    - *As part of the Keycloak.X efforts, the underlying platform is to be changed from Wildfly/Undertow to Quarkus/Vertx.* (12/2021))
  - <u>Keycloakify</u>
    - *Customize the look and feel of your login and registration pages without having to mess with FreeMarker.* (-> React)
    - <https://www.keycloakify.dev/>
  - <https://news.ycombinator.com/item?id=36384636>
- **Auth0**
  - *a company that sells an identity management platform with authentication and authorization services that implements the OAuth2 protocol (among others).* 
  - <https://auth0.com> 
- **AWS Cognito**
  - <https://aws.amazon.com/de/cognito/>
- **Gluu**
  - <https://www.gluu.org/>
- **Authelia**
  - *The Single Sign-On Multi-Factor portal for web apps*
  - *an open-source authentication and authorization server providing 2-factor authentication and single sign-on (SSO) for your applications via a web portal. It acts as a companion of reverse proxies like nginx, Traefik or HAProxy to let them know whether queries should pass through. Unauthenticated users are redirected to Authelia Sign-in portal instead.*
  - <https://github.com/authelia/authelia> <img loading="lazy" src="https://img.shields.io/github/stars/authelia/authelia?style=flat-square"/>
- **Okta**
  - *authentication and user management*
  - <https://www.okta.com/>
- **CAS (Central Authentication Service)**
  - *Enterprise Single Sign On*
  - *attempts to be a comprehensive platform for your authentication and authorization needs*
  - .war-File
  - *built upon: Spring Boot and Spring Cloud*
  - *various protocols (saml, oauth, ...), jwt, ldap, Administrative UIs, ...*
  - <https://github.com/apereo/cas> <img loading="lazy" src="https://img.shields.io/github/stars/apereo/cas?style=flat-square"/> 
- **kratos**
  - *Next-gen identity server (think Auth0, Okta, Firebase) with Ory-hardened authentication, MFA, FIDO2, profile management, identity schemas, social sign in, registration, account recovery, and IoT auth. Golang, headless, API-only - without templating or theming headaches.*
  - <https://github.com/ory/kratos>
- **SuperTokens**
  - *alternative to Auth0 / Firebase Auth / AWS Cognito*
  - <https://github.com/supertokens/supertokens-core>
- **ZITADEL**
  - *combines the ease of Auth0 and the versatility of Keycloak*
  - *out of the box features like secure login, self-service, OpenID Connect, OAuth2.x, SAML2, branding, Passwordless with FIDO2, OTP, U2F, and an unlimited audit trail*
  - <https://github.com/zitadel/zitadel>
- **Logto**
  - *A frontend-to-backend identity solution*  
  - *helps you build the sign-in, auth, and user identity within minutes*
  - *We provide an OIDC-based identity service and the end-user experience with username, phone number, email, and social sign-in, for web and native apps.*
  - <https://github.com/logto-io/logto>
- **Casdoor**
  - *An Identity and Access Management (IAM) / Single-Sign-On (SSO) platform with web UI supporting OAuth 2.0, OIDC, SAML and CAS*
  - *A UI-first centralized authentication / Single-Sign-On (SSO) platform based on OAuth 2.0 / OIDC.* 
  - <https://github.com/casdoor/casdoor>
- **Authing**
  - *serves as an identity infrastructure, or Identity As A Service (IDaaS) for cloud computing* 
  - <https://github.com/Authing/Authing>
- **Hanko**
  - *Authentication and user management for the passkey era*
  - *A passkey is a new way to sign in that works completely without passwords. By using the security capabilities of your devices like Touch ID and Face ID, passkeys are way more secure and easier to use than both passwords and all current 2-factor authentication (2FA) methods.* 
  - <https://github.com/teamhanko/hanko> <img loading="lazy" src="https://img.shields.io/github/stars/teamhanko/hanko?style=flat-square"/>
- **Authentik**
  - *open-source Identity Provider that emphasizes flexibility and versatility*
  - *for implementing sign-up, recovery, and other similar features in your application*
  - <https://github.com/goauthentik/authentik>
- **GLAuth**
  - *LDAP authentication server for developers*
  - *Lightweight alternative to OpenLDAP and Active Directory for development, or a homelab.*
  - *Store your user directory in a file, local or in S3; SQL database; or proxy to existing LDAP servers.*
  - <https://github.com/glauth/glauth> <img loading="lazy" src="https://img.shields.io/github/stars/glauth/glauth?style=flat-square"/>
- **dex**
  - *OpenID Connect (OIDC) identity and OAuth 2.0 provider with pluggable connectors*
  - *acts as a portal to other identity providers through "connectors." This lets dex defer authentication to LDAP servers, SAML providers, or established identity providers like GitHub, Google, and Active Directory. Clients write their authentication logic once to talk to dex, then dex handles the protocols for a given backend.*
  - *ID Tokens are an OAuth2 extension introduced by OpenID Connect and dex's primary feature.*
  - <https://github.com/dexidp/dex> <img loading="lazy" src="https://img.shields.io/github/stars/dexidp/dex?style=flat-square"/>
- **SSOReady**
  - *Making SAML SSO painless* 
  - <https://github.com/ssoready/ssoready> <img loading="lazy" src="https://img.shields.io/github/stars/ssoready/ssoready?style=flat-square"/>
  - [Launch HN](https://news.ycombinator.com/item?id=41110850)
- **OAuth2-Proxy**
  - *A reverse proxy and static file server that provides authentication using Providers (Google, Keycloak, GitHub and others) to validate accounts by email, domain or group.* 
  - <https://github.com/oauth2-proxy/oauth2-proxy> <img loading="lazy" src="https://img.shields.io/github/stars/oauth2-proxy/oauth2-proxy?style=flat-square"/>
- **Spring Security OAuth2**
- **OpenAM**
  - <https://github.com/OpenIdentityPlatform/OpenAM> <img loading="lazy" src="https://img.shields.io/github/stars/OpenIdentityPlatform/OpenAM?style=flat-square"/>


## LDAP & AD
- *LDAP (Lightweight Directory Access Protocol) is an application protocol for querying and modifying items in directory service providers like Active Directory, which supports a form of LDAP.*
- *Active Directory (AD) is a database based system that provides authentication, directory, policy, and other services in a Windows environment*
- *LDAP, is a standards based specification for interacting with directory data. Directory Services can implement support of LDAP to provide interoperability among 3rd party applications. Active Directory is Microsoft's implementation of a directory service that, among other protocols, supports LDAP to query it's data.*
- *Active Directory isn't just an implementation of LDAP by Microsoft, that is only a small part of what AD is. Active Directory is (in an overly simplified way) a service that provides LDAP based authentication with Kerberos based Authorization.*
- *LDAP sits on top of the TCP/IP stack and controls internet directory access. It is environment agnostic.*
