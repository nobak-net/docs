## **Wallet Technical Components:**

#### **Multi-Stellar Account Manager:**

•	**Standard Accounts (ed25519):** For traditional operations.

•	**Soroban Accounts (secp256r1):** Essential for interacting with Soroban smart contracts.

•	**Secure Account Creation:** Uses contract-webauthn-ed25519 and contract-webauthn-secp256r1 with WebAuthn for secure authentication via hardware tokens or biometrics.

#### **Cloud Sync & Recovery:**

•	Implements **SEP-0030** for encrypted client-side backup.

•	**Data Encryption:** Uses AES-256 encryption; encryption keys derived from user passwords never leave the device.

•	**Recovery Mechanism:** Secure account recovery via email, phone, or 2FA.

#### **DApp Directory (Soroban DApp Explorer):**

•	Explore and interact with Soroban-based DApps.

•	**Community Contributions:** Developers add DApps via the [Nobak Metadata Repository](https://github.com/nobak-net/metadata/).

•	**User Interface:** Intuitive design with search/filter options, detailed DApp info, WalletConnect integration.

#### **Native Integration of Lend/Borrow/Swap Contracts:**

•	**Lending/Borrowing (Blend Protocol):** Lend assets or borrow using collateral, seamlessly interacting with smart contracts.

•	**Swapping (Soroswap Protocol):** Swap assets with real-time rates.

•	**Smart Contract Interaction:** Simplifies complexities, securely signing transactions within the wallet.

#### **Fiat On/Off-Ramp:**

•	Implements **SEP-0024** for fiat conversions via compliant anchors.

**User Experience:** Streamlined interface with secure KYC/AML compliance.

#### **Security Features:**

•	**Two-Factor Authentication (2FA):** Adds security during login and transactions.

•	**Biometric Authentication:** Fingerprint and facial recognition for secure access.

•	**End-to-End Encryption:** All sensitive data encrypted on-device using AES-256 and TLS.

•	**Blockaid Integration:** Advanced threat detection, monitoring, and user alerts.

#### **Developer Mode:**

•	**Testnet Access:** Connects to Stellar testnet for safe DApp development.

•	**Debugging Tools:** Logs, diagnostics, and custom network configurations.

#### **Localization and Multi-Language Support:**

•	Supports multiple languages for global accessibility.

•	**Regional Customizations:** Tailored features like debit cards in Argentina via Anclap partnership.

#### **Workflow and Technical Details:**

•	**User Onboarding:** Secure account creation with options for standard or Soroban accounts, security setup, and optional cloud sync.

•	**Interacting with DApps:** Access and interact with DApps via the directory; seamless integration and transaction handling.

•	**Lending, Borrowing, Swapping:** Intuitive interfaces for DeFi activities with real-time data and secure transaction flows.

•	**Fiat Transactions:** Secure KYC/AML-compliant fiat on/off-ramp processes.

•	**Security Management:** Real-time monitoring, alerts, and account management features.

#### **Technical Stack:**

•	**Frontend:** React Native, TypeScript, Redux, WalletConnect.

•	**Backend and APIs:** Stellar SDKs, Soroban SDK, SEP-0024, SEP-0030.

•	**Security:** Blockaid, AES-256, TLS, biometric and 2FA authentication.

•	**Cloud Services:** Encrypted storage, push notifications.

•	**Smart Contracts:** Direct interaction with Soroban contracts, including Blend and Soroswap.

#### **Adoption of Soroban Accounts:**

•	Enhanced security and DeFi access.

•	Simplified user experience with guidance on account usage.

#### **Native Integration of DeFi Contracts:**

•	Direct interaction with lending, borrowing, and swapping protocols.

•	Simplifies complex operations with intuitive interfaces.

•	Ensures security and transparency in all transactions.

#### **Developer Engagement:**

•	**Developer Mode and Testnet Support:** Encourages Soroban ecosystem growth.

•	**Community Contributions:** Open-source resources and support for community-submitted DApps.