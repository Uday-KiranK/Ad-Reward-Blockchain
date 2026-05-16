# AdReward: Decentralized Advertising Reward System

AdReward is a Web2.5 decentralized advertising platform that leverages Ethereum smart contracts and a cryptographic Proof-of-View (PoV) mechanism. It allows advertisers to fund campaigns with ERC-20 tokens (AdRewardToken - ART) and rewards users directly for watching ads, completely bypassing centralized intermediaries.

## 🌟 Features
- **Direct Rewards:** Users earn ART directly to their MetaMask wallets for watching ads.
- **Sybil Resistance:** Phone-based OTP verification ensures 1 human = 1 wallet.
- **Proof-of-View (PoV):** Cryptographic ECDSA signatures guarantee that only legitimate, completed watch sessions can claim on-chain rewards.
- **Anti-Cheat:** Built-in client-side protections against time-skipping, tab-switching, and spoofing.
- **Built-in DEX:** Buy and sell ART tokens directly via the TokenSale smart contract.

---

## 🛠️ Tech Stack
- **Blockchain:** Ethereum, Solidity, Hardhat, Ethers.js (v6)
- **Backend:** Node.js, Express.js, PostgreSQL
- **Frontend:** Vanilla HTML5, CSS3, JavaScript
- **Wallet Integration:** MetaMask

---

## ⚙️ Prerequisites

Before you begin, ensure you have the following installed:
1. [Node.js](https://nodejs.org/) (v18+)
2. [PostgreSQL](https://www.postgresql.org/) (v14+)
3. [MetaMask Browser Extension](https://metamask.io/)

---

## 🚀 Setup & Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Uday-KiranK/Ad-Reward-Blockchain.git
cd Ad-Reward-Blockchain
```

### 2. Install Dependencies
You need to install dependencies for the root, backend, and frontend.
```bash
# Install hardhat/contract dependencies
npm install

# Install backend dependencies
cd backend
npm install
cd ..

# Install frontend dependencies (if any)
cd frontend
npm install
cd ..
```

### 3. Database Setup
1. Open PostgreSQL (via pgAdmin or psql CLI).
2. Create a new database named `adreward`.
```sql
CREATE DATABASE adreward;
```

### 4. Environment Variables
Create a `.env` file in the root directory (or wherever your `server.js` expects it) and add the following configuration:

```ini
# Blockchain Configuration
SEPOLIA_RPC_URL=https://ethereum-sepolia.publicnode.com
PRIVATE_KEY=your_wallet_private_key_here

# PostgreSQL Database Configuration
DB_USER=postgres
DB_HOST=localhost
DB_NAME=adreward
DB_PASSWORD=your_postgres_password_here
DB_PORT=5432
```
*(Note: Never commit your real private key to GitHub!)*

---

## 💻 Running the Application

To run the application locally, you will need to open **two separate terminal windows**.

### Terminal 1: Start the Backend Server
The backend handles phone verification (KYC), tracks watch sessions in PostgreSQL, and generates the cryptographic Proof-of-View signatures.

```bash
cd backend
node server.js
```
*(You should see "Server running on port 3001" and "Database Connected")*

### Terminal 2: Start the Frontend Application
The frontend serves the user interface and connects to MetaMask.

```bash
cd frontend
npx serve .
```
*(This will host the site at `http://localhost:3000`)*

---

## ⛓️ Smart Contract Deployment

If you make changes to the Solidity contracts in `/contracts`, you will need to re-deploy them.

**To deploy to the local Hardhat network:**
```bash
npx hardhat node # (Run this in a separate terminal)
npx hardhat run scripts/deploy.js --network localhost
```

**To deploy to the Sepolia Testnet:**
```bash
npx hardhat run scripts/deploy.js --network sepolia
```

**⚠️ IMPORTANT:** After deploying, you **MUST** copy the new contract addresses generated in the terminal and paste them into the `config` object at the very top of `frontend/app.js`.

---

## 📱 How to Use the App

1. **Sign Up:** Go to `http://localhost:3000/auth.html`. Enter your phone number to receive an OTP (which will log to your backend terminal window).
2. **Link Wallet:** Once verified, MetaMask will prompt you to connect. This links your phone number to your exact Ethereum address.
3. **Advertisers:** Navigate to the "Create Campaign" tab, fund it with ART, and launch your ad.
4. **Users:** Navigate to the "Watch & Earn" tab. Watch the video without skipping or changing tabs. Once it finishes, a "Claim Reward" button will appear.
5. **Claiming:** Clicking claim will verify your session with the backend, generate a cryptographic signature, and prompt your MetaMask to execute the transaction on the blockchain!

---

## 👥 Contributors
- Rajesh M
- Uday Kiran K
- **Supervisor:** Dr. Sunil Kumar P V (IIIT Dharwad)
