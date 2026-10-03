VaultPay API: Authentication

1. Overview

The VaultPay API uses API keys transmitted as Bearer tokens for authentication. Authenticated requests must include a valid "Authorization" header.

Requests without a key, or with an invalid or revoked key, return a "401 Unauthorized" error.

2. Obtaining an API Key

To obtain an API key:

1. Log in to the VaultPay developer dashboard.
2. Generate an API key using the available dashboard options.
3. Store the key securely immediately after generation.

The full secret key is displayed only once. Ensure it is saved in a secure location when generated.

3. Authorization Header

Include the API key in the "Authorization" header of every authenticated request.

Authorization: Bearer YOUR_SECRET_API_KEY
Content-Type: application/json
The "Authorization" header carries the Bearer token. The "Content-Type" header indicates that the request body uses JSON where applicable.

4. Test Keys and Live Keys

VaultPay provides separate key environments.

| Key Prefix | Environment | Usage |
|---|---|---|
| `vp_test_` | Sandbox | Testing without moving real money |
| `vp_live_` | Production | Live transactions |
Use sandbox keys during development and testing. Never use a live key in development or continuous integration (CI) pipelines.

5. Managing Keys Across Environments

Use environment variables to manage API keys across different environments.

Keep test and live credentials separate. Never expose a live API key in development or CI configurations.

For additional key-protection practices, see "Security Best Practices" (security.md).

6. Authentication Errors

An absent, malformed, or revoked API key can result in the following error:

| HTTP Status | Error Code | Description |
|---|---|---|
| 401 | `INVALID_API_KEY` | The API key is missing, malformed, or has been revoked. |
If a request returns this error, check that the authorization header is present and that the key is valid.

7. Related Documentation
- [API Overview](overview.md)
- [Security Best Practices](security.md)
- [Quick Start Guide](quickstart.md)
