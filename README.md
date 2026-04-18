# Finanseer

A financial dashboard for visualising KPIs, revenue, expenses, products, and transactions — with a linear regression model for revenue predictions.

🔗 **Live Demo:** [https://finapp-bpiy.vercel.app](https://finapp-bpiy.vercel.app)

---

## Tech Stack

**Frontend**
- React 18 + TypeScript + Vite
- MUI (Material UI) for components and theming
- Recharts for data visualisation
- Redux Toolkit + RTK Query for state and API calls
- `regression` library for linear regression predictions

**Backend**
- Node.js + Express
- MongoDB + Mongoose
- `mongoose-currency` for currency type handling

**Deployment**
- Frontend → Vercel
- Backend → Vercel (serverless)
- Database → MongoDB Atlas

---

## Features

- Revenue & expenses area/line/bar charts (monthly)
- Operational vs non-operational expense breakdown
- Product price vs expense scatter chart
- Expense breakdown by category (pie charts)
- Products and transactions data grids
- Revenue prediction page using linear regression

---

## Running Locally

### Prerequisites
- Node.js 18+
- A MongoDB Atlas account (or local MongoDB)

### 1. Clone the repo
```bash
git clone https://github.com/DashMav/finapp.git
cd finapp
```

### 2. Set up environment variables

`server/.env`
```env
MONGO_URL=mongodb+srv://<user>:<password>@cluster.mongodb.net/finapp
PORT=9000
```

`client/.env`
```env
VITE_BASE_URL=http://localhost:9000
```

### 3. Install dependencies
```bash
cd server && npm install
cd ../client && npm install
```

### 4. Seed the database (first run only)

In `server/index.js`, temporarily uncomment these lines, start the server once, then re-comment them:
```js
await mongoose.connection.db.dropDatabase();
KPI.insertMany(kpis);
Product.insertMany(products);
Transaction.insertMany(transactions);
```

### 5. Start both servers
```bash
# Terminal 1
cd server && npm run dev

# Terminal 2
cd client && npm run dev
```

Open [http://localhost:5173](http://localhost:5173)

---

## Project Structure

```
finapp/
├── client/          # React + Vite frontend
│   └── src/
│       ├── components/   # Reusable UI components
│       ├── scenes/       # Dashboard, Navbar, Predictions pages
│       └── state/        # RTK Query API + TypeScript types
└── server/          # Express backend
    ├── data/         # Seed data
    ├── models/       # Mongoose models (KPI, Product, Transaction)
    └── routes/       # API routes
```

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/kpi/kpis/` | Fetch all KPI data |
| GET | `/product/products/` | Fetch all products |
| GET | `/transaction/transactions/` | Fetch all transactions |

---

## Roadmap — v2

### Authentication
- Sign up / login / logout
- JWT-based auth with protected routes
- Each user only sees their own data

### Multi-tenancy
- All models scoped to a `userId`
- Fully isolated data per account

### Data Input
- Forms to add, edit, and delete transactions, products, and expenses
- CSV import for bulk uploading historical data
- Onboarding flow to guide new users through their first entries

### Live KPI Calculation
- KPIs (revenue, profit, expenses) auto-calculated from real user data
- Dashboard updates in real time as data is added

### UX Improvements
- Loading skeletons while data fetches
- Error states for failed API calls
- KPI summary cards (total revenue, profit, expenses) at the top of the dashboard
- Daily revenue/expenses chart (data already exists in the model)
- Date range filter across all charts

### Predictions
- Polynomial regression and moving average models alongside the existing linear regression
- Confidence intervals on the prediction chart
