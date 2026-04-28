
# DEX_Nova_MVP

A concise reference for the DEX_Nova_MVP repository. This project pairs a Node.js/Express backend with a React frontend and includes Solidity contract sources.

Repository contents
- `src/` — backend (Express, controllers, models)
- `client/` — React frontend (CRA)
- `contract/`, `migrations/` — Solidity contracts and migration scripts
- `public/`, `data/`, `models/`, `routes/`, `middlewares/` — server assets and helpers

Quick start

1. Install dependencies (root + client):

```bash
npm install
npm install --prefix client
```

2. Create a `.env` at the project root (see Environment section below).

3. Run development servers (backend + frontend):

```bash
npm run dev
```

Useful npm scripts
- `npm run server` — start backend with `nodemon`
- `npm run client` — start React dev server (runs `client/npm start`)
- `npm run dev` — run backend and client concurrently
- `npm start` — start production server (expects built frontend and configured env)

Environment variables

The backend uses several `process.env` keys. Common values to set in `.env`:

- `PORT` (default `4000`)
- `NODE_ENV` (`development` / `production`)
- `MONGO_URI` (MongoDB connection string)
- `JWT_SECRET`, `JWT_EXPIRE`, `COOKIE_EXPIRES_TIME`
- `SENDGRID_API_KEY`, `SENDGRID_MAIL`, `SENDGRID_RESET_TEMPLATEID`, `SENDGRID_ORDER_TEMPLATEID`
- `CLOUDINARY_NAME`, `CLOUDINARY_API_KEY`, `CLOUDINARY_API_SECRET`
- Pay providers: `STRIPE_SECRET_KEY`, `PAYTM_MID`, `PAYTM_MERCHANT_KEY`, etc.
- `CLIENT_URL` — frontend origin used for CORS and email links

An example `.env` was added to the README earlier; I can also generate a full `.env.example` file containing every `process.env` key scanned from `src/`.

Client notes

- The React frontend lives in `client/`. See `client/README.md` and `client/.env.example` for frontend-specific setup. The client uses a `proxy` to forward API requests to `http://localhost:4000` in development.

Contracts

- Solidity sources are in `contract/`. Use Truffle or Hardhat to compile and deploy. Migrations are in `migrations/`.

Contributing

- Fork, branch, and open a pull request with a clear description.
- Run tests and linters before submitting changes.

License

This project is licensed under the MIT License — see [LICENSE](LICENSE).

If you'd like, I can now generate a complete top-level `.env.example` by scanning `src/` for `process.env` usages and creating a file with placeholder values.

## Project details

DEX_Nova_MVP is a minimal viable product that demonstrates a full-stack DEX/marketplace flow combining a REST API backend, a React frontend, and Solidity smart contract artifacts. It is intended as a starting point for prototyping token-enabled marketplaces and simple trading flows.

Key capabilities included in this repo:

- Product catalog and images (backend models + `data/products.json` sample data)
- Shopping cart, save-for-later, and order flows (backend controllers + frontend views)
- User authentication and authorization using JWTs
- Email notifications (SendGrid) and SMTP fallback
- File uploads with Cloudinary integration
- Payment integration scaffolding (Stripe and Paytm placeholders)
- Solidity contracts and migrations in `contract/` for on-chain features

## Technical architecture

- Backend (server): Node.js + Express. Routes are defined under `src/routes`, business logic in `src/controllers`, and data models in `src/models` (Mongoose). The server is stateless and uses JWTs for authentication.
- Database: MongoDB via Mongoose. Connection code lives in `src/config/database.js` and helper connection utilities under `src/middlewares/helpers`.
- Frontend (client): React (Create React App) with Redux for state management and `redux-thunk` for async actions. UI uses MUI and Tailwind where applicable. The client proxies API requests to the server in development (`client/package.json` proxy).
- Smart contracts: Solidity sources in `contract/`, migrations in `migrations/`. Contracts are not automatically deployed by the app — use Truffle/Hardhat to compile and deploy.
- Third-party integrations: SendGrid (`@sendgrid/mail`) for transactional emails, Cloudinary for media storage, Stripe/Paytm SDKs for payments (example hooks present in controllers), and optional analytics keys in the frontend.

## Tech stack (detailed)

- Runtime: Node.js 14+
- Server framework: Express
- Database: MongoDB (Mongoose ODM)
- Authentication: JSON Web Tokens (JWT)
- Frontend: React (Create React App), Redux, react-router-dom
- UI: Material UI (MUI), Tailwind CSS
- Payments: Stripe (example) and Paytm integration scaffolding
- Email: SendGrid (primary), SMTP fallbacks
- File uploads: express-fileupload + Cloudinary
- Contracts: Solidity (pragma), migration scripts for deployment

## Development workflow

1. Install dependencies:

```bash
npm install
npm install --prefix client
```

2. Create `.env` with the variables listed earlier and start development:

```bash
npm run dev
```

3. Frontend runs on port `3006` (development) and proxies API requests to the backend at `http://localhost:4000`.

## Where to look in the codebase

- API entry: `src/server.js` and `src/app.js`
- DB config: `src/config/database.js`
- Auth utilities: `src/utils/jwtToken.js`, `src/middlewares/user_actions/auth.js`
- Controllers: `src/controllers/*` (products, orders, users, payments)
- Models: `src/models/*` (Product, User, Order, Cart, etc.)
- Frontend entry: `client/src/index.js` and `client/src/App.js`
- Contracts: `contract/` and `migrations/`

## Notes & next steps

- Tests: frontend tests use CRA test tooling; backend tests are not included — I can scaffold Jest + supertest if you want.
- CI/CD: no pipeline configured. I can add a GitHub Actions workflow to build and test both server and client.
- Deployment: the `Procfile` suggests Heroku-style deployment; alternatively build the client and serve statically from the Express server.

If you'd like, I will mark this task complete and can also generate a top-level `.env.example` containing every `process.env` key found in `src/`.


[def]: LICENSE