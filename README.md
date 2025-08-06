# FusioFantasyGameV2

A decentralized fantasy game contract built on Ethereum that allows users to compete in portfolio competitions using USDC tokens.

## Overview

FusioFantasyGameV2 is an upgradeable smart contract that manages fantasy portfolio competitions where users pay entry fees in USDC to participate, compete against each other, and win rewards based on their portfolio performance.

## Features

- **Portfolio Competitions**: Users create portfolios by paying USDC entry fees
- **Automated Prize Distribution**: Rewards are distributed based on portfolio performance
- **USDC Integration**: All transactions use USDC stablecoin
- **Admin Controls**: Role-based access control for game management
- **Upgradeable**: Built with OpenZeppelin's UUPS proxy pattern
- **Security**: Implements reentrancy protection and signature verification

## Contract Architecture

### Core Components

- **Game Management**: Create and manage individual game competitions
- **Portfolio System**: Track user portfolios and their associated games
- **Reward Distribution**: Automated reward assignment with signature verification
- **Fee Management**: Configurable admin fees for platform sustainability

### Key Functions

#### Game Creation
- `createGame()`: Create new portfolio competition games
- `updateGameStatus()`: Manage game lifecycle (ACTIVE → COMPLETED)

#### Portfolio Management
- `createPortfolio()`: Join games by creating portfolios with USDC entry fees
- `getPortfolioOwner()`: Retrieve portfolio ownership information

#### Reward System
- `assignReward()`: Assign rewards to individual portfolios
- `batchAssignRewards()`: Batch reward distribution for gas efficiency

#### User Management
- `withdrawBalance()`: Withdraw USDC rewards to user wallet
- `getUserBalance()`: Check user reward balance

## Technical Specifications

### Token
- **Primary Token**: USDC (USD Coin)

### Access Control
- **DEFAULT_ADMIN_ROLE**: Full administrative control
- **GAME_CREATOR_ROLE**: Game creation and management
- **REWARD_MANAGER_ROLE**: Reward distribution authorization

### Security Features
- Reentrancy protection on all external functions
- Signature verification for reward assignments
- Role-based access control
- Input validation and error handling

## Deployment

### Prerequisites
- Node.js >= 14.0.0
- Hardhat development environment
- USDC token address on target network

### Setup
1. Install dependencies:
```bash
npm install
```

2. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

3. Deploy contract:
```bash
npx hardhat run scripts/deploy_v2_testnet.js --network <network>
```

## Usage

### Creating a Game
```solidity
// Only GAME_CREATOR_ROLE can create games
createGame(
    gameId,           // uint256: unique game identifier
    startTime,        // uint256: game start timestamp
    endTime,         // uint256: game end timestamp
    entryFee,        // uint256: USDC entry fee amount
    entryCap         // uint256: maximum portfolio entries
);
```

### Joining a Game
```solidity
// Users create portfolios to join games
createPortfolio(gameId, portfolioId);
```

### Reward Distribution
```solidity
// REWARD_MANAGER_ROLE assigns rewards with signature verification
assignReward(portfolioId, amount, signature);
```

## Configuration

### Admin Settings
- **Admin Fee Percentage**: Configurable up to 50%
- **Admin Wallet**: Address for fee collection
- **Role Management**: Grant/revoke roles for different functions

### Game Parameters
- **Entry Fee**: Minimum USDC amount to participate
- **Entry Cap**: Maximum number of participants
- **Game Duration**: Configurable start and end times

## Events

Key events emitted by the contract:
- `GameCreated`: New game creation
- `PortfolioCreated`: New portfolio/join event
- `RewardAssigned`: Individual reward distribution
- `BatchRewardAssigned`: Batch reward distribution
- `BalanceWithdrawn`: User withdrawal events


## License

MIT
