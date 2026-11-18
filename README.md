# BlockFarm — Blockchain Supply-Chain Tracking Prototype

A Solidity-based learning project exploring how agricultural supply-chain steps can be recorded and traced using Ethereum-compatible smart contracts.

**What the code models:** The contracts currently use a **coffee supply chain**, including cultivation, farm inspection, harvesting, export, import, and processing. This is a prototype, **not an audited or production-ready application**.

## What this project demonstrates

- **Role-aware workflow:** Contract functions verify a caller's role and the next permitted action for each batch.
- **Batch traceability:** Information about a batch is stored and retrieved throughout its lifecycle.
- **Events:** The core contract emits events for the different supply-chain stages.
- **Contract composition:** Separate contracts manage supply-chain logic, storage, and users.
- **Frontend exploration:** The repository includes HTML/CSS prototype pages.

## Tech stack

Solidity 0.4.23 (as configured in Truffle), Ethereum-compatible development networks, Truffle, Ganache-style local JSON-RPC, HTML, and CSS.

## Repository map

| Path | Purpose |
| --- | --- |
| `contracts/CoffeeSupplyChain.sol` | Stage transitions, checks, and events |
| `contracts/SupplyChainStorage.sol` | Storage for users and batches |
| `contracts/SupplyChainUser.sol` | User and role operations |
| `contracts/Ownable.sol` | Ownership-related access |
| `migrations/1_deploy.js` | Contract migration script |
| `test/` | Existing Truffle test stubs and cases |
| `index.html`, `style.css`, `order.css` | Frontend prototype |

## Supply-chain flow

~~~mermaid
flowchart LR
  A[Register batch] --> B[Farm inspection]
  B --> C[Harvesting]
  C --> D[Export]
  D --> E[Import]
  E --> F[Processing]
~~~

See `CoffeeSupplyChain.sol` for the actual role checks, recorded attributes, and emitted events.

## Running locally

You will need Node.js/npm, a Truffle CLI compatible with Solidity **0.4.23**, and a local Ethereum-compatible RPC endpoint.

1. Clone the project: `git clone https://github.com/Rizwankhan0001/Blockfarm.git`
2. Start your development blockchain on `127.0.0.1:8545` (as configured under the `development` network).
3. Run `truffle compile`.
4. Run `truffle test` to execute the existing test scripts.

### Known deployment limitation

The current `migrations/1_deploy.js` references a **hard-coded address for SupplyChainStorage** and has the initial storage deployment commented out. To deploy against a new local network, first deploy `SupplyChainStorage`, then use that newly deployed address for `SupplyChainUser` and `CoffeeSupplyChain`. The existing migration should **not** be assumed to work unchanged on a fresh chain.

The tests are limited and have not been rerun as part of this documentation update.

## Roadmap

- Make migrations deploy all required contracts in the correct order.
- Expand tests for permissions, invalid transitions, and a complete batch lifecycle.
- Document frontend-to-contract interactions with verified screenshots.
- Upgrade the old Solidity/tooling stack only after confirming compatibility.

> **Security:** Do not put real assets, sensitive information, or production supply-chain records into this unaudited prototype.
