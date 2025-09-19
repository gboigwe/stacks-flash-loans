# Stacks Flash Loans

A flash loan protocol built on the Stacks blockchain using Clarity smart contracts.

## Overview

This project implements a flash loan system that allows users to borrow STX or SIP010 tokens without collateral, as long as they repay the loan plus interest within the same transaction.

## Features

- **STX Flash Loans**: Borrow STX with 0.5% interest (5000 pips)
- **SIP010 Token Flash Loans**: Borrow SIP010 tokens with 1% interest (10000 pips)
- **Atomic Transactions**: All borrowing and repayment must happen in a single transaction
- **Interest Fees**: Automatic calculation and enforcement of interest payments

## Smart Contracts

- `flasher.clar`: Main flash loan protocol contract
- `flashloans-trait.clar`: Trait definitions for flash loan recipients
- `mock-token.clar`: Mock SIP010 token for testing
- `mock-flash-recipient.clar`: Example flash loan recipient implementation

## Usage

To use the flash loan protocol, your contract must implement either the `stx-flasher` or `sip010-flasher` trait and define the callback functions:

```clarity
;; For STX flash loans
(define-public (on-stx-flash (amount uint) (return-amount uint))
  ;; Your arbitrage/trading logic here
  ;; Must repay return-amount STX to the flasher contract
)

;; For SIP010 token flash loans  
(define-public (on-sip010-flash (token <ft-trait>) (amount uint) (return-amount uint))
  ;; Your arbitrage/trading logic here
  ;; Must repay return-amount tokens to the flasher contract
)
```

## Testing

Run the test suite:

```bash
npm install
npm run test
```

## Error Codes

- `u101`: Insufficient balance in flasher contract
- `u102`: Outbound transfer failed
- `u103`: Flash loan callback failed
- `u104`: Inbound transfer failed
- `u105`: Insufficient payback amount
- `u106`: Failed to fetch balance
