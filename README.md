# Login Page

A full-stack login/registration system with a sleek animated frontend and a Node.js/Express backend, using PostgreSQL for storage and JWT for authentication.

## 🔗 Live Demo

Frontend: [Vercel deployment link here]

> Note: The backend currently runs locally only, so registration/login won't work on the live demo until the backend is deployed separately (see [Roadmap](#roadmap)).

## Features

- Sleek animated sign-in / sign-up UI with dark/light theme toggle
- Password hashing with bcrypt (passwords are never stored in plain text)
- JWT-based authentication for protected routes
- PostgreSQL database for persistent user storage

## Tech Stack

**Frontend**
- HTML, CSS, JavaScript (vanilla)

**Backend**
- Node.js
- Express
- PostgreSQL (`pg`)
- bcrypt (password hashing)
- jsonwebtoken (JWT auth)
- dotenv (environment variables)
- cors

## Project Structure

```
login page 1/
├── backend/
│   ├── server.js
│   ├── package.json
│   ├── .env          (not committed — see setup below)
│   └── .gitignore
└── frontend/
    └── index.html
```

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org) (LTS version)
- [PostgreSQL](https://www.postgresql.org/download/)

### 1. Clone the repo

```bash
git clone https://github.com/yatzoyap/login-page-template-1.git
cd login-page-template-1/backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up the database

Create a database in PostgreSQL (e.g. via pgAdmin or `psql`), then run:

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);
```

### 4. Configure environment variables

Create a `.env` file inside `backend/`:

```
DB_USER=postgres
DB_HOST=localhost
DB_NAME=your_database_name
DB_PASSWORD=your_db_password
DB_PORT=5432
JWT_SECRET=your_super_secret_key_here
```

### 5. Run the server

```bash
node server.js
```

The server will run on `http://localhost:3000`.

### 6. Open the frontend

Open `frontend/index.html` in your browser, or serve it locally. Make sure the backend is running so the register/login requests succeed.

## Testing From Another Device (e.g. Your Phone)

`localhost:3000` only works on the same machine the server is running on — it will **not** work from a phone or any other device, even if the frontend is live on Vercel.

To test from another device on the same Wi-Fi network:

1. Find your computer's local IP address:
   ```bash
   ipconfig
   ```
   Look for the **IPv4 Address** under your active network adapter (e.g. `192.168.1.42`).

2. In the frontend's `fetch()` calls, replace `http://localhost:3000` with that IP, e.g.:
   ```javascript
   fetch('http://192.168.1.42:3000/api/register', { ... })
   ```

3. Make sure your phone is connected to the **same Wi-Fi network** as your computer.

This is a temporary workaround for local testing. Once the backend is deployed (see [Roadmap](#roadmap)), any device can reach it via its public URL instead.

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/register` | Register a new user |
| POST | `/api/login` | Log in and receive a JWT |
| GET | `/api/dashboard` | Protected route, requires a valid JWT |

## Roadmap

- [ ] Deploy backend to a Node-friendly host (Render / Railway)
- [ ] Move database to a hosted provider (Supabase / Neon)
- [ ] Connect deployed frontend to deployed backend
- [ ] Add password reset flow
- [ ] Add input validation on the frontend

## License

This project is for personal/portfolio use.
As of 9th of September 2026, the website is still running localhost 3000
