VaultPay API: Errors and Rate Limits

1. Error Responses

The VaultPay API uses standard HTTP status codes alongside a structured JSON error body. Every error response includes a machine-readable "code" and a human-readable "message".

Error Response Structure
{
  "status": "error",
  "code": "INSUFFICIENT_BALANCE",
  "message": "Account balance is too low to complete this transfer."
}

2. Common Error Codes

HTTP Status| Error Code| Description
401| "INVALID_API_KEY"| The API key is missing, malformed, or has been revoked.
403| "FORBIDDEN"| The key does not have permission to perform this action.
400| "INVALID_ACCOUNT_NUMBER"| The recipient account number format is invalid.
400| "INVALID_BANK_CODE"| The supplied bank code does not match any supported bank.
400| "INVALID_CURRENCY"| The currency code is unsupported or incorrectly formatted.
400| "MISSING_REQUIRED_FIELD"| A required field in the request body is absent.
402| "INSUFFICIENT_BALANCE"| The account balance is too low to cover the transfer amount.
404| "TRANSACTION_NOT_FOUND"| No transaction exists with the provided ID.
409| "DUPLICATE_REFERENCE"| A transfer with this reference has already been processed.
429| "RATE_LIMIT_EXCEEDED"| Too many requests. Slow down and retry after the window resets.
500| "INTERNAL_SERVER_ERROR"| An unexpected server-side error occurred. Contact support if it persists.

3. Handling Errors

When an API request returns an error:

1. Check the HTTP status code.
2. Read the "code" field to identify the error.
3. Review the "message" field for its description.
4. Correct the request or address the issue indicated by the response.

For rate-limit errors, follow the reset information described in the rate-limit section below.

4. Rate Limits

Rate limits are applied per API key. Exceeding the configured limit returns a "429 Too Many Requests" response.

Limits are measured on a rolling 60-second window.

Rate Limits by Plan

Plan| Requests per Minute| Requests per Day
Sandbox (Test Keys)| 60| 10,000
Starter (Live)| 100| 50,000
Growth (Live)| 300| 200,000
Enterprise (Live)| 1,000| Unlimited

5. Rate-Limit Headers

The API response includes rate-limit metadata in the following headers:

 Header| Description
"X-RateLimit-Limit"| Maximum number of requests allowed in the current window.
"X-RateLimit-Remaining"| Number of requests remaining in the current window.
"X-RateLimit-Reset"| Unix timestamp indicating when the request window resets.
Example Headers

X-RateLimit-Limit: 100
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1717228800

The "X-RateLimit-Reset" value is a Unix timestamp that indicates when the request window resets.

If a request receives a "429 Too Many Requests" response, wait until the indicated reset time before retrying.

6. Related Documentation

- [Authentication](authentication.md)
- [Transfer Operations](transfers.md)
- [Security Best Practices](security.md)
- [Quick Start Guide](quickstart.md)
