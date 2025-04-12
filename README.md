
# Auto Daily MegaETH Bot

This is an automated bot that interacts with the MegaETH blockchain to perform a series of transactions with specified wallets. The bot can swap tokens, mint test tokens, and deposit tokens into a specific router. It runs periodically (every 24 hours) and processes multiple wallets.

### Features
- **Token Swap:** Swap ETH for tokens using the `GTE_ROUTER`.
- **Token Minting:** Mint test tokens like `tkETH`, `tkUSDC`, `cUSD`, and `tkWBTC`.
- **Deposit Tokens:** Deposit specific tokens (`tkUSDC`) to a fixed ID on the TEKO router.
- **Retry Mechanism:** Automatically retries failed operations with exponential backoff.
- **Customizable:** Wallet and token configurations can be set up easily via a configuration file (`private_keys.txt`).
- **Scheduled Execution:** Runs the operations periodically every 24 hours.
  
## Setup

### Prerequisites

1. **Node.js**: Ensure you have [Node.js](https://nodejs.org/) installed. You can check this by running:
   ```bash
   node -v
   ```

2. **Install Dependencies**:
   Clone the repository and install the required dependencies using npm.

   ```bash
   git clone https://github.com/ganjsmoke/megaeth-daily.git
   cd megaeth-daily
   npm install web3@1.8.0
   ```

### Configuration

1. **Private Key File**: The bot expects a file named `private_keys.txt` in the root directory. This file should contain one private key per line, which is used to sign transactions for each wallet.

   Example of `private_keys.txt`:
   ```
   0xXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
   0xXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
   ```

2. **Token Configuration**: The bot swaps and mints tokens from the list defined in the `TokenListGTE` and `TokenTestTeko` arrays. You can customize these lists with your token contract addresses and amounts.


### Execution Flow

1. **Swap Tokens:** The bot will randomly choose a token from `TokenListGTE` and swap ETH for that token using the `GTE_ROUTER`.
2. **Mint Tokens:** The bot will mint a set of test tokens (e.g., `tkETH`, `tkUSDC`, `cUSD`, `tkWBTC`) by calling the `mint` function on each token contract.
3. **Deposit Tokens:** The bot will approve the `TEKO_ROUTER` and deposit a calculated percentage (3%) of the balance from the `tkUSDC` token to the specified address.

### Running the Bot

Run the bot by executing the following command:

```bash
node index.js
```

The bot will continuously run in a loop, processing each wallet and performing the configured operations. It will pause for random intervals between operations and retry failed operations up to three times with an increasing delay.

### Logging

The bot provides detailed logging at each step, including success and failure messages. If a step fails, the bot will retry the operation automatically with an increasing delay between attempts.

### Customization

- **Retry Config**: The number of retries and the initial delay between retries are configured in `RETRY_CONFIG`.
- **Cycle Interval**: The bot runs in a loop, processing wallets every 24 hours. This interval can be adjusted via `CYCLE_INTERVAL`.
- **Token List**: The `TokenListGTE` and `TokenTestTeko` arrays can be customized with different token addresses and amounts.



### Error Handling

If the bot encounters an issue (e.g., insufficient balance, failed transaction), it will log the error and retry the operation up to three times. If the error persists, it will move to the next operation.

### License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

> **Note**: This bot interacts with a blockchain and performs financial operations. Please use it responsibly and ensure that you are fully aware of the risks involved.
