# 🛒 E-Commerce Project  

📅 **Progress Date**: 25/08/2025  

This is a Node.js + Express + MongoDB based **E-Commerce Backend API**.  
  

---

## 🚀 Features Implemented So Far  

### ✅ Orders
- **Create New Order**  
  - Validates required fields (`shippingInfo`, `orderItems`, `paymentInfo`, etc.).  
  - Saves order to MongoDB.  
  - Links order with logged-in user.  

- **Get Single Order (Admin)**  
  - `GET /api/v1/admin/order/:id`  
  - Admin can fetch details of a **specific order** by passing the **Order ID**.  
  - User details (name & email) are populated for reference.  

- **Get My Orders (User)**  
  - `GET /api/v1/orders/user`  
  - Returns all orders created by the logged-in user.  

- **Get All Orders (Admin)**  
  - `GET /api/v1/admin/orders`  
  - Fetches all orders in the database.  
  - Calculates total amount from all orders.  

---

## ⚠️ Pending / In Progress  
- **Order Status Updates**  
  - Add fields for `orderStatus` (Processing, Shipped, Delivered, Cancelled).  
  - Add `updateOrderStatus` controller (Admin only).  
  - Update `deliveredAt` when status is set to Delivered.  

---

## 📂 API Routes  

| Method | Route | Access | Description |
|--------|--------|--------|-------------|
| POST   | `/api/v1/new/order`       | User  | Create new order |
| GET    | `/api/v1/orders/user`     | User  | Get logged-in user's orders |
| GET    | `/api/v1/admin/order/:id` | Admin | **Get details of a specific order by ID** |
| GET    | `/api/v1/admin/orders`    | Admin | Get all orders + total amount |

---

## 🛠️ Tech Stack  
- **Backend**: Node.js, Express.js  
- **Database**: MongoDB (Mongoose ODM)  
- **Auth**: JWT-based Authorization  
- **Utilities**: Custom `ApiResponse`, `ApiError` classes  

---

## 📌 Next Steps  
- Implement **order status update API**.  
 

---

## 👨‍💻 Author  
**Dhruv Sahu**  
MERN Stack Developer  

