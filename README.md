# MVC Authentication API

A complete, production-ready RESTful Authentication API built with **Node.js**, **Express.js**, **MongoDB (Mongoose)**, **JWT**, and **bcryptjs**, structured following the **MVC (Model-View-Controller)** architectural pattern with ES modules.

---

## 📁 Project Architecture

```
MVC Authentication/
├── config/
│   └── db.js                 # MongoDB connection logic using Mongoose
├── controllers/
│   └── authController.js     # User registration, login, and profile logic
├── middleware/
│   ├── authMiddleware.js     # JWT verification & protected route guard
│   └── errorMiddleware.js    # Global error & 404 handler
├── models/
│   └── User.js               # Mongoose schema, validation & bcrypt hooks
├── routes/
│   └── authRoutes.js         # Authentication endpoints router
├── .env                      # Environment variables (secret keys, port, db)
├── .env.example              # Sample environment template
├── .gitignore                # Ignored Git files (node_modules, .env)
├── package.json              # Scripts & dependencies (ES Module enabled)
└── server.js                 # Express application entrypoint
```

---

## 🚀 Setup & Execution

### 1. Install Dependencies
If not already installed, run:
```bash
npm install
```

### 2. Configure Environment Variables
Verify your [.env](file:///d:/fsd-2/MVC%20Authentication/.env) file:
```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/mvc_auth_db
JWT_SECRET=your_super_secret_jwt_key_here_change_in_production
JWT_EXPIRES_IN=7d
```
*(Make sure your local MongoDB server is running or replace `MONGO_URI` with a MongoDB Atlas connection string).*

### 3. Start the Server
- **Development mode (auto-restart with nodemon):**
  ```bash
  npm run dev
  ```
- **Production mode:**
  ```bash
  npm start
  ```

---

## 📡 API Endpoints

### 1. Register User
- **Method:** `POST`
- **URL:** `http://localhost:5000/api/auth/register`
- **Headers:** `Content-Type: application/json`
- **Body:**
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Response (`201 Created`):**
  ```json
  {
    "success": true,
    "message": "User registered successfully",
    "data": {
      "_id": "673cf...",
      "name": "John Doe",
      "email": "john@example.com",
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
  }
  ```

### 2. Login User
- **Method:** `POST`
- **URL:** `http://localhost:5000/api/auth/login`
- **Headers:** `Content-Type: application/json`
- **Body:**
  ```json
  {
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Response (`200 OK`):**
  ```json
  {
    "success": true,
    "message": "Logged in successfully",
    "data": {
      "_id": "673cf...",
      "name": "John Doe",
      "email": "john@example.com",
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
    }
  }
  ```

### 3. Get User Profile (Protected Route)
- **Method:** `GET`
- **URL:** `http://localhost:5000/api/auth/profile`
- **Headers:**
  - `Authorization`: `Bearer <YOUR_JWT_TOKEN>`
- **Response (`200 OK`):**
  ```json
  {
    "success": true,
    "data": {
      "_id": "673cf...",
      "name": "John Doe",
      "email": "john@example.com",
      "createdAt": "2026-11-19T17:00:00.000Z"
    }
  }
  ```
