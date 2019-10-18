## Tutorial

[Auth0 Vue Login Example](https://auth0.com/docs/quickstart/spa/vuejs/02-calling-an-api)

## Project setup

```bash
npm install
```

### Configuration

The project needs to be configured with your Auth0 domain and client ID in order for the authentication flow to work.

To do this, replace the values within `auth_config.json` with your own Auth0 application credentials:

```json
{
  "domain": "<YOUR AUTH0 DOMAIN>",
  "audience": "<YOUR AUTH0 API IDENTIFIER>",
  "clientId": "<YOUR AUTH0 CLIENT ID>"
}
```

Also change the `external_api_config.json` with your own external API endpoint pattern

```json
{
  "url": "<YOUR API ENDPOINT PATTERN>"
}
```

### Running in development

This compiles and serves the Vue app, and starts the backend API server on port 3001:

```bash
npm run dev
```

## Deployment

### Compiles and minifies for production

```bash
npm run build

```

### Docker build

To build the Docker image run `exec.sh`, or `exec.ps1` on Windows.

### Run your tests

```bash
npm run test
```

### Lints and fixes files

```bash
npm run lint
```

## What is Auth0?

Auth0 helps you to:

- Add authentication with [multiple authentication sources](https://docs.auth0.com/identityproviders), either social like **Google, Facebook, Microsoft Account, LinkedIn, GitHub, Twitter, Box, Salesforce, among others**, or enterprise identity systems like **Windows Azure AD, Google Apps, Active Directory, ADFS or any SAML Identity Provider**.
- Add authentication through more traditional **[username/password databases](https://docs.auth0.com/mysql-connection-tutorial)**.
- Add support for **[linking different user accounts](https://docs.auth0.com/link-accounts)** with the same user.
- Support for generating signed [Json Web Tokens](https://docs.auth0.com/jwt) to call your APIs and **flow the user identity** securely.
- Analytics of how, when and where users are logging in.
- Pull data from other sources and add it to the user profile, through [JavaScript rules](https://docs.auth0.com/rules).

## Create a Free Auth0 Account

1. Go to [Auth0](https://auth0.com/signup) and click Sign Up.
2. Use Google, GitHub or Microsoft Account to login.