VaultPay API:  Transfer Operations

1. Overview

The VaultPay Transfer API provides endpoints for initiating money transfers and verifying recipient account details.

The core transfer operations are:

| Method | Endpoint | Purpose |
|---|---|---|
| POST | `/transfers` | Initiate a new money transfer |
| POST | `/transfers/verify` | Verify a recipient account |

2. Initiate a Transfer

Endpoint

POST /transfers

This endpoint creates and submits a new money transfer. The recipient account is validated before the transfer is queued. A successful response returns a unique transaction ID that can be used to track the transfer's status.

Request Body
{
  "amount": 5000,
  "currency": "NGN",
  "recipient_account": "1234567890",
  "bank_code": "058",
  "narration": "Invoice #INV-2025-001",
  "reference": "TX_REF_20250601_001"
}

  


Request Parameters

Field| Type| Required| Description
"amount"| integer| Yes| Transfer amount in the smallest currency unit, such as kobo or cents
"currency"| string| Yes| ISO 4217 currency code, e.g. NGN, USD, GHS
"recipient_account"| string| Yes| Recipient's account number
"bank_code"| string| Yes| Recipient's bank code as listed in "/banks"
"narration"| string| No| Optional description or memo visible to the recipient
"reference"| string| No| Your own unique reference for idempotency tracking

Successful Response, 200 OK

{
  "status": "success",
  "transaction_id": "TX_8A2F4D91E3",
  "amount": 5000,
  "currency": "NGN",
  "recipient": "1234567890",
  "narration": "Invoice #INV-2025-001",
  "timestamp": "2025-06-01T08:35:21Z"
}

The "transaction_id" uniquely identifies the transfer and can be used with the transaction lookup endpoint.

3. Verify a Recipient Account

Endpoint

POST /transfers/verify

This endpoint verifies a recipient account before initiating a transfer. It is intended to confirm that an account number is valid and belongs to the expected bank.

Request Body

{
  "account_number": "1234567890",
  "bank_code": "058"
}

Request Parameters

Field| Type| Description
"account_number"| string| Recipient's account number
"bank_code"| string| Recipient's bank code

Successful Response — 200 OK

{
  "status": "success",
  "account_number": "1234567890",
  "account_name": "John A. Doe",
  "bank_name": "Zenith Bank"
}

The response provides the account name and bank name associated with the supplied account details.

4. Transfer Status Tracking

After initiating a transfer, use the returned "transaction_id" to retrieve its details.

The documented transfer statuses are:

Status| Description
"pending"| Transfer is pending
"processing"| Transfer is being processed
"completed"| Transfer is completed
"failed"| Transfer failed
"reversed"| Transfer was reversed

See "Balances and Transactions" (balance-and-transactions.md) for transaction lookup details.

5. Related Documentation
   - [Authentication](authentication.md)
- [Balances and Transactions](balance-and-transactions.md)
- [Errors and Rate Limits](errors-and-rate-limits.md)
- [Quick Start Guide](quickstart.md)
