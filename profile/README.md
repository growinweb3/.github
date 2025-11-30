<div align="center">
  <img src="https://growish.xyz/logo.png" alt="Growish Logo" width="200"/>
  
  # Growish - Stablecoin Yield Aggregator
  
  **Maximize your DeFi returns with intelligent vault strategies**
  
  [![Website](https://img.shields.io/badge/Website-growish.xyz-blue)](https://growish.xyz/)
  [![Network](https://img.shields.io/badge/Network-Lisk%20Sepolia-purple)](https://sepolia-blockscout.lisk.com/)
  [![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
  
  *Powered by DeFi Excellence*
</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Architecture](#-architecture)
- [Smart Contracts](#-smart-contracts)
- [Deployed Contracts](#-deployed-contracts)
- [User Guide](#-user-guide)
- [Risk Levels](#-risk-levels)
- [How It Works](#-how-it-works)
- [Getting Started](#-getting-started)

---

## 🌟 Overview

**Growish** is a yield aggregator platform focused on stablecoins (USDC) that solves critical DeFi challenges:

- **High Gas Fees**: Batching technology reduces transaction costs by up to 90%
- **Complexity for Beginners**: Simple 1-click deposit interface, no DeFi expertise needed
- **Lack of Transparency**: Real-time APY tracking and clear risk levels

**Current Stats:**
- 💰 **$2.4M+** Total Value Locked
- 📊 **12.5%** Average APY
- 🏦 **3** Active Vaults

---

## ✨ Key Features

### 🏊 Pooled Vault System
Users with the same risk tolerance pool their funds together in shared vaults, enabling:
- Better capital efficiency
- Lower transaction costs per user
- Automated yield optimization

### 📦 Batching Technology
Processes deposits and withdrawals in batches to minimize gas fees:
- Users queue their transactions
- Batch executor processes multiple requests at once
- Gas costs are distributed among all participants

### 🎯 Three Risk Levels

| Risk Level | Strategy | Target Users |
|-----------|----------|--------------|
| **Conservative** | Stable protocols, lower APY | Risk-averse investors |
| **Balanced** | Mix of stable & moderate yield | Moderate risk tolerance |
| **Aggressive** | Higher yield protocols | Risk-seeking investors |

**Initial Allocation**: All vaults start with 50% Protocol A + 50% Protocol B

**Dynamic Rebalancing**: Automatic APY-weighted rebalancing optimizes returns based on real-time performance

---

## 🏗️ Architecture

```
┌─────────────┐
│    User     │
└──────┬──────┘
       │
       ▼
┌─────────────────────────────────────┐
│           Router.sol                │
│  (Entry Point & Batch Manager)      │
└─────────┬───────────────────────────┘
          │
          ├─────────┬──────────┬───────────┐
          ▼         ▼          ▼           ▼
    ┌─────────┐ ┌─────────┐ ┌─────────┐
    │ Vault   │ │ Vault   │ │ Vault   │
    │  Cons.  │ │ Balanced│ │  Aggr.  │
    └────┬────┘ └────┬────┘ └────┬────┘
         │           │           │
    ┌────┴────┐ ┌────┴────┐ ┌────┴────┐
    ▼         ▼ ▼         ▼ ▼         ▼
┌──────┐  ┌──────┐  ┌──────┐  ┌──────┐
│Strat │  │Strat │  │Strat │  │Strat │
│ Aave │  │Comp. │  │ Aave │  │Comp. │
└───┬──┘  └───┬──┘  └───┬──┘  └───┬──┘
    │         │         │         │
    ▼         ▼         ▼         ▼
┌────────────────────────────────────┐
│      External DeFi Protocols       │
│    (Aave, Compound, etc.)          │
└────────────────────────────────────┘
```

---

## 📜 Smart Contracts

### 1. **Router.sol**
**Role**: Main entry point for user interactions

**Responsibilities:**
- Manages deposit and withdrawal queues
- Executes batch transactions for gas efficiency
- Routes funds to appropriate vaults based on risk level

**Key Functions:**
```solidity
deposit(amount, riskLevel)      // Queue deposit
withdraw(shares, riskLevel)     // Queue withdrawal
claimDepositShares(riskLevel)   // Claim vault shares
claimWithdrawAssets(riskLevel)  // Claim USDC
```

---

### 2. **Vault.sol**
**Role**: Funds pool manager and strategy orchestrator

**Responsibilities:**
- Issues ERC-20 shares representing user ownership
- Manages fund allocation across multiple strategies
- Performs auto-compounding of yields
- Executes APY-based rebalancing

**Key Features:**
- Transparent share valuation
- Automated yield harvesting
- Strategy diversification

---

### 3. **Strategy.sol**
**Role**: Technical bridge to external DeFi protocols

**Responsibilities:**
- Contains protocol-specific interaction logic
- Holds receipt tokens from protocols (aTokens, cTokens, etc.)
- Harvests and compounds yields
- Reports performance metrics to Vault

**Interactions:**
- Deposits USDC into lending protocols
- Withdraws funds on demand
- Claims protocol rewards

---

### 4. **MockProtocol.sol**
**Role**: DeFi lending protocol simulator (for testing)

**Purpose:**
- Simulates Aave/Compound behavior
- Generates yield for testing
- Used in testnet environment

---

### 5. **MockUSDC.sol**
**Role**: ERC-20 stablecoin for testing

**Purpose:**
- Represents USDC on testnet
- Enables testing without real USDC

---

## 🚀 Deployed Contracts

All contracts are deployed and verified on **Lisk Sepolia Testnet**:

| Contract | Address | Explorer |
|----------|---------|----------|
| **MockUSDC** | `0x6f576F9A89555b028ce97581DA6d10e35d433F04` | [View](https://sepolia-blockscout.lisk.com/address/0x6f576F9A89555b028ce97581DA6d10e35d433F04) |
| **Router** | `0x7dC0da00F845A4272C08E51a57651ac004f5e0C7` | [View](https://sepolia-blockscout.lisk.com/address/0x7dC0da00F845A4272C08E51a57651ac004f5e0C7) |
| **Vault (Conservative)** | `0x6E69Ed7A9b7F4b1De965328738b3d7Bb757Ea94c` | [View](https://sepolia-blockscout.lisk.com/address/0x6E69Ed7A9b7F4b1De965328738b3d7Bb757Ea94c) |
| **Vault (Balanced)** | `0x21AF332B10481972B903cBd6C3f1ec51546552e7` | [View](https://sepolia-blockscout.lisk.com/address/0x21AF332B10481972B903cBd6C3f1ec51546552e7) |
| **Vault (Aggressive)** | `0xc4E50772bd6d27661EE12d81e62Daa4882F4E6f4` | [View](https://sepolia-blockscout.lisk.com/address/0xc4E50772bd6d27661EE12d81e62Daa4882F4E6f4) |
| **MockProtocol (Aave)** | `0x53175d08E96a961233ea333385EA74E74C556Cf1` | [View](https://sepolia-blockscout.lisk.com/address/0x53175d08E96a961233ea333385EA74E74C556Cf1) |
| **MockProtocol (Compound)** | `0x831f464C241eAa6CcF72F5570c7F5E5f9759317e` | [View](https://sepolia-blockscout.lisk.com/address/0x831f464C241eAa6CcF72F5570c7F5E5f9759317e) |
| **Strategy (Aave)** | `0x85A1B6A61C5E73418A40A3a79F6E811Ee848dAa7` | [View](https://sepolia-blockscout.lisk.com/address/0x85A1B6A61C5E73418A40A3a79F6E811Ee848dAa7) |
| **Strategy (Compound)** | `0x4B29149492019fE65D0363097728Cab61Cb97F0f` | [View](https://sepolia-blockscout.lisk.com/address/0x4B29149492019fE65D0363097728Cab61Cb97F0f) |

---

## 👤 User Guide

### Prerequisites
1. MetaMask or compatible Web3 wallet
2. Connected to **Lisk Sepolia Testnet**
3. Test USDC tokens (get from faucet or contract)

### Step-by-Step: Making a Deposit

#### Option 1: Using the Web App (Recommended)
Visit **[growish.xyz](https://growish.xyz/)** and follow the intuitive interface:

1. **Connect Wallet** → Click "Connect Wallet" button
2. **Choose Risk Level** → Select Conservative, Balanced, or Aggressive
3. **Enter Amount** → Input USDC amount to deposit
4. **Approve** → Approve USDC spending (one-time)
5. **Deposit** → Confirm deposit transaction
6. **Wait for Batch** → Your deposit will be processed in the next batch
7. **Claim Shares** → Claim your vault shares once batch executes

#### Option 2: Direct Smart Contract Interaction

**Step 1: Approve USDC**
```javascript
// Approve Router to spend your USDC
await mockUSDC.approve(routerAddress, amount);
```

**Step 2: Queue Deposit**
```javascript
// Deposit to queue (riskLevel: 0=Conservative, 1=Balanced, 2=Aggressive)
await router.deposit(amount, riskLevel);
```

**Step 3: Wait for Batch Execution**
The batch executor will process your deposit along with others to save gas.

**Step 4: Claim Your Shares**
```javascript
// Claim vault shares after batch execution
await router.claimDepositShares(riskLevel);
```

### Making a Withdrawal

**Step 1: Approve Vault Shares**
```javascript
// Approve Router to spend your vault shares
await vault.approve(routerAddress, shares);
```

**Step 2: Queue Withdrawal**
```javascript
await router.withdraw(shares, riskLevel);
```

**Step 3: Claim USDC**
```javascript
// Claim USDC after batch execution
await router.claimWithdrawAssets(riskLevel);
```

---

## 🎯 Risk Levels

### 🛡️ Conservative Vault
**Target APY**: 6-8%  
**Strategy**: Focus on battle-tested, high-TVL protocols  
**Ideal For**: Capital preservation with stable yields

**Allocation Strategy:**
- Initial: 50% Protocol A + 50% Protocol B
- Rebalancing: APY-weighted based on actual performance
- Risk Mitigation: Quarterly strategy review

---

### ⚖️ Balanced Vault
**Target APY**: 8-12%  
**Strategy**: Mix of stable and moderate-yield opportunities  
**Ideal For**: Users seeking balanced risk-reward

**Allocation Strategy:**
- Initial: 50% Protocol A + 50% Protocol B
- Rebalancing: Dynamic APY optimization
- Diversification: Multiple protocol exposure

---

### 🚀 Aggressive Vault
**Target APY**: 12-20%+  
**Strategy**: Higher yield protocols, newer opportunities  
**Ideal For**: Risk-tolerant investors seeking maximum returns

**Allocation Strategy:**
- Initial: 50% Protocol A + 50% Protocol B
- Rebalancing: Frequent APY-based adjustments
- Risk Acceptance: Higher volatility tolerance

> **Note**: Currently, all vaults use identical allocation logic (equal split initially, then APY-weighted rebalancing). Future versions will implement risk-specific strategies.

---

## ⚙️ How It Works

### 1. **Deposit Flow**
```
User → Approve USDC → Deposit to Queue → Batch Execution 
→ Funds to Vault → Allocated to Strategies → Earning Yield
```

### 2. **Yield Generation**
- Strategies deploy capital to lending protocols
- Protocols generate interest on deposited USDC
- Yield is automatically harvested and compounded

### 3. **Rebalancing**
- Vault monitors APY across all strategies
- Periodically rebalances to maximize returns
- Withdraws from lower APY, deposits to higher APY

### 4. **Withdrawal Flow**
```
User → Approve Shares → Withdraw Request → Batch Execution 
→ Vault Withdraws from Strategies → User Receives USDC
```

---

## 🏁 Getting Started

### For Users
1. Visit **[growish.xyz](https://growish.xyz/)**
2. Connect your wallet to Lisk Sepolia
3. Get test USDC from the faucet
4. Choose your risk level and start earning!

### For Developers
```bash
# Clone the repository
git clone https://github.com/growinweb3/.github.git

# Install dependencies
npm install

# Run tests
npm test

# Deploy contracts
npm run deploy
```

---

## 🔐 Security

- All contracts are audited (link to audit report)
- Non-custodial: Users always control their funds
- Transparent: Open-source smart contracts
- Battle-tested: Built on proven DeFi primitives

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

---

## 📞 Contact & Community

- **Website**: [growish.xyz](https://growish.xyz/)
- **Twitter**: [@growishfi](https://twitter.com/growishfi)
- **Discord**: [Join our community](https://discord.gg/growish)
- **Documentation**: [docs.growish.xyz](https://docs.growish.xyz)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">
  
  **Built with ❤️ by the Growish Team**
  
  *Simplifying DeFi, One Yield at a Time*
  
</div>
