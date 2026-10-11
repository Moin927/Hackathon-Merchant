# MerchantAI — AI-Powered Business Operating System

**Run your business by simply talking to it.**

MerchantAI is an AI-powered business management platform designed to help small businesses manage sales, expenses, inventory, customers, suppliers, invoices, and payments from one place. It combines traditional business management tools with natural-language AI assistance and Solana-based payment verification.

The goal is to make business management simpler, more accessible, and more transparent—especially for small merchants who rely on spreadsheets, notebooks, or disconnected applications.

> **Project status:** Hackathon MVP in development. Features and integrations should be considered complete only when implemented and tested in the current codebase.

---

## Table of Contents

- [The Problem](#the-problem)
- [Our Solution](#our-solution)
- [Key Features](#key-features)
- [How It Works](#how-it-works)
- [Technology Stack](#technology-stack)
- [System Architecture](#system-architecture)
- [Getting Started](#getting-started)
- [Environment Configuration](#environment-configuration)
- [Example Use Cases](#example-use-cases)
- [Security and Reliability](#security-and-reliability)
- [Solana Integration](#solana-integration)
- [Project Structure](#project-structure)
- [Testing](#testing)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## The Problem

Small businesses deal with many operational challenges:

- Sales, expenses, and purchases are recorded manually.
- Inventory tracking becomes difficult as the business grows.
- Customer debts and supplier payments are easy to lose track of.
- Financial reports require time-consuming calculations.
- Business owners may not have access to affordable, intelligent business software.
- Digital payments and payment verification can be disconnected from everyday business operations.

Existing tools can be expensive, fragmented, or unnecessarily complicated for smaller merchants.

## Our Solution

MerchantAI brings essential business operations into a single platform and adds a natural-language interface on top.

Instead of navigating multiple forms, a merchant can describe a business transaction in ordinary language. MerchantAI structures the request, validates it against the business's actual data, and asks for confirmation before executing financial changes.

Merchants can also ask questions about their business and receive answers grounded in database records.

The platform is designed around three principles:

1. **Simplicity:** Manage everyday operations from one interface.
2. **Reliable AI:** Use AI to understand requests, not to invent financial facts.
3. **Verifiable payments:** Use Solana to support transparent, independently verifiable payment records.

## Key Features

### AI-Powered Business Assistant

Ask questions about your business using natural language.

Examples:

- "How much did I sell this month?"
- "Which products are running low?"
- "Which customers still owe me money?"
- "Compare this month's sales with last month."
- "Which products are selling the most?"

The assistant uses approved backend tools to retrieve business information. Financial figures come from database queries rather than model-generated estimates.

### Natural-Language Transaction Entry

Describe a sale, purchase, or expense instead of filling out every field manually.

Example:

> "Sold two iPhones to Ahmed for Rs. 500,000. He paid Rs. 200,000 and owes the rest."

The intended workflow:

1. Parse the request into structured data.
2. Resolve products and customers.
3. Validate prices, quantities, stock, and payment amounts.
4. Present a transaction preview.
5. Ask the merchant to confirm.
6. Record the transaction through the normal backend service.
7. Update inventory, payment balances, and reports.

Ambiguous requests must be clarified rather than silently interpreted.

### Inventory Management

- Create and manage products.
- Track stock quantities.
- Record stock movements.
- Identify low-stock items.
- Maintain historical price and cost information.
- Prevent invalid stock operations.

### Sales, Purchases, and Expenses

Record business transactions and maintain consistent financial records.

- Sales and customer payments.
- Purchases and supplier payments.
- Operating expenses.
- Credit sales and outstanding balances.
- Transaction history and filtering.
- Server-side calculations and validation.

### Customer and Supplier Management

- Maintain customer and supplier records.
- Track transaction history.
- Record partial payments.
- Monitor outstanding receivables and payables.
- View customer and supplier balances.

### Financial Dashboard and Reports

Provide a consolidated view of business performance, including:

- Daily and monthly sales.
- Recorded expenses.
- Estimated gross profit.
- Inventory valuation.
- Top-selling products.
- Low-stock products.
- Outstanding customer payments.
- Outstanding supplier payments.
- Invoice status and payment history.

Financial metrics must use documented calculation rules and actual business records.

### Invoice Management

- Create and issue invoices.
- Add customers and line items.
- Calculate totals on the server.
- Track due dates and payment status.
- Record partial and complete payments.
- Associate verified blockchain payments with the relevant invoice.

### Solana-Based Payment Verification

MerchantAI is designed to support invoice payments using Solana.

The intended workflow is:

1. Generate an invoice and payment request.
2. Initiate a payment using the configured network and supported token.
3. Verify the transaction against Solana transaction data.
4. Validate the recipient, asset, amount, and transaction status.
5. Record the verified payment.
6. Update the invoice balance.

Development and hackathon demonstrations use Devnet or explicitly labelled simulated payments. Simulated transactions are not presented as real blockchain transactions.

## How It Works

### Natural-language transaction flow

```text
Merchant describes a transaction
                |
                v
        AI parses the request
                |
                v
     Structured output validation
                |
                v
     Backend checks business rules
                |
                v
       Merchant confirms details
                |
                v
       Transaction service
                |
                v
           PostgreSQL
                |
                v
  Inventory, balances and reports update
```

### Business question flow

```text
Merchant asks a question
           |
           v
    AI assistant selects
    an approved tool
           |
           v
 Backend queries business data
           |
           v
     Actual results returned
           |
           v
 AI explains the results clearly
```

### Payment verification flow

```text
Invoice created
      |
      v
Payment initiated
      |
      v
Solana transaction
      |
      v
Backend verifies transaction
      |
      v
Amount, recipient and asset checked
      |
      v
Payment recorded as verified
      |
      v
Invoice balance updated
```

## Technology Stack

The intended stack is listed below. Check the current repository and implementation status for the exact versions and components currently in use.

| Layer | Technology |
|---|---|
| Backend API | Python, FastAPI |
| Data validation | Pydantic |
| ORM | SQLAlchemy |
| Database | PostgreSQL |
| Schema migrations | Alembic |
| Authentication | JWT and secure password hashing |
| Frontend | React, TypeScript, Vite |
| Styling | Tailwind CSS |
| Data fetching | TanStack Query |
| Charts | Recharts |
| AI | Configurable LLM provider with demo mode |
| Blockchain | Solana Devnet |
| Backend testing | pytest, HTTPX |
| Development | Git, Docker Compose |

## System Architecture

MerchantAI separates business logic from AI interpretation and payment verification.

```text
                 React Frontend
                       |
                       v
                  FastAPI API
                       |
          +------------+------------+
          |            |            |
          v            v            v
     Business      AI Service    Payment Service
     Services      and Tools     Solana Adapter
          |            |            |
          v            v            v
      PostgreSQL   Validated      Solana RPC
                   DB Queries     / Network
```

**Database-first financial architecture:** The AI does not directly write to the database or independently calculate authoritative financial results. All financial changes pass through validated backend services.

## Getting Started

The following instructions describe the intended local development workflow. Exact commands may need adjustment to match the repository's current dependency files and scripts.

### Prerequisites

Install:

- Python 3.12 or a compatible version used by the project.
- Node.js and npm.
- PostgreSQL, or Docker with Docker Compose.
- Git.

Optional for live integrations:

- An API key for the configured LLM provider.
- A Solana Devnet RPC endpoint, if required.
- A compatible wallet and test funds for the configured payment flow.

### 1. Clone the Repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd merchantai
```

Replace the placeholder with your actual repository URL.

### 2. Configure Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Configure the database and application settings. Do not commit `.env` or real credentials.

### 3. Start PostgreSQL

If the repository includes a working Docker Compose configuration:

```bash
docker compose up -d
```

Otherwise, start PostgreSQL separately and configure `DATABASE_URL`.

### 4. Set Up the Backend

Open a terminal:

```bash
cd backend
python -m venv .venv
```

Activate the environment.

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies using the package manager and dependency file actually present in the repository. For example, if the project uses a `requirements.txt`:

```bash
pip install -r requirements.txt
```

If it uses `pyproject.toml` with an installable project, follow its documented installation command instead.

### 5. Apply Database Migrations

If Alembic is configured in the backend:

```bash
alembic upgrade head
```

Run this from the directory containing the relevant Alembic configuration.

### 6. Load Demo Data

If the demo seeding script has been implemented:

```bash
python ../scripts/seed_demo.py
```

Follow the README instructions or the script's help output if its location or invocation differs.

Use synthetic data for development and demonstrations.

### 7. Start the Backend

From the backend directory, for an application exposed as `app.main:app`:

```bash
uvicorn app.main:app --reload
```

Open the API documentation:

- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`
- Health check: `http://localhost:8000/health`

These URLs depend on the routes configured in the current implementation.

### 8. Start the Frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, commonly `http://localhost:5173`.

If any command differs from the actual project scripts, update this section to reflect the tested command.

## Environment Configuration

The project should provide a `.env.example` containing the supported configuration options.

Typical settings include:

```dotenv
APP_ENV=development
DEMO_MODE=true

DATABASE_URL=postgresql+psycopg://user:password@localhost:5432/merchantai

JWT_SECRET_KEY=replace-with-a-secure-random-secret
JWT_ACCESS_TOKEN_EXPIRE_MINUTES=30

CORS_ORIGINS=http://localhost:5173

AI_PROVIDER=demo
AI_API_KEY=
AI_MODEL=

SOLANA_MODE=demo
SOLANA_NETWORK=devnet
SOLANA_RPC_URL=
SOLANA_TOKEN_MINT=
SOLANA_MERCHANT_WALLET=
```

These are example configuration values, not a guarantee that every variable is currently implemented. The actual settings must match the application's configuration code.

For a live Solana payment flow, configure the actual supported token mint and recipient wallet for the selected network. Never assume a token or transaction is valid merely because an address is supplied.

## Example Use Cases

### 1. Record a Sale

**Merchant:**

"Sold two iPhones to Ahmed for Rs. 500,000."

**MerchantAI:**

- Resolves the product and customer.
- Checks inventory and pricing information.
- Displays the proposed transaction.
- Requests confirmation.
- Records the sale through the backend.

### 2. Check Outstanding Payments

**Merchant:**

"Who owes me money?"

MerchantAI retrieves outstanding customer balances and presents the results from the database.

### 3. Identify Low Stock

**Merchant:**

"Which products should I restock?"

The system checks stock quantities and thresholds and displays products requiring attention. Any demand-based recommendations should be clearly distinguished from simple low-stock rules.

### 4. Pay an Invoice

The merchant issues an invoice and shares its payment page. A supported Solana payment is verified before it is recorded as an on-chain payment. In demo mode, the interface clearly labels the simulated flow.

## Security and Reliability

MerchantAI is designed with the following requirements:

- Secure password hashing.
- JWT-protected endpoints.
- Business-level authorization and data isolation.
- Server-side validation for every financial operation.
- Atomic database transactions where consistency requires them.
- Idempotency protection for sensitive write operations.
- Database-backed financial calculations.
- Human confirmation before AI-proposed financial writes.
- Restricted AI tools with validated arguments.
- Secret management through environment variables.
- No wallet private keys in frontend code.
- Payment verification before invoice settlement.
- Audit trails for important business actions.

These are engineering requirements, not a claim that every security control has already been independently audited. Production use requires further security, accounting, and operational review.

## Solana Integration

Solana provides a verifiable payment layer for supported invoice payment flows.

MerchantAI's intended blockchain functionality is to associate a business invoice with a payment, independently verify the transaction, and reflect the verified payment in the business ledger.

The application should distinguish clearly between:

- **Demo payment:** A simulated transaction used for local development.
- **Devnet payment:** A test transaction verified on Solana Devnet.
- **Production payment:** A future capability requiring additional security, operational, compliance, and financial review.

Medical, customer, and other unnecessary personal information must not be written to the blockchain. Never treat a mock transaction as on-chain evidence.

## Project Structure

The repository is expected to organize code into separate frontend, backend, testing, and documentation areas.

```text
merchantai/
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── ai/
│   │   ├── core/
│   │   ├── db/
│   │   ├── models/
│   │   ├── payments/
│   │   ├── repositories/
│   │   ├── schemas/
│   │   └── services/
│   ├── alembic/
│   └── tests/
├── frontend/
│   └── src/
├── docs/
├── scripts/
├── .env.example
├── .gitignore
├── docker-compose.yml
└── README.md
```

The exact structure may differ as implementation evolves.

## Testing

Run the tests configured in the project.

For a pytest-based backend:

```bash
cd backend
pytest
```

For a frontend using npm scripts:

```bash
cd frontend
npm run build
```

If configured, also run:

```bash
npm run lint
```

Test critical workflows including:

- Registration, login, and authorization.
- Business data isolation.
- Product and inventory operations.
- Sales, purchases, expenses, and payments.
- Financial calculations and report accuracy.
- Invoice creation and status transitions.
- AI structured-output validation.
- Confirmation and duplicate-submission handling.
- Database-backed assistant answers.
- Solana payment verification and duplicate prevention.
- Demo mode without external API keys.

Document which tests have actually passed. Do not report unexecuted tests as successful.

## Roadmap

- [ ] Project foundation and authentication.
- [ ] Product and inventory management.
- [ ] Sales, purchases, and expense tracking.
- [ ] Customers, suppliers, and payment balances.
- [ ] Financial dashboard and reports.
- [ ] Invoice management.
- [ ] AI provider abstraction and demo mode.
- [ ] Natural-language transaction entry.
- [ ] Database-grounded AI business assistant.
- [ ] Solana Devnet payment verification.
- [ ] Complete React dashboard.
- [ ] Demo onboarding and consistent synthetic data.
- [ ] End-to-end tests and security review.
- [ ] Deployment, documentation, and hackathon demo.

Update this checklist as features are implemented and tested.

## Contributing

Contributions and feedback are welcome.

1. Fork the repository.
2. Create a feature branch.
3. Make focused changes.
4. Add or update tests.
5. Run the relevant checks.
6. Submit a pull request describing the change and its verification.

Keep credentials out of commits and never use real customer data in demo fixtures.

## License

Choose and add a license before distributing the project publicly. Until a license is included, do not assume that the repository grants permission to reuse or redistribute its code.

---

**MerchantAI — Less time managing records. More time running your business.**
