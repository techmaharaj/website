---
title: GitHub
description: "Configuring GitHub as Identity Provider"
category: configuration
slug: /single-sign-on/github

---

In this document, we'll show you how to use GitHub as an Identity provider. This will allow your users to login via GitHub and access ZTKA. Below is the list of items that we will cover in this document:


- [Creating a GitHub SSO Application](#creating-a-github-sso-application)
- [Adding an Identity Provider to ZTKA](#adding-an-identity-provider-to-ztka)
- [Verify Login with GitHub](#verify-login-with-github)

## Creating a GitHub SSO Application

Login to your GitHub account and navigate to `Profile -> Settings -> Developer Settings -> OAuth Apps` and **Create a new OAuth App**.

<img src="/img/docs/oidc-github1.png" alt="Creating New GitHub OAuth App" />
Creating New GitHub OAuth App

Provide details like the Name and Description . For homepage url, provide the url to your ZTKA dashboard.
> If you are using this on your local Kind cluster, provide http://console.rafay.local as the value

Leave the **Application Callback URL** empty for now and Register the application.

Note down the `client-id` and `client-secret` as those will be required to configure identity provider for ZTKA.

<img src="/img/docs/oidc-github2.png" alt="GitHub OAuth App Details" />
GitHub OAuth App Details

## Adding an Identity Provider to ZTKA

Login to your ZTKA dashboard and navigate to `System -> Identity Providers` and click on **New Identity Provider**

Provide the name of the identity provider and choose IdP type from the drop down. *Incase your identity provider is not in the list, choose Others.*

For client identifier & secret, provide the `client-id` & `client-secret` of the GitHub app created earlier.

Under **Scopes** provide `user:email`

For **Issuer URL**, provide this url: `https://token.actions.githubusercontent.com`

<img src="/img/docs/oidc-github3.png" alt="Adding new identity provider in ZTKA" />
Adding new identity provider in ZTKA

Click Save & Continue.

From the next screen copy the `Callback URL` and paste it in the callback URL for the GitHub OAuth app created in the earlier step.

<img src="/img/docs/oidc-github4.png" alt="Note down callback URL" />
Callback URL

On the **Mapper Configuration** screen, provide `https://raw.githubusercontent.com/RafayLabs/rcloud-base/main/_kratos/oidc-mappers/github.jsonnet?token=GHSAT0AAAAAABPXWZYYP2YJ62JYWD2WGO3GYUXA4VQ` as the mapper url. Click Save & Exit.

<img src="/img/docs/oidc-github5.png" alt="Add Mapper URL" />
Add Mapper URL

At this point, you have successfully added Github as an identify provider for ZTKA.

<img src="/img/docs/oidc-github6.png" alt="GitHub added as Identity Provider" />
GitHub added as Identity Provider

## Verify Login with GitHub

To confirm if the setup was correct, logout from ZTKA.

On the login screen, you should now see a `Sign In With GitHub` button. Click on it to begin the login process using Github.

<img src="/img/docs/oidc-github7.png" alt="Login using GitHub" />
Login using GitHub

Enter your GitHub credentials and login to GitHub. All the application to access the respective details and sign in.

<img src="/img/docs/oidc-github8.png" alt="Authenticate on GitHub" />
Authenticate on GitHub

Once authenticated, you'll be redirected to ZTKA dashboard.

<img src="/img/docs/oidc-github9.png" alt="Redirect to ZTKA" />
Redirect to ZTKA

> Note: Depending on the permission, the user that logs in using GitHub might not see the above screen. As an admin, you'll have to configure their group and assign them a project.

Congratulations! You've successfully configured GitHub as an identity provider for ZTKA.