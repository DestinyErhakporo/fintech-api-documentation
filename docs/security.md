VaultPay API: Security Best Practices

1. Overview

VaultPay API keys carry the same access level as account credentials and should be treated accordingly.

The following security practices are specified for integrations using the VaultPay API.

2. Keep API Keys Out of Source Code

Never hard-code API keys in:

- Application source files
- Frontend JavaScript
- Version-controlled configuration files

Use environment variables or a secrets manager to store credentials securely.

Examples of secrets-management tools include:

- AWS Secrets Manager
- HashiCorp Vault
- Doppler

3. Use HTTPS Exclusively

All API requests must use TLS/HTTPS. The API rejects plain HTTP connections.

Ensure that your HTTP client does not follow redirects from HTTPS to HTTP.

4. Rotate Credentials Regularly

Rotate API keys periodically, at minimum every 90 days.

Immediately revoke and replace any key that may have been exposed. Revocation takes effect within seconds, according to the API documentation.

5. Use Separate Keys per Environment

Maintain distinct API keys for:

- Development
- Staging
- Production

Never share keys across environments. Separating credentials limits the potential impact if a key is compromised.

6. Restrict Key Permissions

The VaultPay Developer Dashboard allows keys to be scoped to specific endpoints.

For example, a key may be restricted to read-only balance checks.

Follow the principle of least privilege by granting only the permissions required for the integration.

7. Validate Webhook Signatures

When using VaultPay webhooks, verify the "X-VaultPay-Signature" header on incoming requests.

Signature validation is intended to confirm that the payload originated from VaultPay and has not been tampered with.

8. Security Checklist

- [ ] Keep API keys out of source code.
- [ ] Store credentials in environment variables or a secrets manager.
- [ ] Send API requests exclusively over HTTPS.
- [ ] Rotate keys at least every 90 days.
- [ ] Revoke and replace exposed credentials immediately.
- [ ] Use separate credentials for each environment.
- [ ] Restrict API key permissions to the required endpoints.
- [ ] Validate webhook signatures.

9. Related Documentation
- [Authentication](authentication.md)
- [Transfer Operations](transfers.md)
- [Errors and Rate Limits](errors-and-rate-limits.md)
- [Quick Start Guide](quickstart.md)
