## 🔹 Overview

This repository contains two Solidity smart contracts:

1. **`sample.sol` – Ownable Contract**
   A basic ownership pattern where only the owner can execute certain functions.

2. **`bankDemo.sol` – SimpleBank Contract**
   A lightweight banking-style smart contract supporting deposits, withdrawals, transfers, and balance tracking.

Both contracts are written for Solidity **0.8.x** and demonstrate fundamental blockchain development patterns.

---

## 🔗 Wallet & Test ETH Setup

For deploying and testing these contracts, MetaMask was used as the primary Ethereum wallet.

🌐 MetaMask Wallet

MetaMask was connected to Remix using the Injected Provider option, allowing seamless interaction with the blockchain during deployment and contract testing.

💧 Test ETH (0.05 ETH from Google Cloud)

To perform deposits, withdrawals, and transfers on the test network, I obtained 0.05 ETH from the Google Cloud faucet, which provides free test ETH for development purposes.

This test ETH was then used for:

Deploying the Ownable contract

Deploying the SimpleBank contract

Executing deposit/withdraw/transfer transactions inside the bank contract

## 📁 Project Structure

```
/contracts
   ├── sample.sol        // Ownable example contract
   └── bankDemo.sol      // SimpleBank / transaction demo contract
```

---

# 🧩 1. sample.sol — Ownable Contract

### 🔍 Description

The `Ownable` contract implements a simple ownership system:

* The **deployer becomes the owner**.
* The `onlyOwner` modifier restricts functions to the owner.
* Owners can hand over ownership.
* Some functions are owner-only, others are open to everyone.

### 🛠 Key Functions

| Function               | Description                                       |
| ---------------------- | ------------------------------------------------- |
| `setOwner(address)`    | Transfers ownership to a new address. Owner-only. |
| `onlyOwnerCanAccess()` | Example restricted function.                      |
| `anyOneCanAccess()`    | Function callable by anyone.                      |

### 📌 Code Summary

```solidity
constructor() {
    owner = msg.sender;
}

modifier onlyOwner() {
    require(msg.sender == owner, "not owner");
    _;
}
```

A very common pattern used in secure smart contract design.

---

# 🏦 2. bankDemo.sol — SimpleBank Contract

### 🔍 Description

`SimpleBank` stores ETH balances for users inside a smart contract.
Users can:

* **Deposit** ETH
* **Withdraw** ETH
* **Transfer** balance to another on-chain user
* **Check their balance**

### 🛠 Key Features

| Feature      | Description                                |
| ------------ | ------------------------------------------ |
| Deposit      | Users send ETH into the contract.          |
| Withdraw     | Users withdraw stored ETH to their wallet. |
| Transfer     | Move balance from one user to another.     |
| View Balance | Public balance lookup function.            |

### 📌 Main Functions

```solidity
function deposit() external payable;
function withdraw(uint256 amount) external;
function transfer(address to, uint256 amount) external;
function getBalance(address user) external view returns (uint256);
```

### 🔒 Events

Events help track activity:

* `Deposit(address user, uint256 amount)`
* `Withdrawal(address user, uint256 amount)`
* `Transfer(address from, address to, uint256 amount)`

---

# 🚀 Deploying the Contracts (Remix + MetaMask)

1. Open **[https://remix.ethereum.org](https://remix.ethereum.org)**
2. Create two files: `sample.sol` and `bankDemo.sol`
3. Compile both using Solidity **0.8.x**
4. Connect MetaMask
   → *Deploy & Run* → **Injected Provider**
5. Deploy the contracts

---

# 💰 Using the SimpleBank Contract

### Deposit ETH

1. Enter a value in the Remix "Value" field (in wei).
2. Click **deposit()**.
3. Confirm transaction in MetaMask.

### Withdraw ETH

```
withdraw(amount)
```

Amount must be in **wei**.

### Transfer

```
transfer(0xRecipientAddress, amount)
```

### Check Balance

```
getBalance(0xUserAddress)
```
