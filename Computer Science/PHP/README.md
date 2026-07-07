# Backend Technical Challenge

## Technical Test for Backend Developer

This technical challenge is part of the selection process for the **Backend Developer** position.

The test aims to evaluate real-world backend development skills, Laravel/PHP proficiency, API design, jobs/queues, bank notification processing, closing reconciliation, integration with external services, database management, idempotence, traceability, and transactional logic.

We are not looking for an unnecessarily extensive solution or a complete production system. We are looking for a clear, organized, and technically sound implementation that demonstrates how you would make decisions in real-world scenarios.

# 1. Case Context

The company processes payments for merchants.

When a customer makes a payment at the bank, the system receives real-time bank confirmation. This confirmation allows the payment to be operationally recorded within the system.

Later, at the end of the day, the bank sends a reconciliation file or batch with the formal details of the processed transactions. This reconciliation process should not duplicate payments, but rather validate what has been received in real time and detect any discrepancies.

Furthermore, when a transaction is successfully confirmed as paid, the system should simulate a notification to an external service, such as an internal merchant system, a third-party provider, or a settlement module.

The goal is to build a backend API that securely handles this workflow, preventing duplicates, inconsistencies, reprocessing, and settlement errors.

# 2. Suggested Stack

The test should be developed using:

- Modern Laravel.

- PHP 8.2 or higher.

- MySQL or PostgreSQL.

- Laravel Jobs/Queues.

- Redis, a database queue, or any driver you deem appropriate, provided you explain your choice.

- Pest or PHPUnit for basic testing.

Building a frontend is not required.

Appropriate use of the following will be considered an asset:

- Form Requests.

- API Resources.

- Enums or constants for states.

- Services, Actions, or domain classes.

- Jobs.

- Migrations.

- Seeders or factories, if you deem it necessary.

- Logs and traceability.

# 3. Expected Time

The test is designed to be completed in approximately **4-6 hours**.

If, due to time constraints, you decide not to implement any secondary details, you can explain them in your solution's README, indicating how you would address them in a production environment and why.

# 4. Test Scope

You must implement the following modules:

1. Create a payment transaction.

2. Receive real-time bank confirmation.

3. Process the confirmation using a job.

4. Avoid duplicates using `event_id` and `bank_transaction_id`.

5. Validate the amount and currency.

6. Mark transactions as `PAID` or `OBSERVED` as appropriate. 7. Process end-of-day bank reconciliation.

8. Detect matches, discrepancies, and missing transactions.

9. Simulate a notification to an external service when a transaction is marked as `PAID`.

10. Query transactions eligible for settlement, considering status, reconciliation, and cutoff time.

# 5. Module A: Create Payment Transaction

## Endpoint

```http

POST /api/v1/payments
```

## Example Payload

```json
{
"merchant_id": 10,
"customer_document": "76359665",
"amount": 150.50,
"currency": "PEN",
"description": "Monthly Service Payment"
}
```

## Expected Rules

The transaction must be created with:

- Unique payment code.

- Initial status `PENDING`.

- Amount.

- Currency.

- Associated Merchant.

- Customer ID.

- Creation Date.

Example payment code:

```text
LTP-20260424-000001
```

Example response:

```json
{
"payment_code": "LTP-20260424-000001",
"status": "PENDING",
"amount": "150.50",
"currency": "PEN"
}
```

It will be appreciated if the handling of amounts avoids precision errors, for example, using cents as integers or decimals with a clear justification.

# 6. Module B: Receiving Real-Time Bank Confirmation

## Endpoint

```http

POST /api/v1/bank/notifications
```

## Example Payload

```json
{
"event_id": "evt_001",
"bank_transaction_id": "bank_tx_999",
"payment_code": "LTP-20260424-000001",
"amount": 150.50,
"currency": "PEN",
"status": "PAID",
"paid_at": "2026-04-24 20:44:00"
}
```

## Expected Rules

- Validate authenticity using a token, simple signature, HMAC, or equivalent mechanism.

- Save the original received payload.

- Do not process all logic directly in the controller.

- Log the received event.
- Dispatch a job to process the confirmation.

- Avoid processing the same `event_id` twice.

- Avoid duplicate payments if the same `bank_transaction_id` is received twice.

- If the amount does not match the original transaction, the transaction should be marked `OBSERVED`.

- If the currency does not match, the transaction should be marked `OBSERVED`.

- If everything matches, the transaction should be marked `PAID`.

- A record of the decision made must be kept.

The job can be named, for example:

```text
Proc