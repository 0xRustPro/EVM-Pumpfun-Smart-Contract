# PumpFun EVM Smart Contract

A decentralized token launchpad platform for EVM-compatible blockchains, enabling one-click token creation with integrated bonding curve mechanics and automatic Uniswap liquidity migration.

## Overview

The PumpFun EVM Smart Contract brings the viral token launch experience to EVM-compatible chains, starting with Monad. This implementation provides a complete on-chain solution for token creation, trading through bonding curves, and seamless migration to established DEX protocols.

### Core Functionality

- **Token Creation**: Deploy customizable ERC-20 tokens with custom names, symbols, and total supply
- **Bonding Curve Trading**: Linear bonding curve implementation for price discovery and early buyer rewards
- **Automated Liquidity Management**: Embedded bonding curve handles all buy/sell operations without requiring initial AMM setup
- **Uniswap Integration**: Automatic liquidity migration to Uniswap V2/V3 once threshold is reached
- **Fully On-Chain**: All logic executed on-chain for maximum transparency and decentralization
- **EVM Compatibility**: Built with Solidity and compatible with standard Ethereum development tooling

## Technical Architecture

### Smart Contract Structure

- **PumpToken**: Minimal ERC-20 token implementation deployed via factory pattern
- **PumpCloneFactory**: Main factory contract managing token creation, bonding curve operations, and liquidity migration

### Bonding Curve Mechanics

The contract implements a linear bonding curve that determines token prices based on reserve ratios:
- Virtual reserves (vReserve) track the bonding curve state
- Real reserves (rReserve) track actual ETH and token balances
- Price increases as tokens are purchased and decreases as tokens are sold

### Liquidity Migration

When sufficient volume is reached on the bonding curve, liquidity is automatically migrated to Uniswap, enabling:
- Continuous trading on established DEX infrastructure
- Real-time pricing through AMM mechanisms
- Integration with broader DeFi ecosystem

## Technology Stack

- **Smart Contract Language**: Solidity ^0.8.28
- **Target Network**: Monad Testnet (mainnet-ready)
- **DEX Integration**: Uniswap V2 Router
- **Security**: OpenZeppelin Contracts (Ownable, ReentrancyGuard)
- **Development Tools**: Hardhat, Ethers.js, TypeScript

## Installation

### Prerequisites

- Node.js >= 16.x
- npm or yarn package manager
- Hardhat development environment

### Setup

```bash
# Clone the repository
git clone EVM-Pumpfun-Smart-Contract
cd EVM-Pumpfun-Smart-Contract

# Install dependencies
npm install

# Compile contracts
npx hardhat compile

# Run tests (if available)
npx hardhat test
```

## Deployment

### Configuration

1. Set up environment variables in `.env`:
```
PRIVATE_KEY=your_private_key
MONAD_RPC_URL=your_rpc_url
UNISWAP_ROUTER_ADDRESS=router_address
```

2. Update `hardhat.config.ts` with network configuration

### Deploy Factory Contract

```bash
npx hardhat run scripts/deployPump.ts --network monad-testnet
```

## Usage

### Launching a Token

```solidity
// Call launchToken with token name and symbol
factory.launchToken("My Token", "MTK");
```

The creator receives an initial allocation of tokens (1 ETH worth), and the bonding curve is initialized.

### Buying Tokens

```solidity
// Purchase tokens by sending ETH to the factory
// Tokens are minted based on bonding curve calculation
factory.launchToken("Token Name", "SYMBOL");
// or for existing tokens:
// Send ETH directly with appropriate call data
```

### Selling Tokens

```solidity
// Sell tokens back through the bonding curve
factory.sellToken(tokenAddress, amount);
```

## Contract Parameters

### Configurable Settings

- **V_ETH_RESERVE**: Initial virtual ETH reserve (default: 0.015 ETH)
- **V_TOKEN_RESERVE**: Initial virtual token reserve (default: 1,073,000,000 tokens)
- **R_TOKEN_RESERVE**: Initial real token reserve (default: 793,100,000 tokens)
- **TRADE_FEE_BPS**: Trading fee in basis points (default: 100 = 1%)
- **LIQUIDITY_MIGRATION_FEE**: Fee for liquidity migration (default: 0.018 ETH)

These parameters can be updated by the contract owner via admin functions.

## Verified Deployment

### Monad Testnet

**Factory Contract**: [`0x802Bbb3924BEE46831cadD23e9CfA9e74B499Efb`](https://testnet.monadexplorer.com/address/0x802Bbb3924BEE46831cadD23e9CfA9e74B499Efb)

### Example Transactions

- [Token Launch](https://testnet.monadexplorer.com/tx/0x44ce82f48eabc5e5f1be7bfb6414d380071a4993cd458b191d571568bb2c3190)
- [Token Purchase](https://testnet.monadexplorer.com/tx/0xaf91c0e9254248b27310652da1c1bdfbf7a40d88cf7c72b0fabbd76ce24ec160)
- [Token Sale](https://testnet.monadexplorer.com/tx/0x3058ceca20593a1acff0e4c3534a92243ff554dc951f40e61a87476b75c29e9d)
- [Liquidity Migration to Uniswap](https://testnet.monadexplorer.com/tx/0x1dd9da4ec6acab116cc2b4a24c97ff5e6a93a0fe5ce0c8413436a0489243cad2)

## Security Considerations

- Contract uses OpenZeppelin's `ReentrancyGuard` to prevent reentrancy attacks
- Owner-controlled parameters allow for emergency updates if needed
- All token operations are validated on-chain
- Bonding curve calculations are deterministic and transparent

## Development Status

- ✅ Core bonding curve implementation
- ✅ Token creation and trading
- ✅ Uniswap liquidity migration
- ⚠️ Currently deployed on Monad Testnet (awaiting mainnet release)
- 📊 Dashboard and analytics (planned)

## Limitations & Notes

- Currently operational on Monad Testnet only
- Bonding curve parameters are fixed per deployment (adjustable by owner)
- Liquidity migration requires minimum volume threshold
- Bonding curve mechanics are based on the original Pump.fun Solana implementation

## Contributing

Contributions are welcome! Please feel free to submit pull requests, open issues for bugs or feature requests, and suggest improvements to the protocol.

### Development Guidelines

1. Fork the repository
2. Create a feature branch
3. Make your changes with appropriate tests
4. Submit a pull request with a clear description

## Credits & Inspiration

This implementation is inspired by the original [Pump.fun Solana Smart Contract](https://github.com/0xRustPro/EVM-Pumpfun-Smart-Contract), adapted and enhanced for EVM-compatible blockchain infrastructure.


## Contact

For inquiries, integration support, or collaboration opportunities:


