**Security Assertion Markup Language (SAML)**
Security Assertion Markup Language (SAML) is an open standard that allows identity providers (IdP) to pass authorization credentials to service providers (SP). What that jargon means is that you can use one set of credentials to log into many different websites. It’s much simpler to manage one login per user than it is to manage separate logins to email, customer relationship management (CRM) software, Active Directory, etc.
BY

SAML transactions use Extensible Markup Language (XML) for standardized communications between the identity provider and service providers. SAML is the link between the authentication of a user’s identity and the authorization to use a service.

SAML enables Single-Sign On (SSO), a term that means users can log in once, and those same credentials can be reused to log into other service providers.

**What is SAML Used For?**
SAML simplifies federated authentication and authorization processes for users, Identity providers, and service providers. SAML provides a solution to allow your identity provider and service providers to exist separately from each other, which centralizes user management and provides access to SaaS solutions.

SAML implements a secure method of passing user authentications and authorizations between the identity provider and service providers. When a user logs into a SAML enabled application, the service provider requests authorization from the appropriate identity provider. The identity provider authenticates the user’s credentials and then returns the authorization for the user to the service provider, and the user is now able to use the application.

SAML authentication is the process of verifying the user’s identity and credentials (password, two-factor authentication, etc.). SAML authorization tells the service provider what access to grant the authenticated user.

**What is a SAML Provider?**
A SAML provider is a system that helps a user access a service they need. There are two primary types of SAML providers, service provider, and identity provider.

A service provider needs the authentication from the identity provider to grant authorization to the user.

An identity provider performs the authentication that the end user is who they say they are and sends that data to the service provider along with the user’s access rights for the service.

Microsoft Active Directory or Azure are common identity providers. Salesforce and other CRM solutions are usually service providers, in that they depend on an identity provider for user authentication.

**SAML 2.0 flow**

Main Roles:
# Client (User, Browser, ...)
# Service provider, Resource Server, ... (SP)
# Identity provider, Authorization Server, ... (IDP)

1. **Client (User)** --access-URL-in-app--> **Service provider (SP)** --App-generate-auth-request--
2. **Service provider (SP)** --HTTP-POST-to-IDP-with-Auth-request--> **Identity provider (IDP)** --Auth-request-is-passed,-verified--
3. **Identity provider (IDP)** --render(send)-login-page-to--> **Client (User)**
4. **Client (User)** --enter-credentials-to-authenticate--> **Identity provider (IDP)** --SAML token is generated--
5. **Identity provider (IDP)** --redirect-to--App-with-SAML-token--> **Service provider (SP)**
6. **Service provider (SP)** --user-is-logged-in-resource-server--> **Client (User)**

Example:
1. user want to login to https://www.youtube.com/ (Youtube is an SP)
2. Youtube then generate an Authentication request and send it with HTTP POST to 
https://accounts.google.com/signin/v2/identifier?service=youtube&uilel=3&passive=true&continue=https%3A%2F%2Fwww.youtube.com%2Fsignin%3Faction_handle_signin%3Dtrue%26app%3Ddesktop%26hl%3Den%26next%3D%252F&hl=en&flowName=GlifWebSignIn&flowEntry=ServiceLogin (so Google is an IDP), Google then verified that Youtube is allowed to single sign on
3. Google render login page to user to enter username, password and login
4. User login by Google account, Google will check the login process, if username, password is correct then generate a SAML token
5. With the SAML token, Google redirect to Youtube URL user requested
6. Youtube confirm that user is logged and allow to access authenticated resource

**Step to test**
1. access http://localhost:8080/spring-security-saml2-sample/
2. checkin https://idp.ssocircle.com  and Start single sign-on
3. browser will send redirect to /idp.ssocircle.com login page
4. login with username and password: dohungcuongdev Cuong@12101995
5. From there checkin "I am not a robot" and click Continue SAML Single Sign on
6. browser will redirect to http://localhost:8080/spring-security-saml2-sample/ and show authenticated information
7. You can enter the address bar the URL http://localhost:8080/spring-security-saml2-sample/ to login again
8. browser will send redirect to /idp.ssocircle.com without login require
9. You can click logout from there

**References**
# What is SAML
https://www.varonis.com/blog/what-is-saml/

#4.2. Installation steps:
https://docs.spring.io/autorepo/docs/spring-security-saml/1.0.x-SNAPSHOT/reference/htmlsingle/#configuration-metadata-sp

# SAML vs OAUTH
https://www.ubisecure.com/uncategorized/difference-between-saml-and-oauth/