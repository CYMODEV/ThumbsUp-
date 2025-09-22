# ThumbsUp-
ThumbsUp.app is a mobile‑first, real‑time feedback platform that transforms quick reactions into valuable, owned digital assets. In one tap, users can like, vote, or rate — no login required — and earn Thumbs Tokens for meaningful participation. The platform blends instant engagement, crypto‑powered rewards, and token‑weighted scalable ecosystem.
# ThumbsUp.app – Development Disclosure & Public Notice
**Timestamp:** 2025‑09‑03 (Central Daylight Time)  
**Author:** Project Team  
**Project:** ThumbsUp.app – Crypto‑Enabled Real‑Time Feedback Platform

---

## 1. Purpose of Disclosure
This document serves as a **public disclosure** of the concepts, designs, and technical methods underlying ThumbsUp.app.  
It is intended to:
- Establish a **public record** of the invention and its features as of the timestamp above.
- Support intellectual property filings (utility patents, design patents, trademarks).
- Provide transparency for collaborators, contributors, and potential licensees.

---

## 2. Summary of the Invention
ThumbsUp.app is a **mobile‑first, real‑time feedback platform** that enables:
- **One‑tap feedback** (likes, polls, ratings) without requiring user login.
- **Multi‑layer sentiment capture** (binary + qualitative tags in a single interaction).
- **Live poll aggregation** with optional **bias‑correction algorithms**.
- **Crypto‑integrated rewards** via a native **Thumbs Token**.
- **Token‑weighted governance** for platform features and rules.
- **Tipping/gratuity flows** for creators, event hosts, and contributors.
- **Cross‑sector deployment** in retail, education, events, civic engagement, and more.

---

## 3. Key Components
### 3.1 Feedback Engine
- Real‑time polling and sentiment capture.
- Quality scoring algorithm to reward valuable contributions.
- Poll sponsorship marketplace.

### 3.2 Token Economy
- **Thumbs Token** for rewards, tips, sponsorships, and NFT badges.
- Feedback‑to‑earn model with on‑chain settlement.
- Integration with Ethereum L2 for low‑cost transactions.

### 3.3 Governance DAO
- Token‑weighted voting on feature prioritization and platform rules.
- Proposal submission and decision tracking.

### 3.4 Registries
- **People Registry** – Roles, verification, wallet address, engagement history.
- **Places Registry** – Location type, geo‑coordinates, owner, active polls/events.
- **Things Registry** – Item category, owner, associated polls, tokenization status.

---

## 4. Novel Features Claimed
1. **Frictionless, No‑Login Feedback Flow** with token‑based validation.
2. **Single‑Action Binary + Sentiment Capture** in one interaction event.
3. **Real‑Time Bias‑Corrected Aggregation** of poll results.
4. **Integrated Crypto Rewards & Governance** tied to feedback quality.
5. **Dual‑Layer Feedback UI** with live token balance display.
6. **Tipping Flow** embedded directly in poll results screens.

---

## 5. Intended Protections
- **Utility Patents** – For technical methods and systems.
- **Design Patents** – For unique UI layouts, iconography, and animations.
- **Trademarks** – For “ThumbsUp” name, logo, and Thumbs Token symbol.
- **Copyright** – For source code, UI artwork, and documentation.
- **Trade Secrets** – For proprietary algorithms and engagement heuristics.

---

## 6. Licensing & Contributions
- All contributions to this repository are subject to the project’s LICENSE file.
- Contributors agree that any submitted code, designs, or concepts may be incorporated into ThumbsUp.app and associated IP filings.

---

## 7. Disclaimer
This disclosure does not waive any intellectual property rights.  
It is published to establish prior art and to timestamp the invention’s scope as of the date above.

---

© 2025. All rights reserved.

thumbsup/
├── thumbs-contracts/
│   ├── contracts/ThumbsToken.sol
│   ├── scripts/deploy.ts
│   ├── hardhat.config.ts
│   ├── package.json
│   ├── tsconfig.json
│   ├── .env.example
│   └── README.md
├── thumbs-backend/
│   ├── prisma/schema.prisma
│   ├── src/main.ts
│   ├── src/app.module.ts
│   ├── src/prisma.service.ts
│   ├── src/wallet/wallet.controller.ts
│   ├── src/wallet/wallet.service.ts
│   ├── src/incentives/incentives.service.ts
│   ├── src/campaigns/campaigns.module.ts
│   ├── src/incentives/incentives.module.ts
│   ├── src/wallet/wallet.module.ts
│   ├── package.json
│   ├── tsconfig.json
│   ├── .env.example
│   └── README.md
├── thumbs-web/
│   ├── app/providers.tsx
│   ├── app/wallet/page.tsx
│   ├── pages/api/wallet/balance.ts
│   ├── pages/api/wallet/transactions.ts
│   ├── next.config.js
│   ├── package.json
│   ├── tsconfig.json
│   ├── .env.example
│   └── README.md
├── thumbs-mobile/
│   ├── App.tsx
│   ├── app/WalletScreen.tsx
│   ├── package.json
│   ├── tsconfig.json
│   ├── app.json
│   ├── .env.example
│   └── README.md
├── .gitignore
├── docker-compose.yml
└── README.md

{
  "name": "thumbs-contracts",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "compile": "hardhat compile",
    "test": "hardhat test",
    "deploy:sepolia": "hardhat run scripts/deploy.ts --network sepolia"
  },
  "devDependencies": {
    "@nomicfoundation/hardhat-toolbox": "^5.0.0",
    "dotenv": "^16.4.5",
    "hardhat": "^2.22.5",
    "typescript": "^5.4.5"
  },
  "dependencies": {
    "@openzeppelin/contracts": "^5.0.2"
  }
}
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "resolveJsonModule": true,
    "outDir": "dist",
    "types": ["hardhat"]
  },
  "include": ["./scripts", "./test", "./typechain-types", "./hardhat.config.ts"]
}
ALCHEMY_RPC=https://eth-sepolia.g.alchemy.com/v2/replace_me
DEPLOYER_PK=0xreplace_me_private_key
TREASURY_ADDR=0xReplaceTreasury
ADMIN_ADDR=0xReplaceAdmin
ETHERSCAN_KEY=replace_me
import { config as dot } from "dotenv";
dot();
import { HardhatUserConfig } from "hardhat/config";
import "@nomicfoundation/hardhat-toolbox";

const config: HardhatUserConfig = {
  solidity: "0.8.24",
  networks: {
    sepolia: {
      url: process.env.ALCHEMY_RPC || "",
      accounts: process.env.DEPLOYER_PK ? [process.env.DEPLOYER_PK] : []
    }
  },
  etherscan: { apiKey: process.env.ETHERSCAN_KEY || "" }
};

export default config;
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.24;

import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Permit.sol";
import "@openzeppelin/contracts/token/ERC20/extensions/ERC20Pausable.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";

contract ThumbsToken is ERC20Permit, ERC20Pausable, AccessControl {
    bytes32 public constant PAUSER_ROLE = keccak256("PAUSER_ROLE");
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");

    uint256 public immutable MAX_SUPPLY;
    address public immutable treasury;

    event IncentiveMint(address indexed to, uint256 amount, bytes32 indexed reason);
    event TreasuryFunded(address indexed treasury, uint256 amount);

    constructor(
        string memory name_,
        string memory symbol_,
        uint256 maxSupply_,
        address treasury_,
        address admin_
    ) ERC20(name_, symbol_) ERC20Permit(name_) {
        require(treasury_ != address(0) && admin_ != address(0), "bad addr");
        _grantRole(DEFAULT_ADMIN_ROLE, admin_);
        _grantRole(PAUSER_ROLE, admin_);
        _grantRole(MINTER_ROLE, admin_);
        MAX_SUPPLY = maxSupply_;
        treasury = treasury_;
    }

    function pause() external onlyRole(PAUSER_ROLE) { _pause(); }
    function unpause() external onlyRole(PAUSER_ROLE) { _unpause(); }

    function mint(address to, uint256 amount, bytes32 reason) external onlyRole(MINTER_ROLE) {
        require(totalSupply() + amount <= MAX_SUPPLY, "cap");
        _mint(to, amount);
        emit IncentiveMint(to, amount, reason);
    }

    function fundTreasury(uint256 amount) external onlyRole(MINTER_ROLE) {
        require(totalSupply() + amount <= MAX_SUPPLY, "cap");
        _mint(treasury, amount);
        emit TreasuryFunded(treasury, amount);
    }

    function _update(address from, address to, uint256 value)
        internal
        override(ERC20, ERC20Pausable)
    {
        super._update(from, to, value);
    }
}
import { ethers } from "hardhat";

async function main() {
  const [deployer] = await ethers.getSigners();
  const name = "Thumbs Token";
  const symbol = "THUMBS";
  const maxSupply = ethers.parseUnits("100000000", 18); // 100M
  const treasury = process.env.TREASURY_ADDR!;
  const admin = process.env.ADMIN_ADDR || deployer.address;

  const Token = await ethers.getContractFactory("ThumbsToken");
  const token = await Token.deploy(name, symbol, maxSupply, treasury, admin);
  await token.waitForDeployment();

  console.log("ThumbsToken deployed to:", await token.getAddress());
  console.log("Admin:", admin);
  console.log("Treasury:", treasury);
}

main().catch((e) => { console.error(e); process.exit(1); });
# Thumbs Contracts

- Copy .env.example to .env and fill values.
- Compile: `npm run compile`
- Deploy to Sepolia: `npm run deploy:sepolia`
