# Growinweb3

Welcome to **Growinweb3** — building innovative DeFi solutions for Web3.

## 🚀 Our Project: DeFi Yield Aggregator

A gas-optimized yield aggregator protocol built on **Lisk Sepolia Testnet** that enables users to earn yield through multiple DeFi strategies with a batch deposit/withdraw system.

### ✨ Key Features

- **Batch Deposit System** — Gas costs shared among all users through periodic batch execution
- **Multiple Risk Profiles** — Conservative, Balanced, and Aggressive vaults with different yield strategies
- **Automated Execution** — Batches execute every 6 hours via automated keepers
- **Multi-Strategy Yield** — Integration with Aave and Compound protocols

### 🏗️ Architecture

```
User → Router (Queue) → Batch Execution → Vault → Strategies (Aave/Compound)
```

**Core Components:**
- **Router** — Main entry point for deposits/withdrawals with batch queuing
- **Vaults** — Asset managers for different risk levels
- **Strategies** — Yield generators connecting to external DeFi protocols

### 💼 Vault Risk Levels

| Risk Level | Vault | Strategy Allocation |
|------------|-------|---------------------|
| Conservative | Low Risk | 80% Aave, 20% Compound |
| Balanced | Medium Risk | 50% Aave, 50% Compound |
| Aggressive | High Risk | 30% Aave, 70% Compound |

## 📦 Repositories

### [Frontend](https://github.com/growinweb3/frontend)

The frontend application for interacting with the yield aggregator.

**Tech Stack:**
- Next.js 16 with TypeScript
- wagmi & viem for Web3 interactions
- @xellar/kit for wallet connections
- TailwindCSS for styling
- Radix UI components

**Features:**
- Wallet connection (MetaMask, WalletConnect, Xellar Passport)
- Deposit & withdrawal interface with batch awareness
- Transaction history tracking
- Real-time balance updates
- Test token faucet for development

**Quick Start:**
```bash
cd aggregator
pnpm install
pnpm dev
```

## 🌐 Network Information

**Lisk Sepolia Testnet**
- Chain ID: `4202`
- RPC URL: `https://rpc.sepolia-api.lisk.com`
- Block Explorer: `https://sepolia-blockscout.lisk.com`

## 📄 Smart Contracts

**Deployed Contracts (Lisk Sepolia):**

| Contract | Address |
|----------|---------|
| Router | `0x7dC0da00F845A4272C08E51a57651ac004f5e0C7` |
| MockUSDC | `0x6f576F9A89555b028ce97581DA6d10e35d433F04` |
| Conservative Vault | `0x6E69Ed7A9b7F4b1De965328738b3d7Bb757Ea94c` |
| Balanced Vault | `0x21AF332B10481972B903cBd6C3f1ec51546552e7` |
| Aggressive Vault | `0xc4E50772bd6d27661EE12d81e62Daa4882F4E6f4` |
| Aave Strategy | `0x85A1B6A61C5E73418A40A3a79F6E811Ee848dAa7` |
| Compound Strategy | `0x4B29149492019fE65D0363097728Cab61Cb97F0f` |

## 🔄 How It Works

### Deposit Flow
1. **Queue** — Approve USDC and call `deposit(amount, riskLevel)` on Router
2. **Wait** — Batch executes every 6 hours
3. **Claim** — Call `claimDepositShares(riskLevel)` to receive vault shares

### Withdraw Flow
1. **Queue** — Approve vault shares and call `withdraw(shares, riskLevel)` on Router
2. **Wait** — Batch executes every 6 hours
3. **Claim** — Call `claimWithdrawAssets(riskLevel)` to receive USDC

## 🛠️ Development

### Prerequisites
- Node.js 18+
- pnpm package manager
- Web3 wallet (MetaMask recommended)

### Getting Test Tokens
Use the built-in Test Token Faucet in the frontend to mint 1,000 USDC for testing.

## 📚 Documentation

- [Web3 Implementation Guide](https://github.com/growinweb3/frontend/blob/main/aggregator/WEB3_IMPLEMENTATION.md)
- [Frontend Integration Brief](https://github.com/growinweb3/frontend/blob/main/aggregator/frontend-brief.md)
- [Testing Guide](https://github.com/growinweb3/frontend/blob/main/aggregator/TESTING_GUIDE.md)
- [Diagnostic Guide](https://github.com/growinweb3/frontend/blob/main/aggregator/DIAGNOSTIC_GUIDE.md)

## 🤝 Contributing

We welcome contributions! Please feel free to submit issues and pull requests to our repositories.

## 📜 License

See individual repositories for license information.