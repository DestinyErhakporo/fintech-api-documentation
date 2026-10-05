VaultPay Transfer API — Quick Start Guide

1. Introduction

This guide walks through the initial steps for integrating with the VaultPay Transfer API using cURL.

The walkthrough covers:

1. Obtaining a sandbox API key
2. Checking an account balance
3. Verifying a recipient account
4. Initiating a transfer
5. Confirming the transaction

The examples use the sandbox environment and placeholder credentials.

2. Prerequisites

Before starting, you need:

- A VaultPay sandbox API key
- cURL installed in your development environment
- An internet connection to send HTTPS requests

3. Step 1 — Get Your API Key

Sign up at "vaultpay.io" and navigate to the Developer Dashboard.

Copy your test key, which uses the "vp_test_" prefix, for sandbox testing.

Store the key securely and avoid exposing it in source code or public repositories.

4. Step 2 — Check Your Balance

Send a GET request to retrieve the balance associated with your authenticated account.

curl -X GET https://api.vaultpay.io/v1/balance
-H "Authorization: Bearer vp_test_YOUR_KEY"
Replace "vp_test_YOUR_KEY" with your sandbox API key.

5. Step 3 — Verify the Recipient Account

Before initiating a transfer, submit the recipient's account number and bank code for verification.

curl -X POST https://api.vaultpay.io/v1/transfers/verify
-H "Authorization: Bearer vp_test_YOUR_KEY"
-H "Content-Type: application/json"
-d '{
  "account_number": "1234567890",
  "bank_code": "058"
}'

The documented successful response includes the account number, account name, and bank name.

6. Step 4 — Initiate the Transfer

Submit the transfer details using the "POST /transfers" endpoint.

curl -X POST https://api.vaultpay.io/v1/transfers
-H "Authorization: Bearer vp_test_YOUR_KEY"
-H "Content-Type: application/json"
-d '{
  "amount": 5000,
  "currency": "NGN",
  "recipient_account": "1234567890",
  "bank_code": "058",
  "narration": "Test transfer",
  "reference": "MY_REF_001"
}'

A successful response returns a unique "transaction_id" that can be used to look up the transfer.

7. Step 5 — Confirm the Transaction

Use the transaction ID returned from the transfer request to retrieve its details.

The following example uses the sample transaction ID from the API documentation:

curl -X GET https://api.vaultpay.io/v1/transactions/TX_8A2F4D91E3
-H "Authorization: Bearer vp_test_YOUR_KEY"

Replace the sample ID with the actual transaction ID returned by your transfer request.

The response provides transaction details, including the transfer status.

8. Production Environment

For production use, replace the sandbox test key with a live key prefixed with "vp_live_".

The API documentation specifies that VaultPay's KYC and compliance review must be completed before enabling live transfers.

Live keys should never be used in development or CI pipelines.

9. Related Documentation

- - [API Overview](overview.md)
- [Authentication](authentication.md)
- [Transfer Operations](transfers.md)
- [Balances and Transactions](balance-and-transactions.md)
- [Errors and Rate Limits](errors-and-rate-limits.md)
- [Security Best Practices](security.md)
