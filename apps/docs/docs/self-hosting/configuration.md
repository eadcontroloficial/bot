---
sidebar_position: 2
---

import { SponsorButton } from '../../src/js/SponsorButton.jsx'
import { Asterix } from '../../src/js/Asterix.jsx'

# Configuration

Parameters marked with <Asterix/> are required.

## General

| Parameter                            | Default | Description                                                                                                                                                                                                                                 |
| ------------------------------------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DATABASE_URL <Asterix/>              |         | The database URL                                                                                                                                                                                                                            |
| ENCRYPTION_SECRET <Asterix/>         |         | A 256-bit key used to encrypt sensitive data. It is strongly recommended to [generate](https://www.allkeysgenerator.com/Random/Security-Encryption-Key-Generator.aspx) a new one. The secret should be the same between builder and viewer. |
| NEXTAUTH_URL <Asterix/>              |         | The builder base URL. Should be the publicly accessible URL (i.e. `https://typebot.domain.com`)                                                                                                                                             |
| NEXT_PUBLIC_VIEWER_URL <Asterix/>    |         | The viewer base URL. Should be the publicly accessible URL (i.e. `https://bot.domain.com`)                                                                                                                                                  |
| ADMIN_EMAIL                          |         | The email that will get an `UNLIMITED` plan on user creation. The associated user will be able to bypass database rules.                                                                                                                    |
| NEXTAUTH_URL_INTERNAL                |         | The internal builder base URL. You have to set it only when `NEXTAUTH_URL` can't be reached by your builder container / server. For a docker deployment, you should set it to `http://localhost:3000`.                                      |
| DEFAULT_WORKSPACE_PLAN               | FREE    | Default workspace plan on user creation or when a user creates a new workspace. Possible values are `FREE`, `STARTER`, `PRO`, `LIFETIME`, `UNLIMITED`. The default plan for admin user is `UNLIMITED`                                       |
| DISABLE_SIGNUP                       | false   | Disable new user sign ups. Invited users are still able to sign up.                                                                                                                                                                         |
| NEXT_PUBLIC_ONBOARDING_TYPEBOT_ID    |         | Typebot ID used for the onboarding. Onboarding page is skipped if not provided.                                                                                                                                                             |
| DEBUG                                | false   | If enabled, the server will print valuable logs to debug config issues.                                                                                                                                                                     |
| NEXT_PUBLIC_BOT_FILE_UPLOAD_MAX_SIZE |         | Limits the size of each file that can be uploaded in the bots (i.e. Set `10` to limit the file upload to 10MB)                                                                                                                              |

## Email (Auth, notifications)

Used for sending email notifications and authentication

| Parameter             | Default | Description                                                                                                                                                                                                                                                |
| --------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SMTP_USERNAME         |         | SMTP username                                                                                                                                                                                                                                              |
| SMTP_PASSWORD         |         | SMTP password                                                                                                                                                                                                                                              |
| SMTP_HOST             |         | SMTP host. (i.e. `smtp.host.com`)                                                                                                                                                                                                                          |
| SMTP_PORT             | 25      | SMTP port                                                                                                                                                                                                                                                  |
| NEXT_PUBLIC_SMTP_FROM |         | From name and email (i.e. `'Typebot Notifications' <notifications@host.com>`)                                                                                                                                                                              |
| SMTP_SECURE           | false   | If true the connection will use TLS when connecting to server. If false (the default) then TLS is used if server supports the STARTTLS extension. In most cases set this value to true if you are connecting to port 465. For port 587 or 25 keep it false |
| SMTP_AUTH_DISABLED    | false   | To disable the authentication by email but still use the provided config for notifications                                                                                                                                                                 |

## Google (Auth, Sheets, Fonts)

Used authentication in the builder and for the Google Sheets integration step. Make sure to set the required scopes (`userinfo.email`, `spreadsheets`, `drive.readonly`) in your console
The Authorization callback URL should be `$NEXTAUTH_URL/api/auth/callback/google`

| Parameter            | Default | Description                                   |
| -------------------- | ------- | --------------------------------------------- |
| GOOGLE_CLIENT_ID     |         | The Client ID from the Google API Console     |
| GOOGLE_CLIENT_SECRET |         | The Client secret from the Google API Console |

Used for Google Fonts (Optional):

| Parameter                  | Default | Description                             |
| -------------------------- | ------- | --------------------------------------- |
| NEXT_PUBLIC_GOOGLE_API_KEY |         | The API Key from the Google API Console |

### Configuration

https://console.developers.google.com/apis/credentials

The "Authorized redirect URIs" used when creating the credentials must include your full domain and end in the callback path:

- For production:
  - https://{YOUR_DOMAIN}/api/auth/callback/google
  - https://{YOUR_DOMAIN}/api/credentials/google-sheets/callback
- For development:
  - http://localhost:3000/api/auth/callback/google
  - http://localhost:3000/api/credentials/google-sheets/callback

## GitHub (Auth)

Used for authenticating with GitHub. By default, it uses the credentials of a Typebot-dev app.

You can create your own GitHub OAuth app [here](https://github.com/settings/developers). The Authorization callback URL should be `$NEXTAUTH_URL/api/auth/callback/github`

| Parameter            | Default | Description                                                                 |
| -------------------- | ------- | --------------------------------------------------------------------------- |
| GITHUB_CLIENT_ID     |         | Application client ID. Also used to check if it is enabled in the front-end |
| GITHUB_CLIENT_SECRET |         | Application secret                                                          |

## GitLab (Auth)

Used for authenticating with GitLab.
Follow the official GitLab guide for creating OAuth2 applications [here](https://docs.gitlab.com/ee/integration/oauth_provider.html).
The Authorization callback URL should be `$NEXTAUTH_URL/api/auth/callback/gitlab`

| Parameter              | Default            | Description                                                                          |
| ---------------------- | ------------------ | ------------------------------------------------------------------------------------ |
| GITLAB_CLIENT_ID       |                    | Application client ID. Also used to check if it is enabled in the front-end          |
| GITLAB_CLIENT_SECRET   |                    | Application secret                                                                   |
| GITLAB_BASE_URL        | https://gitlab.com | Base URL of the GitLab instance                                                      |
| GITLAB_REQUIRED_GROUPS |                    | Comma-separated list of groups the user has to be a direct member of, e.g. `foo,bar` |
| GITLAB_NAME            | GitLab             | Name of the GitLab instance, used for the SSO Login Button                           |

## Facebook (Auth)

You can create your own Facebook OAuth app [here](https://developers.facebook.com/apps/create/).
The Authorization callback URL should be `$NEXTAUTH_URL/api/auth/callback/facebook`

| Parameter              | Default | Description                                                                 |
| ---------------------- | ------- | --------------------------------------------------------------------------- |
| FACEBOOK_CLIENT_ID     |         | Application client ID. Also used to check if it is enabled in the front-end |
| FACEBOOK_CLIENT_SECRET |         | Application secret                                                          |

## Azure AD (Auth)

If you are using [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) for the authentication you can set the following environment variables.
The Authorization callback URL should be `$NEXTAUTH_URL/api/auth/callback/azure-ad`

| Parameter              | Default | Description                                                   |
| ---------------------- | ------- | ------------------------------------------------------------- |
| AZURE_AD_CLIENT_ID     |         | Application client ID                                         |
| AZURE_AD_CLIENT_SECRET |         | Application client secret. Can be obtained from Azure Portal. |
| AZURE_AD_TENANT_ID     |         | Azure Tenant ID                                               |

## Custom OAuth Provider (Auth)

| Parameter                    | Default              | Description                                                                             |
| ---------------------------- | -------------------- | --------------------------------------------------------------------------------------- |
| CUSTOM_OAUTH_NAME            | Custom OAuth         | Provider name. Will be displayed in the sign in form.                                   |
| CUSTOM_OAUTH_CLIENT_ID       |                      | OAuth client ID.                                                                        |
| CUSTOM_OAUTH_CLIENT_SECRET   |                      | OAuth client secret.                                                                    |
| CUSTOM_OAUTH_WELL_KNOWN_URL  |                      | OAuth .well-known URL (i.e. `https://auth.domain.com/.well-known/openid-configuration`) |
| CUSTOM_OAUTH_USER_ID_PATH    | id                   | Used to map the id from the user info object                                            |
| CUSTOM_OAUTH_USER_NAME_PATH  | name                 | Used to map the name from the user info object                                          |
| CUSTOM_OAUTH_USER_EMAIL_PATH | email                | Used to map the email from the user info object                                         |
| CUSTOM_OAUTH_USER_IMAGE_PATH | image                | Used to map the image from the user info object                                         |
| CUSTOM_OAUTH_SCOPE           | openid profile email | OAuth scope                                                                             |

For `*_PATH` parameters, you can use dot notation to access nested properties (i.e. `account.name`).

## S3 Storage (Media uploads)

Used for uploading images, videos, etc... It can be any S3 compatible object storage service (Minio, Digital Oceans Space, AWS S3...)

| Parameter               | Default | Description                                                                        |
| ----------------------- | ------- | ---------------------------------------------------------------------------------- |
| S3_ACCESS_KEY           |         | S3 access key. Also used to check if upload feature is enabled                     |
| S3_SECRET_KEY           |         | S3 secret key.                                                                     |
| S3_BUCKET               | typebot | Name of the bucket where assets will be uploaded in.                               |
| S3_PORT                 |         | S3 Host port number                                                                |
| S3_ENDPOINT             |         | S3 endpoint (i.e. `s3.domain.com`).                                                |
| S3_SSL                  | true    | Use SSL when establishing the connection.                                          |
| S3_REGION               |         | S3 region.                                                                         |
| S3_PUBLIC_CUSTOM_DOMAIN |         | If the final URL that is used to read public files is different from `S3_ENDPOINT` |

Note that for AWS S3, your endpoint is usually: `s3.<S3_REGION>.amazonaws.com`

In order to function properly, your S3 bucket must be configured. Make sure to read through the [S3 configuration](./guides/s3) doc.

## Giphy (GIF picker)

Used to search for GIF. You can create a Giphy app [here](https://developers.giphy.com/dashboard/)

| Parameter                 | Default | Description   |
| ------------------------- | ------- | ------------- |
| NEXT_PUBLIC_GIPHY_API_KEY |         | Giphy API key |

## Unsplash (image picker)

Used to search for images. You can create a Giphy app [here](https://unsplash.com/developers)

| Parameter                       | Default | Description       |
| ------------------------------- | ------- | ----------------- |
| NEXT_PUBLIC_UNSPLASH_APP_NAME   |         | Unsplash App name |
| NEXT_PUBLIC_UNSPLASH_ACCESS_KEY |         | Unsplash API key  |

## WhatsApp (Preview)

In order to be able to test your bot on WhatsApp from the Preview drawer, you need to set up a WhatsApp business app.

<details><summary><h4>Requirements</h4></summary>
<p>

## 1. [Create a WhatsApp Meta app](../embed/whatsapp/create-meta-app)

## 2. Get the System User token

1. Go to your [System users page](https://business.facebook.com/settings/system-users) and create a new system user that has access to the related.

- Token expiration: `Never`
- Available Permissions: `whatsapp_business_messaging`, `whatsapp_business_management`

2. The generated token will be used as `META_SYSTEM_USER_TOKEN` in your viewer configuration.
3. Click on `Add assets`. Under `Apps`, look for your app, select it and check `Manage app`

## 3. Get the phone number ID

1. Go to your WhatsApp Dev Console

<img src="/img/whatsapp/dev-console.png" alt="WhatsApp dev console" />

2. Add your phone number by clicking on the `Add phone number` button.
3. Select the newly created phone number in the `From` dropdown list and you will see right below the associated `Phone number ID` This will be used as `WHATSAPP_PREVIEW_FROM_PHONE_NUMBER_ID` in your viewer configuration.

## 4. Set up the webhook

1. Head over to `Quickstart > Configuration`. Edit the webhook URL to `$NEXTAUTH_URL/api/v1/whatsapp/preview/webhook`. Set the Verify token to `$ENCRYPTION_SECRET` and click on `Verify and save`.
2. Add the `messages` webhook field.

## 5. Set up the message template

1. Head over to `Messaging > Message Templates` and click on `Create Template`
2. Select the `Utility` category
3. Give it a name that corresponds to your `WHATSAPP_PREVIEW_TEMPLATE_NAME` configuration.
4. Select the language that corresponds to your `WHATSAPP_PREVIEW_TEMPLATE_LANG` configuration.
5. You can format it as you'd like. The user will just have to send a message to start the preview.

</p></details>

| Parameter                             | Default | Description                                             |
| ------------------------------------- | ------- | ------------------------------------------------------- |
| META_SYSTEM_USER_TOKEN                |         | The system user token used to send WhatsApp messages    |
| WHATSAPP_PREVIEW_FROM_PHONE_NUMBER_ID |         | The phone number ID from which the message will be sent |
| WHATSAPP_PREVIEW_TEMPLATE_NAME        |         | The preview start template message name                 |
| WHATSAPP_PREVIEW_TEMPLATE_LANG        | en      | The preview start template message name                 |

## Others

<details><summary><h3>Show</h3></summary>
<p>

The [official Typebot managed service](https://app.typebot.io/) uses other services such as [Stripe](https://stripe.com/) for processing payments, [Sentry](https://sentry.io/) for tracking bugs and [Sleekplan](https://sleekplan.com/) for user feedbacks.

The related environment variables are listed here but you are probably not interested in these if you self-host Typebot.

<details><summary><h4>Stripe</h4></summary>
<p>

| Parameter                               | Default | Description                                 |
| --------------------------------------- | ------- | ------------------------------------------- |
| NEXT_PUBLIC_STRIPE_PUBLIC_KEY           |         | Stripe public key                           |
| STRIPE_SECRET_KEY                       |         | Stripe secret key                           |
| STRIPE_STARTER_PRODUCT_ID               |         | Starter plan product ID                     |
| STRIPE_STARTER_MONTHLY_PRICE_ID         |         | Starter monthly plan price id               |
| STRIPE_STARTER_YEARLY_PRICE_ID          |         | Starter yearly plan price id                |
| STRIPE_PRO_PRODUCT_ID                   |         | Pro plan product ID                         |
| STRIPE_PRO_MONTHLY_PRICE_ID             |         | Pro monthly plan price id                   |
| STRIPE_PRO_YEARLY_PRICE_ID              |         | Pro yearly plan price id                    |
| STRIPE_STARTER_CHATS_MONTHLY_PRICE_ID   |         | Starter Additional chats monthly price id   |
| STRIPE_STARTER_CHATS_YEARLY_PRICE_ID    |         | Starter Additional chats yearly price id    |
| STRIPE_PRO_CHATS_MONTHLY_PRICE_ID       |         | Pro Additional chats monthly price id       |
| STRIPE_PRO_CHATS_YEARLY_PRICE_ID        |         | Pro Additional chats yearly price id        |
| STRIPE_STARTER_STORAGE_MONTHLY_PRICE_ID |         | Starter Additional storage monthly price id |
| STRIPE_STARTER_STORAGE_YEARLY_PRICE_ID  |         | Starter Additional storage yearly price id  |
| STRIPE_PRO_STORAGE_MONTHLY_PRICE_ID     |         | Pro Additional storage monthly price id     |
| STRIPE_PRO_STORAGE_YEARLY_PRICE_ID      |         | Pro Additional storage yearly price id      |
| STRIPE_WEBHOOK_SECRET                   |         | Stripe Webhook secret                       |

</p></details>

<details><summary><h4>Sentry</h4></summary>
<p>

| Parameter              | Default | Description                            |
| ---------------------- | ------- | -------------------------------------- |
| NEXT_PUBLIC_SENTRY_DSN |         | Sentry DSN                             |
| SENTRY_AUTH_TOKEN      |         | Used to upload sourcemaps on app build |
| SENTRY_PROJECT         |         | Sentry project name                    |
| SENTRY_ORG             |         | Sentry organization name               |

These can also be added to the `viewer` environment

</p></details>

<details><summary><h4>Vercel (custom domains)</h4></summary>
<p>

| Parameter                              | Default | Description                                     |
| -------------------------------------- | ------- | ----------------------------------------------- |
| VERCEL_TOKEN                           |         | Vercel API token                                |
| NEXT_PUBLIC_VERCEL_VIEWER_PROJECT_NAME |         | The name of the viewer project in Vercel        |
| VERCEL_TEAM_ID                         |         | Vercel team ID that contains the viewer project |

</p></details>

<details><summary><h4>Sleekplan</h4></summary>
<p>

| Parameter         | Default | Description                                                              |
| ----------------- | ------- | ------------------------------------------------------------------------ |
| SLEEKPLAN_SSO_KEY |         | Sleekplan SSO key used to automatically authenticate a user in Sleekplan |

</p></details>

<details><summary><h4>Telemetry</h4></summary>
<p>

| Parameter                      | Default | Description                                                                                                     |
| ------------------------------ | ------- | --------------------------------------------------------------------------------------------------------------- |
| TELEMETRY_WEBHOOK_URL          |         | Webhook URL called whenever a new telemetry event is captured. See this file that lists all the possible events |
| TELEMETRY_WEBHOOK_BEARER_TOKEN |         | Bearer token to add if the request needs to be authenticated                                                    |

</p></details>

<details><summary><h4>PostHog</h4></summary>
<p>

| Parameter                    | Default                 | Description      |
| ---------------------------- | ----------------------- | ---------------- |
| NEXT_PUBLIC_POSTHOG_API_KEY  |                         | PostHog API Key  |
| NEXT_PUBLIC_POSTHOG_API_HOST | https://app.posthog.com | PostHog API Host |

</p></details>

</p></details>

:::note
If you're self-hosting Typebot, [sponsoring me](https://github.com/sponsors/baptisteArno) is a great way to give back to the community and to contribute to the long-term sustainability of the project.

<SponsorButton />

Thank you for supporting independent creators of Free Open Source Software!
:::
