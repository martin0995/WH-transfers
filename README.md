# Cross-Chain Token Transfer with Wormhole SDK

This project demonstrates how to perform cross-chain token transfers using the Wormhole SDK. It supports transferring native tokens and specific assets (e.g., USDC) across different blockchain networks, including EVM-compatible chains (e.g., Ethereum, Avalanche) and Solana. The solution uses Wormhole's Testnet environment for demonstration purposes.

## Project Structure

The project is organized as follows:

```plaintext
cross-chain-transfer/
├── src/
│   ├── helpers/
│   │   └── helpers.ts    # Helper functions for signer setup and environment variables
│   ├── transfer.ts       # Script to perform a native token transfer between chains
│   └── usdc-transfer.ts  # Script to perform a USDC token transfer between chains
├── .env                  # Environment variables for private keys (not included in the repo)
├── package.json          # Project dependencies and scripts
└── tsconfig.json         # TypeScript configuration
```

## Prerequisites

Ensure you have the following installed:

 - [Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) installed on your machine
 - A wallet with a private key, funded with [native tokens](https://faucets.chain.link/) (Testnet or Mainnet) for gas fees

## Setup and Usage

Follow these steps to clone the repository, set up environment variables, and perform token transfers.

**1. Clone the Repository**

```bash
git clone https://github.com/your-username/cross-chain-transfer.git
cd cross-chain-transfer
```

**2. Install Dependencies**

```bash
npm install
```

**3. Set Up Environment Variables**

Create a `.env` file in the root directory and add your private keys:

```bash
ETH_PRIVATE_KEY="INSERT_PRIVATE_KEY"
SOL_PRIVATE_KEY="INSERT_PRIVATE_KEY"
```

 - ETH_PRIVATE_KEY - private key for an Ethereum-compatible wallet
 - SOL_PRIVATE_KEY - private key for a Solana wallet

Ensure these keys are valid and have the necessary permissions to perform transfers.

**4. Compile the TypeScript Files (Optional)**

This step is optional as scripts will compile automatically during execution. However, to manually compile:

```bash
npx tsc
```

**5. Perform a Native Token Transfer**

To initiate a native token transfer across chains, run:

```bash
npm run transfer
```

> Note: This script is set up to transfer a native token from Solana to Avalanche using the Wormhole SDK. You can modify the source and destination chains within `src/transfer.ts`.

**6. Perform a USDC Token Transfer**

To transfer USDC from one chain to another, run:

```bash
npm run transfer:usdc
```

This script uses pre-configured USDC token addresses on Solana and Avalanche. Update the address in `src/usdc-transfer.ts` if transferring to different chains or using other assets.

## Configuration

You can customize the following options within the scripts:

 - Source and Destination Chains - Modify sendChain and rcvChain in `transfer.ts` and `usdc-transfer.ts`
 - Token Address - Change the token address if transferring assets other than the default USDC
 - Amount and Transfer Settings - Adjust amt, automatic, and nativeGas to suit your needs

## Notes

 - Ensure that the Wormhole Testnet is operational when running scripts.
 - Check your wallet balances and transfer fees before initiating transfers.
 - For production use, switch from Testnet to Mainnet and update configuration accordingly.

## Troubleshooting

 - Missing environment variables: Make sure `.env` is properly set up and keys are valid.
 - Unsupported Platform Error: Verify that the chains are compatible and supported by the Wormhole SDK.
