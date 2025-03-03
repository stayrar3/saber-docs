---
sidebar_position: 1
---
# Technical Architecture

## System Components and Interactions

The Saber Protocol is built as a modular system where specialized components work together to create a complete ecosystem. The diagram below illustrates the high-level architecture and interaction patterns between components:

```
┌────────────────────────────────────────────────────────────────────┐
│                          SABER PROTOCOL                             │
└────────────────────────────────────────────────────────────────────┘
                                   │
                                   │
            ┌────────────────────┬─┴─┬────────────────────┐
            │                    │   │                    │
            ▼                    ▼   ▼                    ▼
┌────────────────────┐  ┌─────────────────┐    ┌────────────────────┐
│                    │  │                 │    │                    │
│  STABLE-SWAP       │  │  POOL MANAGER   │    │  QUARRY            │
│  PROGRAM           │◄─┼─┐               │    │  PROGRAM           │
│                    │  │ │               │    │                    │
└────────────────────┘  │ │               │    └─────────┬──────────┘
            ▲           │ │               │              │
            │           │ │               │              │
            │           │ └──────┐        │              │
            │           │        ▼        │              │
            │           │  ┌────────────┐ │              │
            │           │  │  POOLS     │ │              │
            └───────────┼──┤            │ │              │
                        │  └────────────┘ │              │
                        └─────────────────┘              │
                                 ▲                       │
                                 │                       │
                                 │                       │
                        ┌────────┴────────┐              │
                        │                 │              │
┌───────────────────┐   │  TRIBECA        │    ┌─────────┴──────────┐
│                   │   │  GOVERNANCE     │    │                    │
│  GOKI             │◄──┤                 │◄───┤  MINERS            │
│  SMART WALLET     │   │                 │    │                    │
│                   │   │                 │    │                    │
└───────────────────┘   └─────────────────┘    └────────────────────┘
```

## Component Relationships

### Core Exchange Components

1. **StableSwap ↔ Pool Manager**:
   - Pool Manager creates and administers StableSwap pools
   - StableSwap handles the core swap mechanics and liquidity provision

2. **Pool Manager → Pools**:
   - Pool Manager controls fees and administrative functions
   - Maintains a registry of available pools
   - Each pool represents a trading pair in the system
   - Pools direct fees to the protocol beneficiary

### Liquidity Mining Components

1. **Quarry → Miners**:
   - Quarry program manages reward distribution
   - Miners represent staked positions in the system
   - LP tokens from StableSwap are staked in Quarry to earn additional yield incentives

### Governance Components

1. **Tribeca ↔ Goki Smart Wallet**:
   - Tribeca provides governance framework
   - Goki Smart Wallet executes approved governance decisions
   - Multi-signature security for treasury and administrative functions
   - Governance can update parameters across all components
   - Controls protocol fees, reward rates, and system configuration

## Data Flow: User Interactions

### Liquidity Provision Flow

1. User deposits token pairs to StableSwap pool
2. Pool Manager tracks the pool in the registry  
3. User receives LP tokens representing their share
4. User can stake LP tokens in Quarry to earn SBR rewards
5. User can vote on governance with locked SBR tokens (veSBR)

### Governance Flow

1. SBR token holders lock tokens in Tribeca (veSBR)
2. Governance proposals are created and voted on
3. Approved proposals are queued in Goki Smart Wallet
4. After timelock period, proposals are executed

## Protocol Extension Points

The architecture provides several extension points for future development:

1. **New Pool Types**:
   - Pool Manager can be extended for new asset types
   - Additional swap curves could be implemented

2. **Additional Incentives**:
   - Quarry can support new mining strategies
   - Merge-mining allows for complex reward structures

3. **Cross-Protocol Integration**:
   - Standardized interfaces allow other protocols to build on Saber
   - LP tokens can be used in other DeFi protocols