
## Overview

The process of establishing trust between your identity provider (IdP) and Snyk requires a few separate steps, coordinated between your SSO administrator and Snyk Support.

* In your identity provider platform, enter details about the Snyk environment and user attributes.
* Provide Snyk with details from your IdP.
* Set up a user for testing and send Snyk the username and password for that user.
* Use the link provided by Snyk to generate a payload.
* After Snyk finalizes the connection, confirm the login process is working correctly.
* Users are provisioned to Snyk when they log in. If invitation is required, users may only see a list of your Organizations until the admin adds them to the appropriate Organizations.

After SSO is configured both from Snyk and your company's network, a trust relationship is established between Snyk, Auth0 (on behalf of Snyk), and your network. Any sensitive data is encrypted and stored in Auth0 only for the purposes of enabling user logins.

Each type of SSO connection requires different details for establishing the trust between your identity provider and Snyk. The following sections explain those details. The details are also included in the worksheets in the Resources section at the end of this article.

## Use SAML for SSO 
### Please note that these details are updated for the AU instance

To establish trust with Snyk, add an Entity ID, an Assertion Consumer Service (ACS) URL, and a Signing certificate in your identity provider.

* The **Entity ID** is the URL that uniquely identifies Snyk as a SAML entity or service provider. Note: **default Entity ID must be checked** manually as no default is set for this.
* The **Assertion Consumer Service (ACS)** is the endpoint on the Snyk network that listens for requests from your identity provider to enable communication between users on your network and Snyk. This URL is sometimes called a Reply URL.
* The **Signing certificate** is the Snyk certificate, stored on your server, that is needed to maintain the trust relationship. It contains the necessary encryption keys for authentication.

Use these details to set up the connection with your Identity provider (IdP):

| **Details**                                    | **Description**                                                                                                                                                     |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Entity ID (Snyk AU Tenant)             | **urn:auth0:snyk-mt-au-prod-1:saml-service_nsw_                                                                                                            |
| ACS URL (Snyk AU Tenant )             | [https://snyk-mt-au-prod-1.au.auth0.com/login/callback?connection=saml-](https://snyk-mt-au-prod-1.au.auth0.com/login/callback?connection=saml-service_nsw)service_nsw |
| Signing certificate (Snyk AU Tenant ) | [https://snyk-mt-au-prod-1.eu.auth0.com/pem](https://snyk-mt-au-prod-1.eu.auth0.com/pem)                                                                            |

To map information from your Identity provider to Snyk, name your user attributes as follows (using the same capitalization and spelling):

| **Attribute** | **Description**                                 |
| ------------- | ----------------------------------------------- |
| email         | The user email address                          |
| name          | The name of the person to be authenticated      |
| username      | The person’s username for the identity provider |

If your user attributes do not match, note that the Snyk configuration for your SSO will take more time.

## SAML information to provide to Snyk 
### We have the previous information you provided us, if you would like to change any details please feel free to do so 

Obtain the following information from your identity provider. Provide this information to Snyk to establish trust on the service-provider side.

| Information                   | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Sign-in URL                   | The URL for your identity provider sign-in page                                                                                                                                                                                                                                                                                                                                                                                                                             |
| X509 Signing Certificate      | The identity provider public key, encoded in Base64 format                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Sign-out URL                  | <p>Optional, but recommended -</p><p>The URL for redirect whenever a user logs out of Snyk</p>                                                                                                                                                                                                                                                                                                                                                                              |
| User ID attribute             | <p>Optional default is <strong>http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier</strong> <br><strong></strong><br><strong>Important:</strong> This value uniquely identifies Snyk users and if changed will result in a duplicate user being created. If you see a duplicate user after changing identity provider <a href="https://support.snyk.io/hc/en-us/requests/new">submit a request </a>to Snyk support to have the duplicate user removed.</p> |
| Protocol binding              | HTTP-POST is recommended, HTTP-Redirect is also supported                                                                                                                                                                                                                                                                                                                                                                                                                   |
| IdP initiated flow supported? | Idp-initiated flows carry a security risk and are therefore not recommended. Make sure you understand the risks before enabling                                                                                                                                                                                                                                                                                                                                             |
| Email domains and subdomains  | The email domains and subdomains that need access to the SSO                                                                                                                                                                                                                                                                                                                                                                                                                |


## Complete SSO connection

After you set up the connection with your Identity provider and provide the necessary details to Snyk, Snyk sends you a link to generate a payload.

Ignore any error message you see after clicking this link the first time, as Snyk uses the generated payload to complete the configuration.

When Snyk finishes the configuration, the support agent asks you to navigate to the log in page in incognito mode to prevent cookies from interfering with the log in process.

Use [https://app.au.snyk.io/login/sso](https://app.au.snyk.io/login/sso) for logging into your production environment.

To complete your log in:

1. Enter your email address.
2. Select **Continue to provider**.
3. Log in with your identity provider as you would for other applications.
4. Let Snyk Support know which user to promote as the Group administrator.
