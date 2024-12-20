# Cross-Chain Token Transfer with Wormhole SDK

This project demonstrates how to perform cross-chain token transfers using the [Wormhole SDK](https://github.com/wormhole-foundation/wormhole-sdk-ts). It supports transferring native tokens and specific assets (e.g., USDC) across different blockchain networks, including EVM-compatible chains (e.g., Ethereum, Avalanche) and Solana. The solution uses Wormhole's Testnet environment for demonstration purposes.

## Project Structure

The project is organized as follows:

```plaintext
cross-chain-transfer/
├── src/
│   ├── config/
│   │   └── usdc-addresses.ts   # Configuration file for USDC token contract addresses on supported chains
│   ├── helpers/
│   │   └── helpers.ts          # Helper functions for signer setup and environment variables
│   ├── scripts/
│   │   └── native-transfer.ts  # Script to perform a native token transfer between chains
│   │   └── usdc-transfer.ts    # Script to perform a USDC token transfer between chains
│   │   └── tx-recover.ts       # Script to recover and manually complete a token transfer using a transaction ID
├── .env                        # Environment variables for private keys (not included in the repo)
├── package.json                # Project dependencies and scripts
└── tsconfig.json               # TypeScript configuration
```

## Prerequisites

Ensure you have the following installed:

 - [Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) installed on your machine
 - A wallet with a private key, funded with [native tokens](https://faucets.chain.link/) (Testnet or Mainnet) for gas fees

## Setup and Usage

Follow these steps to clone the repository, set up environment variables, and perform token transfers.

**1. Clone the Repository**

```bash
git clone https://github.com/martin0995/WH-transfers.git
cd WH-transfers
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
SUI_PRIVATE_KEY="INSERT_SUI_MNEMONIC"
```

 - **ETH_PRIVATE_KEY** - private key for an Ethereum-compatible wallet
 - **SOL_PRIVATE_KEY** - private key for a Solana wallet
 - **SUI_PRIVATE_KEY** - mnemonic for a Sui wallet

>Important: For Sui, you must provide a mnemonic instead of a private key. Ensure these keys are valid and have the necessary permissions to perform transfers.

## Native Token Transfer

To initiate a native token transfer across chains, run:

```bash
npm run transfer:native
```

> Note: This script is set up to transfer a native token from Solana to Avalanche using the Wormhole SDK. You can modify the source and destination chains within `src/native-transfer.ts`.

## USDC Token Transfer

To transfer USDC from one chain to another, run:

```bash
npm run transfer:usdc
```

This script uses pre-configured USDC token addresses on Solana and Avalanche. If you are transferring to different chains or using other assets, update the address in `src/usdc-transfer.ts`.

## Recover and Manually Complete a Token Transfer

If a token transfer has been initiated but not completed, you can manually recover it and attempt to finish it using the transaction ID. This can be helpful in cases where the automatic process does not finalize the transfer.

**a. Set the Transaction ID:**

Open `src/tx-recover.ts` and provide the correct transaction ID (`txid`) for the transfer you want to recover. This ID will fetch the transfer details and attempt to complete it on the destination chain.

```typescript
// In src/tx-recover.ts
let recoverTxid = 'INSERT_YOUR_TRANSACTION_ID';
```

**b. Run the Recovery Command:**

Once you have set the transaction ID, run the following command:

```bash
npm run transfer:recover
```

## Configuration

You can customize the following options within the scripts:

 - **Source and Destination Chains** - modify `sendChain` and `rcvChain` in `native-transfer.ts` and `usdc-transfer.ts`
 - **Token Address** - change the token address if transferring assets other than the default USDC
 - **Amount and Transfer Settings** - adjust `amt`, `automatic`, and `nativeGas` to suit your needs

## Notes

 - Unlike other platforms, Sui requires a mnemonic instead of a private key for authentication. Ensure your `.env` file includes this correctly
 - Please make sure that the Wormhole Testnet is operational when running scripts
 - Check your wallet balances and transfer fees before initiating transfers
 - For production use, switch from Testnet to Mainnet and update the configuration accordingly

## Troubleshooting

 - **Missing environment variables** - ensure `.env` is correctly set up and keys are valid
 - **Unsupported platform error** - verify that the chains are compatible and supported by the Wormhole SDK
 - **Transaction Not Going Through** - if the transaction doesn't go through, check if the wrapped token exists on the destination chain. This issue is more common with native tokens
 - **Incomplete Transfers** - if a transfer was not completed, use `tx-recover.ts` to manually finish the transaction by providing the `txid`
