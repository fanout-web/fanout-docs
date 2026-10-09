# Local Setup

Requirements: Node.js 20 or newer, pnpm 9, PostgreSQL 15 or newer, and a Freighter wallet configured for Stellar Testnet.

Clone the application repository and prepare its environment:

```bash
pnpm install --frozen-lockfile
cp .env.example .env
pnpm build
pnpm test
pnpm dev
```

The web app uses port 3000 and the API defaults to port 4000.

## Verify the environment

Open `http://localhost:3000`, then request `http://localhost:4000/health`. The health response should report `status: ok`, `network: testnet`, and the expected database storage mode. Keep Freighter on Testnet before initiating any wallet flow.

Run the production build and test suite before opening a pull request:

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

The repository is a pnpm workspace. Run commands from its root unless a package-specific guide explicitly says otherwise.
