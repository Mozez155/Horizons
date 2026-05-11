# Horizons

Horizons is a decentralized crypto news aggregator and portfolio management platform built on the Stellar blockchain. It combines real-time news curation with sentiment analysis, seamless portfolio tracking via Stellar wallet integration, and on-chain incentives powered by Soroban smart contracts — giving users transparent, borderless access to crypto insights.

Built for crypto enthusiasts, traders, and developers, Horizons makes it easier to stay informed and manage assets in fast-moving markets. Whether you're tracking trends or analyzing on-chain data, the platform's clean UI, robust API, and deep blockchain integration are designed to support confident decision-making.

---

## What it does

- Aggregates crypto news from multiple sources with real-time sentiment analysis
- Tracks portfolio performance with Stellar wallet integration (Freighter / Lobstr)
- Rewards community contributions through Soroban smart contracts
- Exposes a RESTful API for data queries and third-party integrations
- Runs automated data pipelines for market trend analysis and news ingestion

---

## Repository structure

```
horizons/
├── backend/              # NestJS REST API
├── frontend/
│   ├── webapp/           # Next.js web app
│   └── mobile/           # Expo React Native app
├── contracts/            # Soroban smart contracts (Rust)
└── data-processing/      # Python data pipeline
```

---

## Tech stack

**Frontend**
- Next.js 15 with App Router
- React 18 + TypeScript
- Tailwind CSS
- Stellar SDK for wallet interactions
- Recharts for portfolio visualization

**Backend**
- NestJS 11 (Node.js + TypeScript)
- PostgreSQL with TypeORM
- Redis for caching and rate limiting
- BullMQ for async job queues
- JWT + Stellar SEP-10 authentication
- Prometheus metrics

**Data Processing**
- Python 3.9+
- News ingestion, sentiment analysis, and market trend detection
- Stellar on-chain data fetching

**Blockchain**
- Stellar network (testnet / mainnet)
- Soroban smart contracts in Rust
- Contracts: contributor registry, crowdfund vault, grants matching pool, project registry, vesting wallet, treasury, curation

---

## Prerequisites

- Node.js 18+ — [nodejs.org](https://nodejs.org)
- pnpm — `npm install -g pnpm`
- Python 3.9+ — [python.org](https://python.org)
- Rust 1.75+ with WASM target — [rustup.rs](https://rustup.rs)
  ```
  rustup target add wasm32-unknown-unknown
  ```
- Freighter wallet (Stellar testnet) — [freighter.app](https://freighter.app)

---

## Getting started

**1. Clone**
```bash
git clone https://github.com/Pulsefy/Horizons.git
cd Horizons
```

**2. Install dependencies**
```bash
# JS/TS
pnpm install

# Rust contracts
cd contracts && cargo build --target wasm32-unknown-unknown --release && cd ..

# Python
cd data-processing && pip install -r requirements.txt && cd ..
```

**3. Environment**

Copy the example env files and fill in your values:
```bash
cp backend/.env.example backend/.env
cp frontend/webapp/.env.local.example frontend/webapp/.env.local
cp frontend/mobile/.env.example frontend/mobile/.env
cp data-processing/.env.example data-processing/.env
```

Key variables:
```
NODE_ENV=development
PORT=3000
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=your_db_user
DB_PASSWORD=your_db_pass
DB_DATABASE=horizons
STELLAR_NETWORK=testnet
STELLAR_SERVER_SECRET=your_stellar_secret
SOROBAN_RPC_URL=http://localhost:8000/soroban/rpc
JWT_SECRET=your_jwt_secret
REDIS_HOST=localhost
REDIS_PORT=6379
```

**4. Database**

Set up PostgreSQL and run migrations:
```bash
cd backend
npm run migration:run
```

Fund your testnet wallet at [laboratory.stellar.org](https://laboratory.stellar.org).

**5. Run locally**

Start each service in a separate terminal:
```bash
# Backend
cd backend && npm run start:dev

# Web app
cd frontend/webapp && npm run dev

# Mobile
cd frontend/mobile && npx expo start

# Data processing
cd data-processing && python src/main.py
```

Services:
- Web app: http://localhost:3000
- Backend API: http://localhost:3001
- Data processing: runs as a background pipeline

**6. Deploy contracts**
```bash
cd contracts
soroban contract deploy --wasm target/wasm32-unknown-unknown/release/horizons.wasm --network testnet
```

---

## Running tests

```bash
# Backend (Jest)
cd backend && npm run test

# Web app (Vitest)
cd frontend/webapp && npm run test

# Contracts (Rust)
cd contracts && cargo test

# Data processing (pytest)
cd data-processing && pytest
```

---

## Deployment

- **Web app** — Vercel (connect repo, add env vars)
- **Backend / Data processing** — Railway or AWS (Docker recommended for Python)
- **Contracts** — GitHub Actions CI/CD, verify on Stellar explorer
- Set `STELLAR_NETWORK=mainnet` for production and audit contracts before deploying

---

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

Quick start:
1. Fork and branch: `git checkout -b feat/your-feature`
2. Write code, add tests, run lint
3. Commit with a clear message: `feat: add news sentiment filter`
4. Open a PR to `main`

---

## Migration notes

Horizons runs on Stellar/Soroban. For details on architecture decisions, completed migrations, and legacy cleanup see [document/STELLAR_MIGRATION_NOTES.md](document/STELLAR_MIGRATION_NOTES.md).

For local setup details including wallet configuration, seeded data, and service startup order see [document/LOCAL_SETUP.md](document/LOCAL_SETUP.md).

---

## License

MIT — see [LICENSE](LICENSE).

## Community

- Discord: [discord.gg/gBmApTNVV](https://discord.gg/gBmApTNVV)
- Issues: open one on GitHub
- Built by the Horizons team. Powered by Stellar.
