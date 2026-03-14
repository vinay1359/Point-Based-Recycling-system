# Point-Based Recycling System

A full-stack web application that incentivizes recycling by rewarding users with points they can redeem for vouchers and discounts at partner merchants. The platform allows users to submit recyclable items, accumulate eco-points, and track their environmental impact alongside a community of fellow recyclers.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [API Reference](#api-reference)
- [Database Schema](#database-schema)
- [Authentication](#authentication)
- [Points and Rewards System](#points-and-rewards-system)

---

## Overview

The Point-Based Recycling System, internally called **EcoRewards**, is designed to make recycling rewarding and measurable. Users browse a catalog of accepted recyclable materials (plastic, glass, metal, paper, electronics), add items to a cart, and submit them at a collection point. Upon checkout, the system calculates the monetary value of their submission and converts it into eco-points at a rate of 10 points per rupee. Those points can then be spent on vouchers from partners such as Amazon, Flipkart, Myntra, Swiggy, Zomato, and BookMyShow.

An admin dashboard provides operational visibility into user activity, transaction history, and aggregate platform statistics.

---

## Features

### User Features

- **Account Management** - Register with name, email, mobile number, and password. Login and logout with JWT-based session handling.
- **Recyclable Item Catalog** - Browse items organized by category (plastic, glass, metal, paper, electronics) with size variants (small, medium, large) and per-unit pricing.
- **Shopping Cart** - Add, remove, and adjust quantities of items. Cart persists in browser local storage between sessions.
- **Checkout** - Specify a submission location, submission date, payment method, and optional notes. Points earned are displayed before confirming the order.
- **Rewards Redemption** - Spend accumulated points on vouchers from partner merchants. Browse available rewards and view redemption history.
- **User Profile and Dashboard** - View personal details, current point balance, recycling statistics, and transaction history.
- **Community Leaderboard** - See how your recycling activity compares to other users on the platform.
- **Environmental Impact Counter** - Real-time display of total items recycled and total points distributed across the platform.

### Admin Features

- **Summary Dashboard** - Platform-wide metrics including total transactions, total users, revenue generated, and reward value distributed.
- **User Management** - View all registered users, search by name or email, and sort by points balance.
- **Purchase History** - Browse all purchase records with user details and item breakdowns.
- **Per-User Purchase Tracking** - Drill down into any individual user's transaction history.

---

## Technology Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 15.2.4 (App Router) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 3.4.17 |
| UI Components | Radix UI |
| Animations | Framer Motion |
| Forms | React Hook Form 7.54.1 + Zod 3.24.1 |
| Charts | Recharts 2.15.0 |
| Icons | Lucide React |
| Notifications | Sonner |
| Theme Management | next-themes |
| Authentication | JSON Web Tokens (jsonwebtoken 9.0.2) |
| Password Hashing | bcrypt 5.1.1 |
| Database | SQLite via better-sqlite3 11.9.1 |
| Runtime | Node.js |

---

## Project Structure

```
Point-Based-Recycling-system/
└── pointbased/                        # Next.js application root
    ├── app/
    │   ├── page.tsx                   # Home / landing page
    │   ├── layout.tsx                 # Root layout
    │   ├── globals.css
    │   ├── api/
    │   │   ├── auth/
    │   │   │   ├── login/route.ts
    │   │   │   ├── signup/route.ts
    │   │   │   ├── logout/route.ts
    │   │   │   └── me/route.ts
    │   │   ├── purchases/route.ts
    │   │   ├── final-checkout/route.ts
    │   │   ├── purchase-reward/route.ts
    │   │   ├── user/
    │   │   │   ├── purchases/route.ts
    │   │   │   └── stats/route.ts
    │   │   └── admin/
    │   │       ├── summary/route.ts
    │   │       ├── users/route.ts
    │   │       ├── users/[userId]/purchases/route.ts
    │   │       └── purchases/[purchaseId]/items/route.ts
    │   ├── login/page.tsx
    │   ├── admin/page.tsx
    │   ├── cart/page.tsx
    │   ├── checkout/
    │   │   ├── page.tsx
    │   │   └── success/page.tsx
    │   ├── recyclables/page.tsx
    │   ├── rewards/page.tsx
    │   ├── history/page.tsx
    │   ├── profile/page.tsx
    │   ├── available-rewards/page.tsx
    │   ├── about/page.tsx
    │   ├── faq/page.tsx
    │   ├── contact/page.tsx
    │   ├── privacy/page.tsx
    │   └── terms/page.tsx
    ├── components/
    │   ├── navbar.tsx
    │   ├── footer.tsx
    │   ├── hero-section.tsx
    │   ├── recyclable-items.tsx
    │   ├── cart-provider.tsx
    │   ├── how-it-works.tsx
    │   ├── impact-counter.tsx
    │   ├── community-leaderboard.tsx
    │   ├── eco-mascot.tsx
    │   ├── theme-provider.tsx
    │   ├── theme-toggle.tsx
    │   └── ui/                        # Radix UI component wrappers
    ├── lib/
    │   ├── db.ts                      # SQLite setup and schema initialization
    │   ├── authContext.tsx            # Authentication context provider
    │   └── utils.ts
    ├── hooks/
    │   ├── use-toast.ts
    │   └── use-mobile.tsx
    ├── database/
    │   └── eco-rewards.db             # SQLite database file (auto-created)
    ├── public/                        # Static assets and partner logos
    ├── middleware.ts                  # JWT authentication middleware
    ├── next.config.mjs
    ├── tailwind.config.ts
    ├── tsconfig.json
    ├── postcss.config.mjs
    └── package.json
```

---

## Getting Started

### Prerequisites

- Node.js 18 or later
- npm or pnpm

### Installation

```bash
# Clone the repository
git clone https://github.com/vinay1359/Point-Based-Recycling-system.git
cd Point-Based-Recycling-system/pointbased

# Install dependencies
npm install
```

### Development

```bash
npm run dev
```

The application will be available at `http://localhost:3000`.

### Production Build

```bash
npm run build
npm start
```

### Linting

```bash
npm run lint
```

### Database Initialization

The SQLite database is created automatically at `pointbased/database/eco-rewards.db` on first run. No manual migration step is required. To reset the database, delete the file and restart the server.

---

## Environment Variables

Create a `.env.local` file inside the `pointbased` directory with the following variable:

| Variable | Description | Default |
|---|---|---|
| `JWT_SECRET` | Secret key used to sign and verify JWT tokens | `fallback_secret` (insecure, change in production) |

Example:

```env
JWT_SECRET=your_strong_random_secret_here
```

---

## API Reference

All API routes are located under `/api/`. Authenticated routes require a valid `auth_token` HTTP-only cookie issued at login.

### Authentication

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| POST | `/api/auth/signup` | Create a new user account | No |
| POST | `/api/auth/login` | Authenticate and receive a session cookie | No |
| POST | `/api/auth/logout` | Clear the session cookie | No |
| GET | `/api/auth/me` | Return the currently authenticated user | No (reads cookie) |

### User

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| GET | `/api/user/purchases` | List the authenticated user's purchase history | Yes |
| GET | `/api/user/stats` | Return the user's point balance and recycling statistics | Yes |

### Shopping and Checkout

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| POST | `/api/purchases` | Record cart items as a purchase in the database | Yes |
| POST | `/api/final-checkout` | Complete checkout, deduct cart, and add points to the user account | Yes |
| POST | `/api/purchase-reward` | Redeem accumulated points for a reward | Yes |

### Admin

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| GET | `/api/admin/summary` | Platform-wide statistics | Yes |
| GET | `/api/admin/users` | List all registered users | Yes |
| GET | `/api/admin/users/[userId]/purchases` | Purchase history for a specific user | Yes |
| GET | `/api/admin/purchases/[purchaseId]/items` | Line items for a specific purchase | Yes |

---

## Database Schema

The application uses SQLite with three tables.

### users

| Column | Type | Description |
|---|---|---|
| `id` | INTEGER | Primary key, auto-increment |
| `name` | TEXT | Full name |
| `email` | TEXT | Unique email address |
| `mobile` | TEXT | Mobile number |
| `password` | TEXT | bcrypt-hashed password |
| `points` | INTEGER | Current point balance (default 0) |
| `created_at` | DATETIME | Account creation timestamp |

### purchases

| Column | Type | Description |
|---|---|---|
| `id` | INTEGER | Primary key, auto-increment |
| `user_id` | INTEGER | Foreign key to `users.id` |
| `total_amount` | REAL | Total value of the submission in rupees |
| `payment_method` | TEXT | Payment method selected at checkout |
| `submission_location` | TEXT | Location where items were submitted |
| `created_at` | DATETIME | Transaction timestamp |

### purchase_items

| Column | Type | Description |
|---|---|---|
| `id` | INTEGER | Primary key, auto-increment |
| `purchase_id` | INTEGER | Foreign key to `purchases.id` |
| `item_id` | TEXT | Catalog item identifier |
| `name` | TEXT | Item name |
| `size` | TEXT | Size variant (small, medium, large) |
| `quantity` | INTEGER | Number of units |
| `price` | REAL | Price per unit in rupees |
| `image` | TEXT | Image path |
| `is_reward` | BOOLEAN | True if this line item is a redeemed reward |

---

## Authentication

Authentication is handled with JSON Web Tokens stored in HTTP-only cookies. The middleware at `middleware.ts` intercepts requests to protected routes (`/profile`, `/checkout`) and verifies the token before allowing access. Unauthenticated requests are redirected to `/login` with a `callbackUrl` parameter so users are returned to their intended destination after logging in.

Tokens are signed using the `JWT_SECRET` environment variable and are valid for 7 days.

---

## Points and Rewards System

The points system is designed around a simple conversion rate:

```
10 eco-points = 1 rupee of recyclable value
```

For example, submitting recyclable items worth 150 rupees earns the user 1,500 eco-points. Points are credited immediately upon checkout confirmation and reflected in the user's profile and on the leaderboard.

Points can be spent in the rewards catalog to obtain discount vouchers or gift cards from partner merchants. The `purchase-reward` API endpoint deducts the appropriate point cost and records the redemption in `purchase_items` with `is_reward = true`.
