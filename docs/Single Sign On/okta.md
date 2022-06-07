---
title: Okta
description: "Configuring Okta as Identity Provider"
slug: /single-sign-on/okta

---

In this document, we'll show you how to use Okta as an Identity provider. This will allow your users to login via Okta and access ZTKA. Below is the list of items that we will cover in this document:

- [Creating a Okta SSO Application](#creating-a-okta-sso-application)
- [Adding an Identity Provider to ZTKA](#adding-an-identity-provider-to-ztka)
- [Verify Login with Okta](#verify-login-with-okta)

## Creating a Okta SSO Application

Login to your Okta account as an admin and navigate to `Applications -> Applications` and **Create a new App Integration**.

In the dialog that opens, choose **OIDC - Open ID Connect** as the **Sign-in Method** and **Web Application** as the **Applicaton Type.**

On the next screen provide a name for the application. Under **Assignments -> Controlled Access**, select `Skip Group Assignment For Now`

<img src="/img/docs/oidc-okta-1.png" alt="Creating New Okta OAuth App" />
Creating New Okta OAuth App

Leave the **Application Callback URL** empty for now and Register the application.

Note down the `client-id` and `client-secret` as those will be required to configure identity provider for ZTKA.

## Adding an Identity Provider to ZTKA

Login to your ZTKA dashboard and navigate to `System -> Identity Providers` and click on **New Identity Provider**

Provide the name of the identity provider and choose IdP type from the drop down. *Incase your identity provider is not in the list, choose Others.*

For client identifier & secret, provide the `client-id` & `client-secret` of the Okta app created earlier.

Under **Scopes** provide `openid, profile, email`

For **Issuer URL**, provide the url for your Okta Account. *For example: https://dev-8830220.okta.com*

<img src="/img/docs/oidc-okta-5.png" alt="Adding new identity provider in ZTKA" />
Adding new identity provider in ZTKA

Click Save & Continue.

From the next screen copy the `Callback URL` and paste it in the callback URL for the Okta OAuth app created in the earlier step.

On the **Mapper Configuration** screen, provide `https://gist.githubusercontent.com/akshay196/34a8223622554bfa065800108d6f1a34/raw/3e96e2c211839f170655334e3d69fedbe9cb4857/okta.jsonnet` as the mapper url.

Click Save & Exit.

At this point, you have successfully added Okta as an identify provider for ZTKA.

## Verify Login with Okta

To confirm if the setup was correct, logout from ZTKA.

On the login screen, you should now see a `Sign In With Okta` button. Click on it to begin the login process using Okta.

<img src="/img/docs/oidc-okta-3.png" alt="Login using Okta" />
Login using Okta

Enter your Okta credentials and login. All the application to access the respective details and sign in.

<img src="/img/docs/oidc-okta-4.png" alt="Login using Okta - providing credentials" />
Login using Okta - providing credentials

Once authenticated, you'll be redirected to ZTKA dashboard.

<img src="/img/docs/oidc-okta-6.png" alt="Redirect to ZTKA" />
Redirect to ZTKA

> Note: Depending on the permission, the user that logs in using Okta might not see the above screen. As an admin, you'll have to configure their group and assign them a project.

Congratulations! You've successfully configured Okta as an identity provider for ZTKA.