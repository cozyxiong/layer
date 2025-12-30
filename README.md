# Multi-Asset Restaking Protocol

A universal and modular **multi-asset restaking framework** for Ethereum Layer 2 networks and Actively Validated Services (AVS).

Inspired by EigenLayer's shared security model, this protocol allows users to restake arbitrary ERC-20 tokens and delegate their staking shares to professional operators. Operators can use the aggregated economic security to provide validation services, fast finality, or other active duties, while stakers earn additional yields.

## Contracts Overview

### StrategyBase
Universal base for all token-specific strategies.
- Floating exchange rate using virtual shares/balance offsets (prevents zero-share issues)
- Enforces per-deposit and total deposit limits
- Only callable by `StrategyManager`

### StrategyManager
Primary user interface.
- Manages strategy whitelist and third-party transfer restrictions
- Handles deposits (with optional EIP-712 signed gasless approval)
- Tracks per-user shares across all strategies

### DelegationManager
Core delegation and finality provider system.
- Operators register with earnings receiver and configurable staker exit delay
- Stakers delegate to operators (supports approver + replay protection)
- Two withdrawal paths:
    - `undelegate()` – personal full exit from delegation
    - `queueWithdrawals()` – operator-initiated batch withdrawals (self-withdrawal forbidden for security)
- Enforces minimum and per-strategy waiting periods before completion

### RewardManager
Distributes rewards from external sources.
- Proportional allocation between operator and stakers
- Configurable staker reward percentage
- Separate claim functions for operators and individual stakers

## Use Cases

- **Fast Finality Layer** for modular L2 chains
- **Dedicated Economic Security** for Actively Validated Services (AVS)
- **Multi-Asset Restaking Hub** supporting native tokens, LSTs, stablecoins, etc.