# XY Store — Multi-Store Retail Management System

A Rust backend for managing retail operations across multiple stores under a
single business: inventory, sales, stock transfers, customers, and expenses.

> **Status:** early scaffolding. Domain models are drafted; the HTTP layer
> (controllers, routes, services, middlewares) is not yet implemented.

## Project structure

```
.
├── src/
│   ├── main.rs          # entry point
│   ├── models/          # domain data structures
│   ├── controllers/     # request handlers (planned)
│   ├── routes/          # route definitions (planned)
│   ├── services/        # business logic (planned)
│   ├── middlewares/     # request/response middleware (planned)
│   ├── errors/          # error types (planned)
│   └── utils/           # shared helpers (planned)
├── docs/                 # requirements and design documents
├── Cargo.toml
└── Cargo.lock
```

## Domain models

Defined under `src/models/`:

- **Business / Store** — a business with one or more stores, each with a
  status (`Active` / `Inactive`).
- **User / StoreEmployee** — users assigned to a store with a role
  (`Manager`, `Cashier`, `InventoryOfficer`).
- **Product** — catalog items belonging to a business (SKU, price).
- **Inventory** — per-store stock levels and reorder thresholds for a product.
- **StockTransfer** — movement of stock between stores, with a status
  (`Pending`, `Approved`, `Rejected`, `Completed`, `Cancelled`).
- **Customer** — customers attached to a business.
- **Sale / SaleItem** — point-of-sale transactions and their line items.
- **Expense** — store expenses categorized (`Rent`, `Salary`,
  `Electricity`, etc.).

## Getting started

Requires a recent [Rust toolchain](https://www.rust-lang.org/tools/install).

```bash
cargo build
cargo run
```

## Development workflow

1. Create a branch from `main` (`feat/fr-11-stock-movements`, `fix/...`).
2. Before pushing, run the same checks as CI:

   ```bash
   # backend
   cargo fmt --all && cargo clippy --all-targets -- -D warnings && cargo test

   # frontend
   cd frontend && pnpm lint && pnpm typecheck && pnpm build
   ```

3. Open a pull request. The template asks which SRS requirement IDs it covers
   (FR-xx / NFR-xx) and how they were tested (SRS Part C).
4. CI must pass before merging:
   - **Backend CI** (`.github/workflows/backend.yml`): fmt, clippy, tests,
     release build, `cargo audit` (also runs weekly).
   - **Frontend CI** (`.github/workflows/frontend.yml`): lint, typecheck,
     build, `pnpm audit`.
   - **No AI attribution** (`.github/workflows/attribution.yml`): fails if any
     commit or the PR description contains AI co-author or "Generated with"
     lines (e.g. `Co-Authored-By: Claude`). Run it locally with
     `.github/scripts/check-attribution.sh origin/main..HEAD`.
5. Dependabot opens weekly dependency update PRs.

## Documentation

See [`docs/multi_store_retail_management_system_requirements.docx`](docs/multi_store_retail_management_system_requirements.docx)
for the full requirements specification.
