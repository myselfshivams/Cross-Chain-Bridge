# Cross-Chain Asset Transfer System

## Overview
This project implements a cross-chain asset transfer system where assets can be locked on one blockchain and minted as a representation on another. The system ensures security, transparency, and proof-of-transfer mechanisms.

## Features Implemented
- **Lock & Mint Mechanism**: Users can lock ERC-20/ERC-721 tokens on Chain A and receive a minted equivalent on Chain B.
- **Proof of Transfer**: Every transfer generates a receipt with a hash, timestamp, sender, receiver, and amount.
- **Security Mechanisms**: Replay protection, contract access controls, input validation, and gas-efficient execution.
- **Wallet Connectivity**: Supports MetaMask and Wallet Connect for seamless interaction.
- **UI Features**: Displays balances, pending transfers, successful transactions, and logs.
- **Decentralized Relayers**: Off-chain relayer or oracle-based verification for cross-chain communication.

## Deployment Details
- **Backend**: Hosted on [Railway](https://railway.app/).
- **Frontend**: Hosted on [Vercel](https://hackiitk2.itshivam.me/).
- **Live Demo**: Please visit [Live Application](https://hackiitk2.itshivam.me/) to test the platform.
- **Smart Contracts Deployed At:**
  - **Sepolia (Ethereum Testnet):** [0x1E05c0521B744bbf303bfD32071AE1B88F2d1bA6](https://sepolia.etherscan.io/address/0x1E05c0521B744bbf303bfD32071AE1B88F2d1bA6#code)
  - **Amoy (Polygon Testnet):** [0xd5d5b65Cecab2F99EAe927c6552F05aEd993832c](https://amoy.polygonscan.com/address/0xd5d5b65Cecab2F99EAe927c6552F05aEd993832c#code)

## Frontend Features
- **Responsive and Modern UI**: Designed with a user-friendly and interactive interface.
- **Fetch Token Balances**: Retrieves balances from both Ethereum Sepolia and Polygon Amoy testnets.
- **Transaction History**: Displays historical transactions from both networks.
- **Live Updates**: Shows real-time transaction progress and confirmation.

## Getting Started

## How to Test Frontend Locally
1. Navigate to the frontend directory:
   ```sh
   cd frontend
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Start the development server:
   ```sh
   npm run dev
   ```
4. Open your browser and navigate to `http://localhost:3000/` to access the frontend UI.

## How to Test Smart Contracts Locally
1. Navigate to the contracts directory:
   ```sh
   cd contracts
   ```
2. Start a local Hardhat node:
   ```sh
   npx hardhat node
   ```
3. Deploy contracts to the local network:
   ```sh
   npx hardhat run scripts/deployA.js --network localhost
   npx hardhat run scripts/deployB.js --network localhost
   ```
4. Interact with contracts using Hardhat console:
   ```sh
   npx hardhat console --network localhost
   ```
5. Use MetaMask to connect to `http://localhost:8545/` by importing one of the test accounts generated by Hardhat.

### Running Tests
To verify the correctness of smart contracts and ensure security checks:
1. Navigate to the contracts directory:
   ```sh
   cd contracts
   ```
2. Run the test suite using Hardhat:
   ```sh
   npx hardhat test
   ```
3. View the test results and verify that all checks pass successfully.
1. Navigate to the contracts directory:
   ```sh
   cd contracts
   ```
2. Start a local Hardhat node:
   ```sh
   npx hardhat node
   ```
3. Deploy contracts to the local network:
   ```sh
   npx hardhat run scripts/deployA.js --network localhost
   npx hardhat run scripts/deployB.js --network localhost
   ```
4. Interact with contracts using Hardhat console:
   ```sh
   npx hardhat console --network localhost
   ```
5. Use MetaMask to connect to `http://localhost:8545/` by importing one of the test accounts generated by Hardhat.


### Prerequisites
Ensure you have the following installed:
- [Node.js](https://nodejs.org/)
- [Hardhat](https://hardhat.org/)
- [MetaMask](https://metamask.io/)
- [WalletConnect](https://walletconnect.com/)

### Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/myselfshivams/Cross-Chain-Bridge.git
   cd cross-chain-bridge
   ```
2. Install dependencies:
   ```sh
   npm install
   ```
3. Set up environment variables:
   ```sh
   cp contracts/.env.example contracts/.env
   # Edit .env with appropriate values
   ```

### Deploying Smart Contracts
1. Navigate to the `contracts` directory:
   ```sh
   cd contracts
   ```
2. Compile the contracts:
   ```sh
   npx hardhat compile
   ```
3. Deploy to testnets (Amoy & Sepolia):
   ```sh
   npx hardhat run scripts/deployA.js --network amoy
   npx hardhat run scripts/deployB.js --network sepolia
   ```

### Running the Frontend
1. Navigate to the frontend directory:
   ```sh
   cd frontend
   ```
2. Start the development server:
   ```sh
   npm run dev
   ```

## Smart Contract Details
- **Lock & Mint Contracts**: Handle token locking and minting across chains.
- **Event-Based Architecture**: Facilitates transfer tracking.
- **Relayer Integration**: Uses oracles, signature verification, or Merkle proofs.

### Key Smart Contracts & Functions
#### **Lock.sol**
- **Functions**: `lockERC20`, `lockERC721`, `unlock`, `grantRelayerRole`, `revokeRelayerRole`, `_isERC721`
- **Events**: `Locked`, `Unlocked`
- **Mappings**: `userNonce`, `lockRecords`
- **Modifiers**: `nonReentrant`

#### **ChainAGateway.sol**
- **Functions**: `lock`, `unlock`, `setChainBGateway`, `setMerkleRoot`, `verifySignature`, `splitSignature`
- **Events**: `Locked`, `Unlocked`
- **Mappings**: `processedNonces`

#### **ChainBGateway.sol**
- **Functions**: `mint`, `burn`, `setChainAGateway`, `setMerkleRoot`, `verifySignature`, `splitSignature`
- **Events**: `Minted`, `Burned`
- **Mappings**: `processedNonces`

#### **ChainGateway.sol**
- **Functions**: `setRelayer`, `lockAsset`, `unlockAsset`, `updateOwner`
- **Events**: `AssetLocked`, `AssetUnlocked`, `RelayerUpdated`, `OwnershipTransferred`, `RelayerProcessed`
- **Mappings**: `authorizedRelayers`
- **Modifiers**: `onlyOwner`, `onlyRelayer`

#### **ProofOfTransfer.sol**
- **Functions**: `logTransfer`, `getTransferProof`
- **Events**: `TransferLogged`
- **Mappings**: `receipts`

#### **TokenB.sol**
- **Functions**: `setGateway`, `mint`, `burn`, `totalSupply`, `balanceOf`, `transfer`, `allowance`, `approve`, `transferFrom`
- **Mappings**: `_balances`, `_allowances`
- **Modifiers**: `onlyGateway`

#### **MerkleProof.sol**
- **Functions**: `verify`, `processProof`, `multiProofVerify`, `processMultiProof`

#### **ReentrancyGuard.sol**
- **Functions**: `_nonReentrantBefore`, `_nonReentrantAfter`, `_reentrancyGuardEntered`
- **Modifiers**: `nonReentrant`
- **Lock & Mint Contracts**: Handle token locking and minting across chains.
- **Event-Based Architecture**: Facilitates transfer tracking.
- **Relayer Integration**: Uses oracles, signature verification, or Merkle proofs.

## Security Measures
- **Reentrancy Protection**: Prevents malicious contract calls.
- **Access Controls**: Restricts unauthorized contract interactions.
- **Replay Attack Prevention**: Ensures transactions cannot be duplicated.
- **Gas Optimization**: Efficient execution of transactions.
- **Merkle Proofs**: Implemented in `ChainAGateway.sol`, `ChainBGateway.sol`, and `MerkleProof.sol` for secure transaction validation.
- **Modifiers**: Used in `ChainGateway.sol`, `Lock.sol`, `ReentrancyGuard.sol`, and `TokenB.sol` for restricting function execution.
- **OnlyOwner Restriction**: Enforced in `ChainAGateway.sol`, `ChainBGateway.sol`, `ChainGateway.sol`, and `TokenB.sol` to limit administrative actions.
- **Reentrancy Guard**: Implemented in `ReentrancyGuard.sol` to prevent multiple function calls.
- **Require Statements**: Used extensively in `ChainAGateway.sol`, `ChainBGateway.sol`, `ChainGateway.sol`, `Lock.sol`, `MerkleProof.sol`, `ProofOfTransfer.sol`, and `TokenB.sol` to enforce conditions and security checks.
- **Reentrancy Protection**: Prevents malicious contract calls.
- **Access Controls**: Restricts unauthorized contract interactions.
- **Replay Attack Prevention**: Ensures transactions cannot be duplicated.
- **Gas Optimization**: Efficient execution of transactions.

## Future Enhancements
- **Fully Decentralized Relayers**: Remove reliance on centralized infrastructure.


## Our Team
We are a dedicated team of blockchain developers, cloud/backend developers, full stack developers, software engineers, and security experts passionate about decentralized finance and improving blockchain accessibility. Our goal is to create seamless, secure, and efficient blockchain solutions.

- [Shivam](https://github.com/myselfshivams)
- [Ritik Gupta](https://github.com/ritikgupta06)
- [Sanskar Soni](https://github.com/sunscar-sony)
- [Parth Agarwal](https://github.com/TheInfernitex)
- [Ashish Verma](https://github.com/AshishJii)



[![Contributors](https://contrib.rocks/image?repo=myselfshivams/Gasless-Forwarder)](https://github.com/myselfshivams/Cross-Chain-Bridge/contributors)

---

## Project Demonstration
Watch our project demonstration video here: [YouTube](#)

---

## Acknowledgment
Special thanks to HACKIITK for organizing this hackathon.


