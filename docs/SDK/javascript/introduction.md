# Nobak Recovery SDK Documentation

## Overview

The Nobak Recovery SDK simplifies integration with the Nobak Recovery Hub API, providing developers with an easy-to-use interface for account management, authentication, contract execution, and server interactions within the Stellar ecosystem.

This SDK abstracts the complexities of direct API calls, allowing developers to focus on building robust applications with account recovery and security features.

## Table of Contents

- [Nobak Recovery SDK Documentation](#nobak-recovery-sdk-documentation)
  - [Overview](#overview)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Initialization](#initialization)
  - [Services](#services)
    - [Auth](#auth)
      - [Methods](#methods)
      - [Usage](#usage)
    - [Account](#account)
      - [Methods](#methods-1)
      - [Usage](#usage-1)
    - [Contract](#contract)
      - [Methods](#methods-2)
      - [Usage](#usage-2)
    - [Server](#server)
      - [Methods](#methods-3)
      - [Usage](#usage-3)
  - [Examples](#examples)
    - [Registering a Stellar Address](#registering-a-stellar-address)
    - [Verifying a Stellar Address](#verifying-a-stellar-address)
    - [Adding Authentication Methods](#adding-authentication-methods)
    - [Executing a Contract](#executing-a-contract)
    - [Listing Available Servers](#listing-available-servers)
  - [API Reference](#api-reference)
    - [RecoverySDK](#recoverysdk)
      - [Constructor](#constructor)
      - [Properties](#properties)
    - [Auth Service](#auth-service)
      - [Methods](#methods-4)
    - [Account Service](#account-service)
      - [Methods](#methods-5)
    - [Contract Service](#contract-service)
      - [Methods](#methods-6)
    - [Server Service](#server-service)
      - [Methods](#methods-7)
  - [Error Handling](#error-handling)
  - [License](#license)

---

## Installation

You can install the Nobak Recovery SDK via npm:

```bash
npm install nobak-sdk
```

---

## Initialization

To start using the SDK, import it and initialize it with your API key and other optional parameters.

```javascript
import { RecoverySDK } from 'nobak-sdk';

const sdk = new RecoverySDK({
  KEY: 'YOUR_API_KEY',        // Required
  USER_TOKEN: 'USER_TOKEN',   // Optional, obtained after authentication
  NETWORK: 'TESTNET',         // Optional, 'TESTNET' or 'MAINNET', default is 'TESTNET'
});
```

- **`KEY`**: Your API key provided by the Nobak Recovery Hub.
- **`USER_TOKEN`**: A token representing the user's session. Required for certain operations.
- **`NETWORK`**: The Stellar network to interact with. Defaults to `'TESTNET'`.

---

## Services

The SDK provides four main services:

1. **Auth**: Handles authentication and verification of Stellar addresses.
2. **Account**: Manages user accounts and authentication methods.
3. **Contract**: Executes contracts related to account recovery.
4. **Server**: Interacts with recovery servers.

Each service is accessible via the initialized SDK instance.

### Auth

The `Auth` service is used to register and verify Stellar addresses with the Nobak Recovery Hub.

#### Methods

- **`register({ stellar_address })`**: Initiates the registration process for a Stellar address.
- **`verify({ stellar_address, XDR })`**: Verifies the Stellar address using a signed transaction (XDR).

#### Usage

```javascript
// Register a Stellar address
const registrationResponse = await sdk.Auth.register({
  stellar_address: 'GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
});

// Verify the Stellar address with signed XDR
const verificationResponse = await sdk.Auth.verify({
  stellar_address: 'GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  XDR: 'SIGNED_XDR_STRING',
});
```

---

### Account

The `Account` service manages user accounts and authentication methods like email, phone number, or Stellar addresses.

#### Methods

- **`register({ type, value })`**: Adds a new authentication method to the user's account.
  - **`type`**: The type of method (`'email'`, `'phone_number'`, `'stellar_address'`).
  - **`value`**: The value of the method (e.g., email address, phone number).
- **`verify({ value, state })`**: Verifies the authentication method using a code or state.
- **`profile()`**: Retrieves the user's profile and linked authentication methods.

#### Usage

```javascript
// Add an email authentication method
const addEmailResponse = await sdk.Account.register({
  type: 'email',
  value: 'user@example.com',
});

// Verify the email using a state or code
const verifyEmailResponse = await sdk.Account.verify({
  value: 'user@example.com',
  state: 'VERIFICATION_STATE_OR_CODE',
});

// Retrieve user profile
const profile = await sdk.Account.profile();
```

---

### Contract

The `Contract` service executes contracts related to account recovery, such as adding or removing signers.

#### Methods

- **`execute({ contract, data })`**: Executes a contract.
  - **`contract`**: The type of contract to execute (`ContractType.ADD_SIGNERS`, `ContractType.REMOVE_SIGNERS`, `ContractType.SIGN`).
  - **`data`**: Data required for the contract execution.

#### Usage

```javascript
import { ContractType } from 'nobak-sdk/types';

// Add signers
const addSignersResponse = await sdk.Contract.execute({
  contract: ContractType.ADD_SIGNERS,
  data: {
    server_ids: ['server1', 'server2', 'server3'], // At least two server IDs
  },
});

// Sign a transaction
const signResponse = await sdk.Contract.execute({
  contract: ContractType.SIGN,
  data: {
    XDR: 'TRANSACTION_XDR_TO_SIGN',
  },
});
```

---

### Server

The `Server` service interacts with the recovery servers, allowing you to list servers, authenticate them, and verify them.

#### Methods

- **`list()`**: Lists all servers associated with the user's account.
- **`available()`**: Lists all available servers.
- **`auth({ name })`**: Initiates authentication with a server.
- **`verify({ name, signed_xdr })`**: Verifies the server using a signed transaction.

#### Usage

```javascript
// List servers associated with the account
const serverList = await sdk.Server.list();

// List available servers
const availableServers = await sdk.Server.available();

// Authenticate with a server
const authResponse = await sdk.Server.auth({ name: 'server1' });

// Verify the server with signed XDR
const verifyResponse = await sdk.Server.verify({
  name: 'server1',
  signed_xdr: 'SIGNED_XDR_STRING',
});
```

---

## Examples

### Registering a Stellar Address

```javascript
// Initialize the SDK
const sdk = new RecoverySDK({
  KEY: 'YOUR_API_KEY',
});

// Register a Stellar address
const registrationResponse = await sdk.Auth.register({
  stellar_address: 'GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
});

// Handle the response
if (registrationResponse) {
  // Proceed to sign the transaction
  const XDR = registrationResponse.xdr;

  // Sign the XDR with your Stellar private key (using Stellar SDK or similar)
  const signedXDR = signXDR(XDR, 'YOUR_SECRET_KEY');

  // Verify the registration
  const verificationResponse = await sdk.Auth.verify({
    stellar_address: 'GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
    XDR: signedXDR,
  });

  if (verificationResponse) {
    console.log('Stellar address verified successfully.');
  } else {
    console.error('Verification failed.');
  }
} else {
  console.error('Registration failed.');
}
```

---

### Verifying a Stellar Address

Assuming you have already registered the Stellar address and obtained the XDR:

```javascript
// Sign the XDR
const signedXDR = signXDR(XDR, 'YOUR_SECRET_KEY');

// Verify the Stellar address
const verificationResponse = await sdk.Auth.verify({
  stellar_address: 'GXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX',
  XDR: signedXDR,
});

if (verificationResponse) {
  console.log('Stellar address verified successfully.');
} else {
  console.error('Verification failed.');
}
```

---

### Adding Authentication Methods

```javascript
// Add a phone number to the account
const addPhoneResponse = await sdk.Account.register({
  type: 'phone_number',
  value: '+1234567890',
});

// Verify the phone number with a code received via SMS
const verifyPhoneResponse = await sdk.Account.verify({
  value: '+1234567890',
  state: 'VERIFICATION_CODE_FROM_SMS',
});

if (verifyPhoneResponse) {
  console.log('Phone number verified successfully.');
} else {
  console.error('Phone verification failed.');
}
```

---

### Executing a Contract

```javascript
import { ContractType } from 'nobak-sdk/types';

// Add signers to the account
const addSignersResponse = await sdk.Contract.execute({
  contract: ContractType.ADD_SIGNERS,
  data: {
    server_ids: ['server1', 'server2'],
  },
});

if (addSignersResponse) {
  console.log('Signers added successfully.');
} else {
  console.error('Failed to add signers.');
}
```

---

### Listing Available Servers

```javascript
// Get a list of available servers
const availableServers = await sdk.Server.available();

console.log('Available servers:', availableServers);
```

---

## API Reference

### RecoverySDK

#### Constructor

```typescript
new RecoverySDK({
  KEY: string;           // Required
  USER_TOKEN?: string;   // Optional
  NETWORK?: 'TESTNET' | 'MAINNET'; // Optional
});
```

#### Properties

- **`Auth`**: Instance of the `Auth` service.
- **`Account`**: Instance of the `Account` service.
- **`Contract`**: Instance of the `Contract` service.
- **`Server`**: Instance of the `Server` service.

---

### Auth Service

Handles authentication and verification of Stellar addresses.

#### Methods

- **`register({ stellar_address: string }): Promise<any>`**  
  Initiates the registration process for a Stellar address.

- **`verify({ stellar_address: string, XDR: string }): Promise<any>`**  
  Verifies the Stellar address using a signed transaction (XDR).

---

### Account Service

Manages user accounts and authentication methods.

#### Methods

- **`register({ type: string, value: string }): Promise<any>`**  
  Adds a new authentication method to the user's account.

- **`verify({ value: string, state: string }): Promise<any>`**  
  Verifies the authentication method using a code or state.

- **`profile(): Promise<any>`**  
  Retrieves the user's profile and linked authentication methods.

---

### Contract Service

Executes contracts related to account recovery.

#### Methods

- **`execute({ contract: ContractType, data?: any }): Promise<any>`**  
  Executes a specified contract.

---

### Server Service

Interacts with recovery servers.

#### Methods

- **`list(): Promise<any>`**  
  Lists all servers associated with the user's account.

- **`available(): Promise<any>`**  
  Lists all available servers.

- **`auth({ name: string }): Promise<any>`**  
  Initiates authentication with a server.

- **`verify({ name: string, signed_xdr: string }): Promise<any>`**  
  Verifies the server using a signed transaction.

---

## Error Handling

All methods return a promise that resolves to the API response. In case of an error, the response may be `null` or contain error details.

Example:

```javascript
try {
  const response = await sdk.Auth.register({ stellar_address });
  if (response) {
    // Handle success
  } else {
    // Handle API error
    console.error('API Error: Registration failed.');
  }
} catch (error) {
  // Handle network or other errors
  console.error('An error occurred:', error);
}
```

---

## License

This SDK is licensed under the MIT License.

---

**Note**: Replace placeholders like `'YOUR_API_KEY'`, `'YOUR_SECRET_KEY'`, and other sample data with actual values when implementing.