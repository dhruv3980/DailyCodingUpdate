# E-Commerce Project – User Authentication Module

**Date:** 21 August 2025  

## Overview

Today, I implemented the **User Authentication and Authorization** functionality in my E-Commerce project. This includes:

- **User Registration**
- **User Login**
- **JWT Token Generation**
- **Password Hashing with bcrypt**
- **Cookie-based Authentication**
- **Authorization Middleware**

---

## Features Implemented

### 1. User Registration (`/registeruser`)
- Users can register with **name, email, and password**.
- Password is hashed before saving using **bcrypt**.
- JWT token is generated upon successful registration.
- Token is stored as an **HTTP-only secure cookie**.
- Response includes the user data and token.

### 2. User Login (`/login-user`)
- Users can log in with **email and password**.
- Passwords are compared using **bcrypt.compare**.
- JWT token is generated upon successful login.
- Token is sent via **HTTP-only secure cookie**.
- Response includes user data and token.

### 3. JWT Token Helper
- `jwthelper` function generates JWT token.
- Sets **HTTP-only cookie** with a 3-day expiration.
- Sends a unified response including user and token.

### 4. Authorization Middleware
- Checks if the **JWT token** exists in cookies.
- Verifies token using `jwt.verify`.
- Attaches authenticated user to `req.user`.
- Protects routes for authorized users only.

---

## Tech Stack & Libraries
- **Node.js** & **Express.js**
- **MongoDB** with **Mongoose**
- **bcrypt** – Password hashing
- **jsonwebtoken** – JWT generation & verification
- **Express Middleware** for async error handling
- **Cookie-parser** for cookie management

---

## Folder Structure (Relevant Files)
controllers/
Usercontroller.js
middlewares/
asyncHandlermiddleware.js
Authorization.js
models/
User.models.js
utils/
Apiresponse.js
ApiError.js
JwttokenSenderhelper.js
routes/
userRoutes.js

yaml
Copy code

---

## Usage
1. **Register User**
```http
POST /registeruser
Content-Type: application/json
Body:
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "password": "password123"
}
Login User

http
Copy code
POST /login-user
Content-Type: application/json
Body:
{
  "email": "johndoe@example.com",
  "password": "password123"
}
Protected Routes

Include Authorization middleware to protect routes.

Example:

javascript
Copy code
app.get('/getProfile', Authorization, getProfileController);
Notes
Used userSchema.pre('save') hook to hash passwords automatically.

userSchema.methods.checkPasswordCorrect compares entered password with hashed password.

JWT token expiration set via process.env.JwtExpiry.

Cookie options include httpOnly: true and secure: true for better security.

✅ Status: Completed registration, login, JWT handling, and authorization middleware successfully.

