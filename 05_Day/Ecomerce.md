
# 🛒E-Commerce Project 

**Date:** 22 August 2025  

🚀 Features Implemented
1. Email Service (Password Reset Support)

Integrated Nodemailer with environment-based configuration.

Implemented a reusable sendEMail function for sending emails.

Added password reset flow:

User can request a reset link.

Token is generated & hashed (crypto).

Reset link expires in 30 minutes.

Email sent with secure reset link.

2. Authentication Enhancements

Logout User endpoint:

Clears JWT token from cookies.

Ensures secure session management.

Role-Based Access Middleware:

Restricts access to routes based on roles.

Example: roleBasedAccess("admin") → only admins can perform certain actions.

3. User Schema Update

Added generatePasswordResetToken method.

Uses crypto to generate and hash tokens.

Stores token + expiry on user model.

4. Product Schema Update

Linked product to a user (creator) using ref: "User".

Helps track who created the product.

5. Protected Routes for Admin

Only admin users can:

Create products

Update products

Delete products

📂 Folder Structure
/controllers
   - UserController.js
   - ProductController.js
/models
   - User.models.js
   - Product.models.js
/utils
   - sendMail.js
   - ApiError.js
   - ApiResponse.js
/middleware
   - roleBasedAccess.js
   - asyncHandler.js

⚡ API Endpoints (New/Updated)
Auth & User

POST /api/v1/auth/logout → Logout user

POST /api/v1/auth/request-reset-password → Send password reset token

POST /api/v1/auth/reset/:token → Reset password

Products (Protected – Admin Only)

POST /api/v1/products → Create product

PUT /api/v1/products/:id → Update product

DELETE /api/v1/products/:id → Delete product

🔒 Security

JWT stored in httpOnly cookies.

Password reset tokens hashed before saving in DB.

Admin-only access for product management.