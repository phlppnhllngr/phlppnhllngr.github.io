---
tags: [Notebooks/Security]
title: 'Auth'
created: '2019-02-21T15:15:28.438Z'
modified: '2021-09-05T12:01:45.300Z'
parent: Security
---

# Auth

## Auth Methods
- https://testdriven.io/blog/web-authentication-methods/

### Single Sign On
- *allows a user to log in with a single ID and password to any of several related, yet independent, software systems*
- https://www.onelogin.com/learn/how-single-sign-on-works
- https://auth0.com/blog/what-is-and-how-does-single-sign-on-work/


## Tools
- **Keycloak**
  - https://www.keycloak.org
  - https://github.com/thomasdarimont/awesome-keycloak
  - https://github.com/keycloak/keycloak-quickstarts
  - [How to secure your Spring Apps with Keycloak](@attachment/Praesentationen/2019-nn-thomas_darimont-sichere_spring-anwendungen_mit_keycloak-praesentation.pdf)
  - [Easily Secure your Microservices with Keycloak](@attachment/Praesentationen/2019-nn-sebastien_blanc-easily_secure_your_microservices_with_keycloak-praesentation.pdf)
  - deployment
    - *Keycloak is a standalone server based in Wildfly. It is not possible to deploy it in other application servers.*
    - es ist/war wohl doch möglich, keycloak auch auf anderen servern zu installieren, allerdings schwierig und nicht offiziell dokumentiert
      https://reachmnadeem.wordpress.com/2015/01/14/deploying-keycloak-in-tomcat
- **OAuth(2)**
- **AWS Cognito**
  - https://aws.amazon.com/de/cognito/
- **Auth0**
  - https://auth0.com/
- **Gluu**
  - https://www.gluu.org/
- **Authelia**
  - *The Single Sign-On Multi-Factor portal for web apps*
  - *an open-source authentication and authorization server providing 2-factor authentication and single sign-on (SSO) for your applications via a web portal. It acts as a companion of reverse proxies like nginx, Traefik or HAProxy to let them know whether queries should pass through. Unauthenticated users are redirected to Authelia Sign-in portal instead.*
  - https://github.com/authelia/authelia *5.7k
- **vault**
  - *A tool for secrets management, encryption as a service, and privileged access management*
  - *a tool for securely accessing secrets (...) such as API keys, passwords, certificates, and more*
  - https://github.com/hashicorp/vault *20.7k
  - →; spring-cloud-vault
- **Okta**
  - *authentication and user management*
  - https://www.okta.com/
- **CAS (Central Authentication Service)**
  - *Enterprise Single Sign On*
  - *attempts to be a comprehensive platform for your authentication and authorization needs*
  - .war-File
  - *built upon: Spring Boot and Spring Cloud*
  - *various protocols (saml, oauth, ...), jwt, ldap, Administrative UIs, ...*
  - https://github.com/apereo/cas *8.9k
