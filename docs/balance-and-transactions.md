‎VaultPay API: Balances and Transactions
‎
‎1. Overview
‎
‎The VaultPay API provides endpoints for retrieving the authenticated account's current balance and looking up the details of an individual transaction.
‎
‎| Method | Endpoint | Purpose |
|---|---|---|
| GET | `/balance` | Retrieve the current account balance |
| GET | `/transactions/{id}` | Look up a transaction by ID |
‎2. Retrieve Account Balance
‎
‎Endpoint
‎
‎GET /balance
‎
‎This endpoint returns the current balance for the authenticated account. No request body is required. The account is identified by the API key included in the "Authorization" header.
‎
‎Successful Response — 200 OK
‎
‎{
  "status": "success",
  "currency": "NGN",
  "balance": 250000,
  "ledger_balance": 270000,
  "timestamp": "2025-06-01T08:36:00Z"
}
‎
‎Response Fields
‎
‎Field| Type| Description
‎"status"| string| Indicates the response status
‎"currency"| string| Currency of the account balance
‎"balance"| number| Available account funds
‎"ledger_balance"| number| Ledger balance, including pending debits that have not yet settled
‎"timestamp"| string| Timestamp associated with the response
‎
‎The "balance" field reflects available funds. The "ledger_balance" field includes pending debits that have not yet settled.
‎
‎3. Retrieve Transaction Details
‎
‎Endpoint
‎
‎GET /transactions/{id}
‎
‎This endpoint returns full details for a specific transaction.
‎
‎Use the "transaction_id" returned by "POST /transfers", or an ID retrieved from the VaultPay dashboard.
‎
‎Path Parameter
‎
‎Parameter| Type| Description
‎"id"| string| Unique transaction ID, e.g. "TX_8A2F4D91E3"
‎
‎Successful Response, 200 OK
‎
‎{
‎  "status": "success",
‎  "transaction_id": "TX_8A2F4D91E3",
‎  "type": "debit",
‎  "amount": 5000,
‎  "currency": "NGN",
‎  "recipient": "1234567890",
‎  "bank_code": "058",
‎  "narration": "Invoice #INV-2025-001",
‎  "transfer_status": "completed",
‎  "timestamp": "2025-06-01T08:35:21Z"
‎}
‎
‎Response Fields
‎
‎Field| Type| Description
‎"status"| string| Indicates the response status
‎"transaction_id"| string| Unique transaction identifier
‎"type"| string| Transaction type, e.g. debit
‎"amount"| number| Transaction amount
‎"currency"| string| Transaction currency
‎"recipient"| string| Recipient account number
‎"bank_code"| string| Recipient's bank code
‎"narration"| string| Transfer description
‎"transfer_status"| string| Current recorded transfer status
‎"timestamp"| string| Transaction timestamp
‎
‎The documented "transfer_status" values are "pending", "processing", "completed", "failed", and "reversed".
‎
‎4. Related Documentation
‎
‎- [API Overview](overview.md)
- [Authentication](authentication.md)
- [Transfer Operations](transfers.md)
- [Errors and Rate Limits](errors-and-rate-limits.md)
- [Quick Start Guide](quickstart.md)
