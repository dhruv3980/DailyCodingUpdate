# 🛒 E-Commerce Project – Day 1 Progress

## 📌 Today's Update
Today, I set up the initial structure of my **E-Commerce Project**.  
I focused on two main parts:
1. **Product Schema** – defined using Mongoose.
2. **Product Controllers** – to handle CRUD operations.

---

## 🗂️ Product Schema
I created a `Product` model with the following fields:
- **name** (required) – product name.
- **description** (required) – product details.
- **price** (required, max 7 digits).
- **ratings** – default `0`.
- **images** – array with `public_id` and `url`.
- **category** (required).
- **stock** (required, max `9999`, default `1`).
- **numOfReviews** – default `0`.
- **reviews** – array with `name`, `rating`, and `comment`.
- **createdAt** – default `Date.now`.

📂 File: `models/Product.models.js`

---

## ⚡ Product Controllers
I implemented **5 controller functions** to manage product operations:

1. **Create Product**  
   ➝ `POST /api/products`  
   Creates a new product.

2. **Delete Product**  
   ➝ `DELETE /api/products/:id`  
   Deletes a product by ID.

3. **Get All Products**  
   ➝ `GET /api/products`  
   Fetches all products.

4. **Get Single Product**  
   ➝ `GET /api/products/:id`  
   Fetches a single product by ID.

5. **Update Product**  
   ➝ `PUT /api/products/:id`  
   Updates product details.

📂 File: `controllers/product.controllers.js`

---

🚀 *Day 1 complete – Backend setup started successfully!*
