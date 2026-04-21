# SSO - Azure Entra ID

In this article, we will look at how to set up Azure AD so that it can be used as an external identity provider for Subscription Manager, allowing single sign-on capability between Azure AD and Subscription Manager.

## Register application

Start by registering a new application in Azure AD by following [these](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app) instructions.

## Copy application (client) ID

Immediately after registering your application, an overview page will be opened for the new application. A unique application (client) ID would have been assigned to the application.

> [!WARNING]
> Copy this ID. You will add it in Subscription Manager's _web.config_ file shortly.

![Copy application client ID](../images/copy-client-id.png)

## Credentials

Next, create a secret for Subscription Manager. Follow the steps below:

1. On the left, click on _Certificates & secrets._
2. Click on _New client secret._
3. Add a description for your new client secret.
4. Choose a duration.
5. Click _Add._
6. Copy the value of the newly generated secret and store it safely for later use.

![Add secret step 1](../images/add-secret-1-1.png)

![Add secret step 2](../images/add-secret-2-2.png)

> [!WARNING]
> Both the application client ID and the secret need to be added to Subscription Manager's _web.config_ file. You will not be able to retrieve the secret once the page has been closed. Make sure to copy and safely store the secret before the page is closed, or you will need to repeat the previous steps.

1. On the left, click _Token Configuration_.
2. Click _Add Optional Claim_.
3. Select the _ID_ token type.
4. Select _upn_ from the list of claims.
5. Click Add
6. Click '...'  -> Edit
7. Set 'Externally authenticated' to Yes
8. Save
9. Open the app _Manifest_.
10. Set _"acceptMappedClaims": true (applies from v4.4.19+)_
11. Navigate to the IIS location where Subscription Manager has been installed.
12. Open the file _web.config_ file.
13. Scroll down to the "_xmpro_" section.

> [!NOTE]
> This section might have to be decrypted, for which you can find instructions [here](https://docs.xmpro.com/knowledge-base-2/how-to-encrypt-and-decrypt-a-web-config-file/).

1. Add the application (client) ID that you copied earlier to the `clientId` attribute of the `azureAD` element
2. Copy the secret and add it to the _web.config_.

![Azure AD web config clientId and key](../images/sso-azuread-web-config-clientid-and-key.png)

> [!NOTE]
> If you're using the Azure key store to manage app settings and secrets, use the `${}` syntax for the azureAD attributes in the _web.config_, similar to:
> `<azureAD clientId="${ADClientID}" key="${ADSecret}" />`

1. And define the following secrets in the key store:

| **Name** | **Value** |
| --- | --- |
| ADClientID | Application Id |
| ADSecret | Application Secret |

## Authentication

1. Copy the baseUrl value in the _web.config_ - you will need it later in this guide.

![Azure AD web config baseUrl](../images/sso-azuread-web-config-baseurl.png)

1. In Azure Portal, click on _Authentication_ and add the following URL in the space provided:

* The URL where Subscription Manager is hosted (base URL, which you have just copied), ending in "_identity/signin-azuread_"

  Example: _<https://mysampleserver/xmprosubscriptionmanager/identity/signin-azuread>_

![Authentication configuration](../images/authentication-4.png)

1. On the Authentication page, scroll down until you see "_Advanced Settings_".
2. Select "_ID tokens_" and click _Save_.

![Authentication advanced settings](../images/authentication-advanced-settings.png)

## API permissions

1. Select _API permissions_ on the left-hand menu.
2. Make sure the permissions set on the application correspond to the image below.

![API permissions configuration](../images/permissions-1.png)

## Sync Azure AD Role to SM's Business Role

This optional functionality allows a user's Business Role to be synced to a corresponding Azure AD Claim each time they log in.

1. Get the desired user claim name from Azure AD.
2. Navigate to the IIS location where Subscription Manager has been installed.
3. Open the _web.config_ file.
4. Add the claim name to the "businessRoleClaim" attribute in the "identityProviders" tag.
   `<identityProviders businessRoleClaim="PUT THE CLAIM NAME HERE">`
5. Save the file and restart the Subscription Manager service.

[See the Sync Business Roles from Azure Entra ID article for more information](../concepts/manage-access.md#sync-business-roles-from-azure-entra-id).

## Guest User access across Tenants

When your Azure AD is in a different Tenant to Subscription Manager and the User has Guest membership in Azure AD, then add the TenantID for Azure AD.

![Azure AD web config guest tenant](../images/sso-azuread-web-config-guest-tenant.png)
