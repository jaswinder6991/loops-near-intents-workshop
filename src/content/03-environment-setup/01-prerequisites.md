Prerequisites and Installation

**Estimated Time:** 25 minutes  
**Prerequisites:** Basic command-line familiarity  
**Learning Objectives:**
- Install and configure the NEAR CLI
- Set up a NEAR account for testing
- Install Node.js and project dependencies
- Configure environment variables
- Verify your setup is working correctly

## Introduction

Now that you understand the concepts behind cross-chain swaps and the 1Click API, it's time to set up your development environment. We'll install the necessary tools and configure everything you need to start building.

## Required Tools Overview

You'll need these tools to complete the workshop:

1. **NEAR CLI** - For interacting with the NEAR blockchain
2. **Node.js and npm/yarn** - For running the TypeScript examples
3. **Git** - For cloning the workshop repository
4. **A NEAR account** - For executing transactions
5. **EVM wallet** - For cross-chain operations (optional)

Let's install each of these step by step.

## Step 1: Install NEAR CLI

The NEAR CLI is essential for blockchain interactions. We'll use the Rust-based CLI for the best performance.

**Web2 Parallel:** Installing NEAR CLI is like installing a specialized database client that lets you interact with the NEAR blockchain database from your terminal.

### Option A: Install via npm (Recommended)

Ensure you're not running in windows32 directory.  Run in your ~/Users/NAME directory

```bash
npm install -g near-cli-rs
```

### Option B: Install via Cargo (if you have Rust)
```bash
cargo install near-cli-rs
```

### Verify Installation
```bash
near --version
```

You should see output similar to:
```bash
near-cli-rs 0.7.0
```

> **Note:** If you see "command not found," you may need to restart your terminal or check your PATH configuration.

## Step 2: Create a NEAR Account

You'll need a NEAR account to interact with the Intents contract. Let's create one and fund it.

### Create an Implicit Account
An implicit account is defined by a cryptographic key pair rather than a human-readable name:

```bash
near account create-account sponsor-by-faucet-service <example-name.testnet> autogenerate-new-keypair print-to-terminal network-config testnet create
```

This will:
- Generate a new key pair
- Create an account ID (64 random characters)
- Save the credentials to a JSON file in `~/.near-credentials/implicit/`
- Display the file path where your account was saved

### Find Your Account ID
The CLI will save your account to a file and display something like:
```bash
The file "/Users/username/.near-credentials/implicit/c6fca557927e803b903013349b552edbceddd57a72d8b305d670655208d03665.json" was saved successfully
```

Your account ID is the filename (without the .json extension). In this example, it's:
`c6fca557927e803b903013349b552edbceddd57a72d8b305d670655208d03665`

**Alternative methods to find your account ID:**

**Method 1: Check the filename**
```bash
ls ~/.near-credentials/implicit/
```

**Method 2: View account details**
```bash
cat ~/.near-credentials/implicit/*.json
```

This will show all your accounts with their `implicit_account_id` field.

**Important:** Copy and save this account ID - you'll need it throughout the workshop.

### Get Your Private Key
You'll need your private key for the workshop scripts. Extract it directly from the JSON file:

```bash
cat ~/.near-credentials/implicit/YOUR_ACCOUNT_ID.json | grep -o '"private_key":"[^"]*"' | cut -d'"' -f4
```

Replace `YOUR_ACCOUNT_ID` with your actual account ID. This will output just the private key value:

```bash
ed25519:5hDAZYSw9GiFxL68c8pbxVfWXePM9Tx9DqxdhHsws16eWbiAuWNS1816bFDNKpeRZBUxHnFXGn6H6hnJKcYk4ha4
```

**Important:** Copy and save this complete private key value - you'll need it for the environment configuration.

## Step 3: Fund Your Account

Your new account needs NEAR tokens to pay for transaction fees.

> **Important:** NEAR Intents and the 1Click API only work on mainnet. You cannot use testnet for this workshop as the intent infrastructure is not available there.

### Option A: Request Funds at a Hackathon
If you're at a hackathon, approach a mentor to request mainnet NEAR funds.

### Option B: Use NEAR Intents Frontend
If you have funds on any supported chain:
1. Visit the [NEAR Intents frontend](mdc:https://intents.near.org)
2. Connect your wallet with existing funds
3. Swap some tokens to NEAR
4. Send NEAR to your new account

### Option C: Purchase NEAR Tokens
You can purchase NEAR tokens on any major exchange and send them to your account:
1. Buy NEAR on exchanges like Binance, Coinbase, or Kraken
2. Withdraw NEAR to your account address
3. Wait for confirmation (usually 1-2 minutes)

### Verify Your Balance
Check that your account has funds:
```bash
near account view-account-summary YOUR_ACCOUNT_ID network-config mainnet
```

You should see a balance greater than 0.

## Step 4: Clone the Workshop Repository

Get the workshop code:

```bash
git clone https://github.com/nearuaguild/near-intents-1click-example
cd near-intents-1click-example
```

## Step 5: Install Node.js Dependencies

The workshop uses TypeScript and several NEAR-related packages.

### Install Dependencies
```bash
# Using npm
npm install

# Or using Yarn
yarn install
```

### Verify Package Installation
Check that key packages are installed:
```bash
cd near-intents-1click-example
npm list @near-js/accounts
```

You should see the @near-js/accounts package version.

## Step 6: Configure Environment Variables

The workshop requires several environment variables for authentication.

### Copy the Example Environment File
```bash
cp .env.example .env
```

### Edit Your Environment File
Open `.env` in your preferred editor and fill in these values:

```bash
# Your NEAR account ID (the 64-character string from earlier)
ACCOUNT_ID=your_account_id_here

# Your NEAR private key (from the export command)
NEAR_PRIVATE_KEY=your_private_key_here

# Your EVM private key (optional, for cross-chain operations)
EVM_PRIVATE_KEY=your_evm_private_key_here
```

### EVM Private Key (Optional)
If you want to test cross-chain withdrawals, you'll need an EVM-compatible wallet:
- MetaMask private key
- Any Ethereum/Arbitrum wallet private key
- Can be a test wallet with minimal funds

> **Security Note:** Never use private keys from wallets containing significant funds. Create test wallets specifically for this workshop.

## Step 7: Verify Your Setup

Let's make sure everything is working correctly.

### Test NEAR CLI Connection
```bash
near account view-account-summary YOUR_ACCOUNT_ID network-config mainnet now
```

> **Note:** The `now` parameter tells NEAR CLI to use the latest block, avoiding interactive prompts that ask you to choose between "now" and previous blocks.

Expected output:
```bash
Account details for 'your-account-id':
  Balance: 0.1 NEAR
  Locked: 0 NEAR
  Storage used: 182 bytes
```

### Test Node.js Setup
```bash
node --version
npm --version
```

You should see version numbers for both.

### Test Environment Variables
Create a quick test file:

```bash
echo 'console.log("NEAR Account:", process.env.ACCOUNT_ID);' > test-env.js
node -r dotenv/config test-env.js
rm test-env.js
```

You should see your account ID printed.

## Step 8: Explore Available Tokens

Let's verify the 1Click API is accessible and see what tokens are available:

```bash
yarn run tokens
```

This script will:
- Connect to the 1Click API
- Fetch all supported tokens
- Display a table showing different token representations

Expected output:
```bash
┌─────────┬──────────────────────────┬─────────────────────┐
│ Token   │ Token ID                 │ Chain               │
├─────────┼──────────────────────────┼─────────────────────┤
│ ETH     │ nep141:eth.bridge.near   │ Ethereum Mainnet    │
│ ETH     │ nep141:arb.omft.near     │ Arbitrum            │
│ ETH     │ nep141:base.omft.near    │ Base                │
│ NEAR    │ nep141:wrap.near         │ NEAR                │
└─────────┴──────────────────────────┴─────────────────────┘
```

## Troubleshooting Common Issues

### NEAR CLI Not Found
- Restart your terminal
- Check if `~/.cargo/bin` is in your PATH (for Cargo installation)
- Try installing with npm instead of Cargo

### Account Creation Fails
- Ensure you have an internet connection
- Verify you're using the correct network (mainnet) for NEAR Intents
- Check if the account ID is already taken (for named accounts)

### Node.js Dependencies Fail
- Ensure you're using Node.js 16 or later: `node --version`
- Clear npm cache: `npm cache clean --force`
- Delete `node_modules` and reinstall: `rm -rf node_modules && npm install`

### Environment Variables Not Loading
- Ensure `.env` file is in the project root
- Check file permissions: `chmod 644 .env`
- Verify no extra spaces around the `=` signs

## Next Steps

Excellent! Your development environment is now set up and ready. You have:

- ✅ NEAR CLI installed and configured
- ✅ A funded NEAR account
- ✅ Project dependencies installed  
- ✅ Environment variables configured
- ✅ Verified connection to NEAR and 1Click API

Now let's start with your first cross-chain operation: depositing NEAR tokens into the Intents contract.

Continue to [NEAR Token Deposits](mdc:../04-cross-chain-deposits/01-near-deposits.md) 
