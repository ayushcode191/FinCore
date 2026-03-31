# 🏦 Fincore – Banking Backend API

Fincore is a backend system that simulates core banking operations like user authentication, account management, and secure money transfers.

The focus of this project is not just CRUD APIs, but building a system that handles transactions reliably using concepts like **ledger entries, idempotency, and JWT-based authentication**.

---

## 📌 Project Highlights

- User authentication using JWT  
- Support for multiple accounts per user  
- Secure fund transfer between accounts  
- Ledger-based transaction system (no direct balance updates)  
- Idempotency handling to prevent duplicate transactions  
- Token blacklisting for logout  
- Account status management (`ACTIVE`, `FROZEN`, `CLOSED`)  
- Email notifications for important actions  

---

## 🧠 Design Approach

Instead of storing balance directly in the account, this project follows a **ledger-based model**.

Every transaction creates:
- a **DEBIT entry** (from sender)
- a **CREDIT entry** (to receiver)

The account balance is calculated from these entries when needed.

This approach helps in:
- maintaining transaction history
- avoiding inconsistencies
- making the system closer to real-world banking systems

---

## 🏗️ Tech Stack

- Node.js  
- Express.js  
- MongoDB (Mongoose)  
- JWT for authentication  
- bcrypt for password hashing  
- Nodemailer for email service  

---

## 📁 Project Structure

```bash
Backend-Fincore/
│
├── src/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── app.js
│
├── server.js
├── .env
└── package.json
```

---

## ⚙️ Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/ayushcode191/FinCore.git
cd FinCore
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create `.env` file

```env
PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_secret_key

EMAIL_USER=your_email
EMAIL_PASS=your_password
```

### 4. Run the server

```bash
npm run dev
```

or

```bash
node server.js
```

---

## 🔐 Authentication

- Register → creates user with hashed password  
- Login → returns JWT token  
- Logout → token is blacklisted  

---

## 🏦 Core APIs

### Auth
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/logout`

### Accounts
- `POST /api/accounts/create`
- `GET /api/accounts`
- `GET /api/accounts/:accountId/balance`

### Transactions
- `POST /api/transactions/create`
- `POST /api/transactions/initial-funds`

---

## 💸 Example Transaction

```json
{
  "fromAccount": "account_id_1",
  "toAccount": "account_id_2",
  "amount": 500,
  "idempotencyKey": "unique-key-123"
}
```

---

## 🔒 Notes on Safety

- Passwords are stored in hashed form  
- Ledger entries cannot be modified once created  
- Duplicate transactions are avoided using idempotency keys  
- Only authenticated users can access protected routes  

---

## 💡 Backend Concepts Implemented

This project covers several important backend concepts:

- REST API design  
- authentication & authorization using JWT  
- secure password hashing  
- database schema design with MongoDB  
- ledger-based accounting system  
- idempotent transaction handling  
- multi-account management  
- token blacklisting for logout  

The goal was to build something closer to a real-world backend rather than a simple CRUD application.

---

## 🚀 Future Improvements

- Transaction history with pagination  
- Admin features (freeze/unfreeze accounts)  
- Rate limiting and security middleware  
- API documentation (Swagger)  
- Frontend integration  

---

## 👨‍💻 Author

**Ayush Bansal**  
B.Tech IT  

---

## ⭐

If you found this useful, feel free to star the repo.