# 📦 Online Product Inventory System

A modern, full-stack inventory management system built with **React.js**, **Laravel**, and **PostgreSQL**.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![React](https://img.shields.io/badge/React-18.x-61dafb.svg)
![Laravel](https://img.shields.io/badge/Laravel-12.x-ff2d20.svg)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15.x-336791.svg)

## ✨ Features

### Core Features

- **User Authentication** - Secure login/logout with Laravel Sanctum
- **Category Management** - Full CRUD operations for product categories
- **Product Management** - Complete product lifecycle management with search & filters
- **Stock Management** - Stock in/out operations with validation and audit trail
- **Dashboard Analytics** - Real-time stats, low stock alerts, and visualizations

### Technical Features

- 🔐 Token-based authentication (Bearer tokens)
- 🔄 Real-time data updates with React Query
- 📱 Fully responsive design
- ✅ Form validation on frontend and backend
- 📊 Interactive charts with Recharts
- 🎨 Beautiful UI with Tailwind CSS & shadcn/ui

## 🏗️ Architecture

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│   React.js      │────▶│   Laravel       │────▶│  PostgreSQL     │
│   Frontend      │     │   REST API      │     │   Database      │
│                 │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
     Port 5173              Port 8000              Port 5432
```

## 📁 Project Structure

```
assignment/
├── client/                    # React Frontend
│   ├── src/
│   │   ├── components/       # Reusable UI components
│   │   ├── contexts/         # React contexts (Auth)
│   │   ├── hooks/            # Custom React hooks
│   │   ├── pages/            # Page components
│   │   ├── shared/           # Shared types & routes
│   │   └── lib/              # Utilities
│   ├── vercel.json           # Vercel deployment config
│   └── package.json
│
├── server/                    # Laravel Backend
│   ├── app/
│   │   ├── Http/Controllers/Api/
│   │   └── Models/
│   ├── database/
│   │   ├── migrations/
│   │   └── seeders/
│   ├── routes/api.php
│   └── render.yaml           # Render deployment config
│
└── README.md
```

## 🚀 Quick Start

### Prerequisites

- PHP 8.2+
- Composer
- Node.js 18+
- PostgreSQL 15+

### Local Development

#### Backend Setup

```bash
cd server

# Install dependencies
composer install

# Configure environment
cp .env.example .env
php artisan key:generate

# Update .env with your database credentials
# DB_CONNECTION=pgsql
# DB_HOST=127.0.0.1
# DB_PORT=5432
# DB_DATABASE=inventory_system
# DB_USERNAME=postgres
# DB_PASSWORD=postgres

# Run migrations and seed
php artisan migrate --seed

# Start server
php artisan serve --port=8003
```

#### Frontend Setup

```bash
cd client

# Install dependencies
npm install

# Start development server
npm run dev
```

## 🔑 Demo Credentials

| Role  | Email               | Password    |
| ----- | ------------------- | ----------- |
| Admin | admin@inventory.com | password123 |
| Demo  | demo@inventory.com  | demo123     |

## 📡 API Endpoints

### Authentication

| Method | Endpoint           | Description       |
| ------ | ------------------ | ----------------- |
| POST   | /api/auth/register | Register new user |
| POST   | /api/auth/login    | Login user        |
| POST   | /api/auth/logout   | Logout user       |
| GET    | /api/auth/me       | Get current user  |

### Categories

| Method | Endpoint            | Description         |
| ------ | ------------------- | ------------------- |
| GET    | /api/categories     | List all categories |
| POST   | /api/categories     | Create category     |
| GET    | /api/categories/:id | Get category        |
| PUT    | /api/categories/:id | Update category     |
| DELETE | /api/categories/:id | Delete category     |

### Products

| Method | Endpoint          | Description                  |
| ------ | ----------------- | ---------------------------- |
| GET    | /api/products     | List products (with filters) |
| POST   | /api/products     | Create product               |
| GET    | /api/products/:id | Get product                  |
| PUT    | /api/products/:id | Update product               |
| DELETE | /api/products/:id | Delete product               |
| GET    | /api/stats        | Get dashboard stats          |

### Stock Management

| Method | Endpoint                          | Description       |
| ------ | --------------------------------- | ----------------- |
| POST   | /api/products/:id/stock-in        | Add stock         |
| POST   | /api/products/:id/stock-out       | Remove stock      |
| GET    | /api/products/:id/stock-movements | Get stock history |

## 🗃️ Database Schema

### Categories Table

| Column      | Type      | Description            |
| ----------- | --------- | ---------------------- |
| id          | BIGINT    | Primary Key            |
| name        | VARCHAR   | Category name (unique) |
| description | TEXT      | Optional description   |
| status      | ENUM      | active/inactive        |
| created_at  | TIMESTAMP | Created timestamp      |

### Products Table

| Column      | Type    | Description                     |
| ----------- | ------- | ------------------------------- |
| id          | BIGINT  | Primary Key                     |
| category_id | BIGINT  | Foreign Key to categories       |
| name        | VARCHAR | Product name                    |
| sku         | VARCHAR | Stock Keeping Unit (unique)     |
| price       | INTEGER | Price in cents                  |
| quantity    | INTEGER | Current stock level             |
| status      | ENUM    | in_stock/low_stock/out_of_stock |
| description | TEXT    | Optional description            |
| image_url   | VARCHAR | Product image URL               |

### Stock Movements Table

| Column            | Type    | Description     |
| ----------------- | ------- | --------------- |
| id                | BIGINT  | Primary Key     |
| product_id        | BIGINT  | Foreign Key     |
| user_id           | BIGINT  | Who made change |
| type              | ENUM    | in/out          |
| quantity          | INTEGER | Amount changed  |
| previous_quantity | INTEGER | Before change   |
| new_quantity      | INTEGER | After change    |
| notes             | TEXT    | Optional notes  |

## 🔒 Validation Rules

### Product Validation

- **name**: Required, max 255 characters
- **sku**: Required, unique, max 100 characters
- **category**: Required
- **price**: Required, numeric, min 0
- **quantity**: Required, integer, min 0

### Stock Movement Validation

- **quantity**: Required, integer, min 1
- Cannot stock-out more than available quantity

## 🎨 UI Components

Built with [shadcn/ui](https://ui.shadcn.com/) components:

- Responsive tables with sorting
- Form validation with error messages
- Toast notifications
- Delete confirmation dialogs
- Loading skeletons
- Animated transitions (Framer Motion)

## 🧪 Testing

```bash
# Backend tests
cd server
php artisan test

# Frontend (if configured)
cd client
npm test
```

## 📦 Deployment

### Frontend on Vercel

1. Push your code to GitHub
2. Go to [vercel.com](https://vercel.com) and import the repository
3. Set **Root Directory** to `client`
4. Add environment variable:
   - `VITE_API_URL` = `https://your-render-app.onrender.com/api`
5. Deploy!

### Backend on Render

1. Go to [render.com](https://render.com) and create a new **Web Service**
2. Connect your repository and set **Root Directory** to `server`
3. Configure:
   - **Runtime**: PHP
   - **Build Command**: `composer install --no-dev --optimize-autoloader`
   - **Start Command**: `php artisan serve --host=0.0.0.0 --port=$PORT`
4. Add environment variables:
   - `APP_KEY` - Generate with `php artisan key:generate --show`
   - `APP_ENV` = `production`
   - `APP_DEBUG` = `false`
   - `DB_CONNECTION` = `pgsql`
   - `DB_HOST` = Your PostgreSQL host
   - `DB_DATABASE` = Your database name
   - `DB_USERNAME` = Your database user
   - `DB_PASSWORD` = Your database password
   - `FRONTEND_URL` = Your Vercel URL
   - `SANCTUM_STATEFUL_DOMAINS` = Your Vercel domain

5. Create a PostgreSQL database on Render or use external provider
6. After deployment, run migrations:
   ```bash
   php artisan migrate --seed
   ```

## 🔧 Environment Variables

### Backend (.env)

```env
APP_URL=http://localhost:8000
DB_CONNECTION=pgsql
DB_HOST=localhost
DB_DATABASE=inventory_system
DB_USERNAME=postgres
DB_PASSWORD=postgres
FRONTEND_URL=http://localhost:5173
SANCTUM_STATEFUL_DOMAINS=localhost:5173
```

### Frontend (.env)

```env
VITE_API_URL=http://localhost:8000/api
```

## 📝 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- [Laravel](https://laravel.com/)
- [React](https://react.dev/)
- [shadcn/ui](https://ui.shadcn.com/)
- [Tailwind CSS](https://tailwindcss.com/)
- [React Query](https://tanstack.com/query)
