# Paisa-Lens Requirements

## Project Overview
Paisa-Lens is a TypeScript library for parsing and extracting financial information from SMS messages sent by Indian banks and credit card providers.

## Version 1.0 Scope

### Supported Institutions
1. HDFC Bank
   - Account transactions (credit/debit)
   - UPI transactions
   - ATM withdrawals
   
2. American Express Credit Card
   - Purchase transactions
   - Payment receipts
   
3. SBI Credit Card
   - Purchase transactions
   - Payment receipts

### Core Features

#### SMS Pattern Recognition
- Identify the sending institution
- Validate message format
- Handle variations in message formats
- Filter out non-transaction messages (OTP, promotional)

#### Data Extraction
- Transaction amount
- Transaction type (credit/debit/purchase/payment)
- Account/card details (last 4 digits)
- Date and time
- Available balance/credit limit
- Merchant information (where applicable)
- Transaction method (UPI/ATM/POS)
- Reference IDs (where available)

#### Error Handling
- Invalid message format detection
- Unknown message type handling
- Missing data field handling
- Parsing error reporting

### Technical Requirements

#### Input Format
```typescript
interface SMSMessage {
  message: string;
  timestamp?: Date;
  sender?: string;
}
```

#### Output Format
```typescript
interface ParsedTransaction {
  success: boolean;
  institution: string;
  type: string;
  amount: number;
  accountNumber?: string;
  cardNumber?: string;
  date: Date;
  balance?: number;
  merchantName?: string;
  raw: string;
  error?: string;
}
```

### Usage Example
```typescript
import { PaisaLens } from 'paisa-lens';

const parser = new PaisaLens();
const result = parser.parse('HDFC Bank: Rs.1,000.00 debited...');
```

## Future Enhancements (v2.0+)
1. Additional Banks
   - ICICI Bank
   - SBI Bank
   - Axis Bank

2. Additional Features
   - Statement summary generation
   - Transaction categorization
   - Expense analytics
   - Export functionality (CSV/JSON)

## Non-Functional Requirements

### Performance
- Parse messages in under 50ms
- Handle batch processing efficiently
- Minimal memory footprint

### Reliability
- 99.9% accuracy in parsing known formats
- Graceful handling of unknown formats
- No crashes on malformed inputs

### Code Quality
- 90%+ test coverage
- TypeScript strict mode compliance
- ESLint compliance
- Comprehensive documentation

### Package Size
- Core package under 100KB
- Minimal dependencies

## Development Guidelines
1. Test-Driven Development (TDD) approach
2. Modular design for easy institution additions
3. Clear documentation for each parser
4. Regular expression optimization
5. Comprehensive error messages