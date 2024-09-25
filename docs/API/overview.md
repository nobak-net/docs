---
title: "Overview"
sidebar_position: 1
---

The Recovery Hub API is designed to provide developers with robust tools and endpoints for managing account recovery processes on the Stellar network. This API is essential for applications that require secure, decentralized recovery mechanisms, allowing users to regain control of their Stellar accounts in the event of lost credentials.

## Purpose

The primary purpose of the Recovery Hub API is to facilitate secure interactions between users, recovery servers, and the Stellar network. It ensures that users can recover their accounts by utilizing a network of trusted servers, while developers can easily integrate these functionalities into their applications.

## Key Features

1. **Account Recovery:**  
   - The API allows users to initiate and manage account recovery processes by adding or removing recovery servers as signers to their Stellar accounts.

2. **Multi-Signer Verification:**
   - The API provides endpoints for verifying that multiple recovery servers have signed a transaction, ensuring a secure recovery process.

3. **Secure Authentication:**
   - Authentication mechanisms are built into the API, allowing for secure and verified interactions between users and recovery servers.

4. **Server Management:**
   - Developers can use the API to manage recovery servers, check their availability, and authenticate them for use in recovery processes.

## Use Cases

- **Decentralized Wallets:** Integrate the API to provide users with secure account recovery options.
- **Multi-Signature Services:** Utilize the API to manage multi-signer setups for enhanced account security.
- **Stellar-Based Applications:** Implement recovery features that ensure users can regain access to their accounts if they lose their private keys.

This API is a critical tool for developers building on the Stellar network, offering the necessary functionality to enhance user security and trust through reliable account recovery processes.

## Example Usage

The Recovery Hub API can be used in a variety of scenarios, including:

- **Account Recovery**: Allow users to recover access to their Stellar accounts in case of lost private keys.
- **Multi-Factor Authentication**: Enhance security by requiring multiple recovery servers to verify a user's identity before granting access.
- **Secure Transaction Signing**: Ensure that recovery transactions are signed by trusted servers before being submitted to the Stellar network.
  