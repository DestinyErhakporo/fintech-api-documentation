‎VaultPay Transfer API: Overview
‎
‎1. Introduction
‎
‎The VaultPay Transfer API is a RESTful interface that enables developers to embed financial transfer capabilities directly into their applications. It provides programmatic access to core financial operations over HTTPS using JSON payloads.
‎
‎This documentation is intended for:
‎
‎♦ Backend developers integrating payment flows into web or mobile applications
‎♦ Fintech startups building wallets, remittance tools, or B2B payment platforms
‎♦ Enterprise teams automating payroll, vendor payments, or fund disbursements
‎
‎2. Core Capabilities
‎
‎The API provides the following core capabilities:
‎
‎♦ Money transfers: Initiate money transfers between accounts.
‎♦ Balance retrieval: Retrieve account balance information.
‎♦ Transaction lookup: Look up transaction details and verify payment status.
‎♦ Structured error handling: Receive structured error responses to support error handling in applications.
‎
‎3. API Architecture
‎
‎The VaultPay Transfer API uses REST principles and JSON payloads over HTTPS. Authenticated requests use Bearer token authorization.
‎
‎| Property | Description |
|---|---|
| API style | REST |
| Data format | JSON |
| Transport | HTTPS |
| Authentication | Bearer token |
| API version | v1 |
‎
‎4. Base URL
‎
‎All API requests use the following base URL:
‎
‎"https://api.vaultpay.io/v1"
‎
‎All requests must be made over HTTPS. HTTP requests are rejected.
‎
‎API versioning is embedded in the URL path. When breaking changes are introduced, a new version path will be released, with advance deprecation notices before older versions are retired.
‎
‎5. Core Endpoints
‎
‎Method| Endpoint| Purpose
‎POST| "/transfers"| Initiate a money transfer
‎GET| "/balance"| Retrieve the current account balance
‎GET| "/transactions/{id}"| Retrieve transaction details
‎POST| "/transfers/verify"| Verify a recipient account
‎
‎6. Transaction Statuses
‎
‎The transaction lookup endpoint can return the following transfer statuses:
‎
‎- "pending"
‎- "processing"
‎- "completed"
‎- "failed"
‎- "reversed"
‎
‎7. Documentation Navigation
‎
- [Authentication](authentication.md)
- [Transfer Operations](transfers.md)
- [Balances and Transactions](balance-and-transactions.md)
- [Errors and Rate Limits](errors-and-rate-limits.md)
- [Security Best Practices](security.md)
- [Quick Start Guide](quickstart.md)
