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
{
  "name": "thumbs-backend",
  "version": "1.0.0",
  "private": true,
  "scripts": {
    "start": "nest start",
    "start:dev": "nest start --watch",
    "build": "nest build",
    "test": "jest",
    "prisma:generate": "prisma generate",
    "prisma:migrate": "prisma migrate dev --name init"
  },
  "dependencies": {
    "@nestjs/common": "^10.3.2",
    "@nestjs/core": "^10.3.2",
    "@nestjs/platform-express": "^10.3.2",
    "@prisma/client": "^5.16.2",
    "class-transformer": "^0.5.1",
    "class-validator": "^0.14.1",
    "dotenv": "^16.4.5",
    "ethers": "^6.12.1",
    "reflect-metadata": "^0.1.13",
    "rxjs": "^7.8.1"
  },
  "devDependencies": {
    "@nestjs/cli": "^10.3.2",
    "@nestjs/schematics": "^10.1.3",
    "@nestjs/testing": "^10.3.2",
    "@types/node": "^20.12.12",
    "jest": "^29.7.0",
    "prisma": "^5.16.2",
    "ts-jest": "^29.1.2",
    "ts-node": "^10.9.2",
    "typescript": "^5.4.5"
  }
}
{
  "compilerOptions": {
    "module": "commonjs",
    "declaration": false,
    "removeComments": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "allowSyntheticDefaultImports": true,
    "target": "es2017",
    "sourceMap": true,
    "outDir": "./dist",
    "baseUrl": "./",
    "incremental": true
  }
}
DATABASE_URL=postgresql://thumbs:thumbs@localhost:5432/thumbs
RPC_URL=https://eth-sepolia.g.alchemy.com/v2/replace_me
TOKEN_ADDRESS=0xReplaceWithDeployedToken
MINTER_PK=0xreplace_me_private_key
TREASURY_ADDRESS=0xReplaceTreasury
PORT=4000
datasource db { provider = "postgresql"; url = env("DATABASE_URL") }
generator client { provider = "prisma-client-js" }

model User {
  id           String   @id @default(cuid())
  email        String   @unique
  handle       String   @unique
  passwordHash String
  wallet       Wallet?
  createdAt    DateTime @default(now())
  updatedAt    DateTime @updatedAt
}

model Wallet {
  id        String   @id @default(cuid())
  userId    String   @unique
  address   String   @unique
  chain     String
  onchain   Boolean  @default(false)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  user      User     @relation(fields: [userId], references: [id])
}

model Transaction {
  id          String   @id @default(cuid())
  userId      String
  type        String   // CREDIT|DEBIT|INCENTIVE|PAYOUT
  amount      BigInt
  tokenSymbol String?
  ref         String?
  meta        Json?
  createdAt   DateTime @default(now())
  user        User     @relation(fields: [userId], references: [id])
}

model IncentiveRule {
  id       String   @id @default(cuid())
  actor    String   // CREATOR|PARTNER|COMMUNITY
  action   String   // PUBLISH|MILESTONE|REFERRAL|CHALLENGE_WIN
  amount   Int      // in whole tokens; service converts to wei
  enabled  Boolean  @default(true)
  meta     Json?
  createdAt DateTime @default(now())
}
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as dotenv from 'dotenv';

async function bootstrap() {
  dotenv.config();
  const app = await NestFactory.create(AppModule);
  app.enableCors({ origin: true, credentials: true });
  const port = process.env.PORT ? Number(process.env.PORT) : 4000;
  await app.listen(port);
  // eslint-disable-next-line no-console
  console.log(`Backend listening on http://localhost:${port}`);
}
bootstrap();
import { Module } from '@nestjs/common';
import { PrismaService } from './prisma.service';
import { WalletModule } from './wallet/wallet.module';
import { IncentivesModule } from './incentives/incentives.module';
import { CampaignsModule } from './campaigns/campaigns.module';

@Module({
  imports: [WalletModule, IncentivesModule, CampaignsModule],
  providers: [PrismaService],
})
export class AppModule {}
import { INestApplication, Injectable, OnModuleInit } from '@nestjs/common';
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService extends PrismaClient implements OnModuleInit {
  async onModuleInit() { await this.$connect(); }
  async enableShutdownHooks(app: INestApplication) {
    this.$on('beforeExit', async () => { await app.close(); });
  }
}
import { Module } from '@nestjs/common';
import { WalletService } from './wallet.service';
import { WalletController } from './wallet.controller';
import { PrismaService } from '../prisma.service';

@Module({
  controllers: [WalletController],
  providers: [WalletService, PrismaService]
})
export class WalletModule {}
import { Controller, Get, Post, Body, Query } from '@nestjs/common';
import { WalletService } from './wallet.service';

@Controller('wallet')
export class WalletController {
  constructor(private readonly svc: WalletService) {}

  @Get('balance')
  async balance(@Query('userId') userId: string) {
    return this.svc.getBalance(userId);
  }

  @Get('transactions')
  async tx(@Query('userId') userId: string) {
    return this.svc.getTransactions(userId);
  }

  @Post('withdraw')
  async withdraw(@Body() dto: { userId: string; amountWei: string; address: string }) {
    return this.svc.requestWithdraw(dto.userId, dto.amountWei, dto.address);
  }
}
import { Injectable } from '@nestjs/common';
import { PrismaService } from '../prisma.service';

@Injectable()
export class WalletService {
  constructor(private prisma: PrismaService) {}

  async getBalance(userId: string) {
    const credits = await this.prisma.transaction.aggregate({
      where: { userId, type: { in: ['CREDIT','INCENTIVE'] } },
      _sum: { amount: true },
    });
    const debits = await this.prisma.transaction.aggregate({
      where: { userId, type: { in: ['DEBIT','PAYOUT'] } },
      _sum: { amount: true },
    });
    const available = (credits._sum.amount ?? BigInt(0)) - (debits._sum.amount ?? BigInt(0));
    return { userId, available: available.toString() };
  }

  async getTransactions(userId: string) {
    return this.prisma.transaction.findMany({
      where: { userId }, orderBy: { createdAt: 'desc' }, take: 100
    });
  }

  async requestWithdraw(userId: string, amountWei: string, toAddress: string) {
    const tx = await this.prisma.transaction.create({
      data: {
        userId, type: 'PAYOUT', amount: BigInt(amountWei),
        meta: { to: toAddress, status: 'REQUESTED' }
      }
    });
    return { requestId: tx.id, status: 'REQUESTED' };
  }
}
import { Module } from '@nestjs/common';
import { IncentivesService } from './incentives.service';
import { PrismaService } from '../prisma.service';

@Module({
  providers: [IncentivesService, PrismaService],
  exports: [IncentivesService]
})
export class IncentivesModule {}
import { Injectable } from '@nestjs/common';
import { PrismaService } from '../prisma.service';
import * as dotenv from 'dotenv';
import { ethers } from 'ethers';

// Minimal ABI for ThumbsToken.mint(address,uint256,bytes32)
const TOKEN_ABI = [
  "function mint(address to, uint256 amount, bytes32 reason) external",
];

dotenv.config();

@Injectable()
export class IncentivesService {
  private provider = new ethers.JsonRpcProvider(process.env.RPC_URL!);
  private wallet = new ethers.Wallet(process.env.MINTER_PK!, this.provider);
  private token = new ethers.Contract(process.env.TOKEN_ADDRESS!, TOKEN_ABI, this.wallet);

  constructor(private prisma: PrismaService) {}

  async reward(userId: string, action: string, meta?: any) {
    const rule = await this.prisma.incentiveRule.findFirst({ where: { action, enabled: true }});
    if (!rule) return { ok: false, reason: 'no-rule' };

    const wallet = await this.prisma.wallet.findUnique({ where: { userId }});
    if (!wallet?.address) return { ok: false, reason: 'no-address' };

    const amount = BigInt(rule.amount) * 10n ** 18n;
    const reason = ethers.id(action);

    const tx = await this.token.mint(wallet.address, amount, reason);
    await tx.wait(1);

    await this.prisma.transaction.create({
      data: {
        userId, type: 'INCENTIVE', amount,
        ref: action, meta: { ruleId: rule.id, txHash: tx.hash, ...meta }
      }
    });

    return { ok: true, txHash: tx.hash, amount: amount.toString() };
  }
}
import { Module } from '@nestjs/common';

@Module({})
export class CampaignsModule {}
# Thumbs Backend (NestJS + Prisma)

- Copy `.env.example` to `.env`
- Install: `npm install`
- Prisma: `npx prisma generate && npx prisma migrate dev --name init`
- Run: `npm run start:dev`
{
  "name": "thumbs-web",
  "private": true,
  "version": "1.0.0",
  "scripts": {
    "dev": "next dev -p 3000",
    "build": "next build",
    "start": "next start -p 3000"
  },
  "dependencies": {
    "@rainbow-me/rainbowkit": "^2.1.3",
    "axios": "^1.7.2",
    "next": "^14.2.4",
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "recharts": "^2.10.4",
    "viem": "^2.9.1",
    "wagmi": "^2.9.8"
  }
}
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": false,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "incremental": true,
    "baseUrl": "."
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
BACKEND_URL=http://localhost:4000
WALLETCONNECT_PROJECT_ID=replace_me
/** @type {import('next').NextConfig} */
const nextConfig = { reactStrictMode: true };
module.exports = nextConfig;
"use client";
import { WagmiConfig, configureChains, createConfig } from "wagmi";
import { mainnet, sepolia } from "wagmi/chains";
import { http } from "viem";
import { RainbowKitProvider, getDefaultWallets } from "@rainbow-me/rainbowkit";
import "@rainbow-me/rainbowkit/styles.css";

const { chains, publicClient } = configureChains(
  [sepolia, mainnet],
  [http()]
);
const { connectors } = getDefaultWallets({
  appName: "ThumbsUp",
  projectId: process.env.NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID || "demo",
  chains
});
const config = createConfig({ autoConnect: true, connectors, publicClient });

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <WagmiConfig config={config}>
      <RainbowKitProvider chains={chains}>{children}</RainbowKitProvider>
    </WagmiConfig>
  );
}
"use client";
import React, { useEffect, useState } from "react";
import axios from "axios";
import { PieChart, Pie, Cell, ResponsiveContainer } from "recharts";
import { Providers } from "../providers";
import { ConnectButton } from "@rainbow-me/rainbowkit";

const COLORS = ["#FF8A00", "#FFB347", "#FFD9A0"];

export default function WalletPage() {
  const [balance, setBalance] = useState("0");
  const [txs, setTxs] = useState<any[]>([]);
  const [breakdown, setBreakdown] = useState<any[]>([]);
  const userId = "demo-user"; // replace with real auth linkage

  useEffect(() => {
    (async () => {
      const b = await axios.get(`/api/wallet/balance`, { params: { userId } });
      const t = await axios.get(`/api/wallet/transactions`, { params: { userId } });
      setBalance(b.data.available);
      setTxs(t.data);

      const credits = t.data.filter((r: any) => ["CREDIT","INCENTIVE"].includes(r.type));
      const map: Record<string, number> = {};
      credits.forEach((r: any) => {
        const k = r.type === "INCENTIVE" ? (r.ref || "INCENTIVE") : r.type;
        map[k] = (map[k] || 0) + 1;
      });
      const arr = Object.entries(map).map(([name, value]) => ({ name, value }));
      setBreakdown(arr.length ? arr : [{ name: "INCENTIVE", value: 1 }]);
    })();
  }, []);

  return (
    <Providers>
      <div style={{ padding: 24 }}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center" }}>
          <h1>Wallet</h1>
          <ConnectButton />
        </div>

        <div style={{ background: "linear-gradient(90deg,#FF8A00,#FFB347)", color: "#fff", borderRadius: 16, padding: 20, marginTop: 16 }}>
          <div style={{ fontSize: 14, opacity: 0.9 }}>Available Balance</div>
          <div style={{ fontSize: 36, fontWeight: 800 }}>{Number(balance)/1e18} THUMBS</div>
          <div style={{ fontSize: 12, opacity: 0.8 }}>Pending: —</div>
        </div>

        <div style={{ display: "flex", gap: 24, marginTop: 24 }}>
          <div style={{ flex: 1, background: "#FFF6EB", borderRadius: 16, padding: 16 }}>
            <h3>Earnings breakdown</h3>
            <div style={{ height: 200 }}>
              <ResponsiveContainer>
                <PieChart>
                  <Pie data={breakdown} dataKey="value" outerRadius={80} label>
                    {breakdown.map((_, i) => <Cell key={i} fill={COLORS[i % COLORS.length]} />)}
                  </Pie>
                </PieChart>
              </ResponsiveContainer>
            </div>
          </div>

          <div style={{ flex: 2, background: "#FFF6EB", borderRadius: 16, padding: 16 }}>
            <h3>Recent transactions</h3>
            <ul style={{ listStyle: "none", padding: 0, margin: 0 }}>
              {txs.map((t) => (
                <li key={t.id} style={{ display: "flex", justifyContent: "space-between", padding: "12px 0", borderBottom: "1px solid #FFE1C2" }}>
                  <span>{t.type}{t.ref ? ` • ${t.ref}` : ""}</span>
                  <span style={{ color: ["CREDIT","INCENTIVE"].includes(t.type) ? "#0B8F34" : "#B00020" }}>
                    {["CREDIT","INCENTIVE"].includes(t.type) ? "+" : "-"}{Number(t.amount)/1e18} THUMBS
                  </span>
                </li>
              ))}
            </ul>
          </div>
        </div>
      </div>
    </Providers>
  );
}
import type { NextApiRequest, NextApiResponse } from "next";
import axios from "axios";

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const backend = process.env.BACKEND_URL || "http://localhost:4000";
  const r = await axios.get(`${backend}/wallet/balance`, { params: { userId: req.query.userId } });
  res.status(200).json(r.data);
}
import type { NextApiRequest, NextApiResponse } from "next";
import axios from "axios";

export default async function handler(req: NextApiRequest, res: NextApiResponse) {
  const backend = process.env.BACKEND_URL || "http://localhost:4000";
  const r = await axios.get(`${backend}/wallet/transactions`, { params: { userId: req.query.userId } });
  res.status(200).json(r.data);
}
# Thumbs Web (Next.js)

- Copy `.env.example` to `.env.local` or `.env`
- Install: `npm install`
- Run: `npm run dev`
{
  "name": "thumbs-mobile",
  "version": "1.0.0",
  "private": true,
  "main": "App.tsx",
  "scripts": {
    "start": "expo start",
    "android": "expo run:android",
    "ios": "expo run:ios"
  },
  "dependencies": {
    "axios": "^1.7.2",
    "expo": "^51.0.10",
    "expo-status-bar": "~1.12.1",
    "react": "18.2.0",
    "react-native": "0.74.1"
  },
  "devDependencies": {
    "typescript": "^5.4.5"
  }
}
{
  "expo": {
    "name": "ThumbsUp",
    "slug": "thumbsup",
    "scheme": "thumbsup",
    "version": "1.0.0",
    "orientation": "portrait",
    "sdkVersion": "51.0.0"
  }
}
{
  "compilerOptions": {
    "target": "ES2020",
    "jsx": "react",
    "moduleResolution": "node",
    "strict": true,
    "allowJs": true,
    "esModuleInterop": true,
    "noEmit": true,
    "skipLibCheck": true
  }
}
EXPO_PUBLIC_API=http://localhost:4000
import React from "react";
import { SafeAreaView } from "react-native";
import WalletScreen from "./app/WalletScreen";

export default function App() {
  return (
    <SafeAreaView style={{ flex: 1 }}>
      <WalletScreen />
    </SafeAreaView>
  );
}
import React, { useEffect, useState } from "react";
import { View, Text, FlatList, TouchableOpacity } from "react-native";
import axios from "axios";

export default function WalletScreen() {
  const [balance, setBalance] = useState("0");
  const [txs, setTxs] = useState<any[]>([]);
  const userId = "demo-user";

  useEffect(() => {
    (async () => {
      const base = process.env.EXPO_PUBLIC_API || "http://localhost:4000";
      const b = await axios.get(`${base}/wallet/balance`, { params: { userId } });
      const t = await axios.get(`${base}/wallet/transactions`, { params: { userId } });
      setBalance(b.data.available);
      setTxs(t.data);
    })();
  }, []);

  return (
    <View style={{ flex: 1, padding: 16, backgroundColor: "#FFF" }}>
      <View style={{ backgroundColor: "#FF9A2F", borderRadius: 16, padding: 16 }}>
        <Text style={{ color: "#fff", opacity: 0.9 }}>Available Balance</Text>
        <Text style={{ color: "#fff", fontSize: 36, fontWeight: "800" }}>{Number(balance)/1e18} THUMBS</Text>
        <Text style={{ color: "#fff", opacity: 0.8 }}>Pending —</Text>
      </View>

      <View style={{ marginTop: 16, backgroundColor: "#FFF6EB", borderRadius: 16, padding: 16, flex: 1 }}>
        <Text style={{ fontWeight: "700", marginBottom: 8 }}>Recent transactions</Text>
        <FlatList
          data={txs}
          keyExtractor={(item) => item.id}
          renderItem={({ item }) => (
            <View style={{ flexDirection: "row", justifyContent: "space-between", paddingVertical: 8, borderBottomColor: "#FFE1C2", borderBottomWidth: 1 }}>
              <Text>{item.type}{item.ref ? ` • ${item.ref}` : ""}</Text>
              <Text style={{ color: ["CREDIT","INCENTIVE"].includes(item.type) ? "#0B8F34" : "#B00020" }}>
                {["CREDIT","INCENTIVE"].includes(item.type) ? "+" : "-"}{Number(item.amount)/1e18} THUMBS
              </Text>
            </View>
          )}
        />
      </View>

      <View style={{ flexDirection: "row", gap: 8, marginTop: 12 }}>
        <TouchableOpacity style={{ backgroundColor: "#FF8A00", padding: 12, borderRadius: 12 }}>
          <Text style={{ color: "#fff" }}>Withdraw</Text>
        </TouchableOpacity>
        <TouchableOpacity style={{ borderColor: "#FF8A00", borderWidth: 2, padding: 12, borderRadius: 12 }}>
          <Text style={{ color: "#FF8A00" }}>Transfer</Text>
        </TouchableOpacity>
      </View>
    </View>
  );
}
# Thumbs Mobile (Expo)

- Copy `.env.example` to `.env`
- Install: `npm install`
- Run: `npm start`
# dependencies
node_modules
# environment
.env
.env.*
# build
dist
.build
.cache
coverage
# os
.DS_Store
# next
.next
out
# expo
.expo
.expo-shared
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_USER: thumbs
      POSTGRES_PASSWORD: thumbs
      POSTGRES_DB: thumbs
    ports: ["5432:5432"]
    volumes: ["pg:/var/lib/postgresql/data"]

  backend:
    build: ./thumbs-backend
    working_dir: /app
    command: npm run start:dev
    environment:
      DATABASE_URL: postgresql://thumbs:thumbs@db:5432/thumbs
      RPC_URL: ${RPC_URL:-https://eth-sepolia.g.alchemy.com/v2/replace_me}
      TOKEN_ADDRESS: ${TOKEN_ADDRESS:-0x0000000000000000000000000000000000000000}
      MINTER_PK: ${MINTER_PK:-0x0000000000000000000000000000000000000000000000000000000000000001}
      TREASURY_ADDRESS: ${TREASURY_ADDRESS:-0x0000000000000000000000000000000000000000}
      PORT: 4000
    depends_on: [db]
    ports: ["4000:4000"]
    volumes:
      - ./thumbs-backend:/app

  web:
    build: ./thumbs-web
    working_dir: /app
    command: npm run dev
    environment:
      BACKEND_URL: http://backend:4000
      NEXT_PUBLIC_WALLETCONNECT_PROJECT_ID: demo
    depends_on: [backend]
    ports: ["3000:3000"]
    volumes:
      - ./thumbs-web:/app

volumes:
  pg: {}
# ThumbsUp Monorepo

- Contracts (Solidity + Hardhat)
- Backend (NestJS + Prisma)
- Web (Next.js)
- Mobile (Expo React Native)

## Quick start

1) Contracts

2) Backend

3) Web

4) Mobile
