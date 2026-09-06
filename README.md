# 🛒 Sales Savvy - E-Commerce Application

A full-stack e-commerce application built with **React.js** (Frontend) and **Spring Boot** (Backend), featuring secure payment integration with Razorpay.

---

## 📋 Table of Contents
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Screenshots](#screenshots)
- [Contributing](#contributing)
- [License](#license)

---

## ✨ Features

### User Features
- 🔐 User Authentication (Login/Register)
- 🛍️ Browse Products by Category
- 🛒 Add/Remove Items from Cart
- 💳 Secure Checkout with Razorpay Payment Gateway
- 📦 Order History & Tracking
- 👤 User Profile Management

### Admin Features
- 📊 Admin Dashboard
- ➕ Add/Edit/Delete Products
- 👥 User Management
- 📋 Order Management
- 📈 View Total Sales

---

## 🛠️ Tech Stack

### Frontend
- **React.js** (v19.1.1) - UI Library
- **React Router DOM** (v7.9.4) - Navigation
- **Bootstrap** (v5.3.8) - UI Framework
- **Axios** (v1.12.2) - HTTP Client
- **Vite** (v7.1.7) - Build Tool

### Backend
- **Spring Boot** (v3.5.0) - Java Framework
- **Spring Security** - Authentication & Authorization
- **Spring Data JPA** - Database ORM
- **MySQL** (v8.0.38) - Database
- **JWT** (v0.11.5) - Token-based Authentication
- **Razorpay SDK** (v1.4.5) - Payment Integration

---

## 📁 Project Structure

```
sales-savvy/
├── sales-savvy-be/                    # Backend (Spring Boot)
│   ├── src/main/java/com/salesSavvy/
│   │   ├── config/                    # Security & CORS Configuration
│   │   ├── controller/                # REST Controllers
│   │   ├── dto/                       # Data Transfer Objects
│   │   ├── entity/                    # JPA Entities
│   │   ├── exception/                 # Custom Exceptions
│   │   ├── repository/                # Database Repositories
│   │   ├── security/                  # JWT & Security Classes
│   │   └── service/                   # Business Logic
│   ├── src/main/resources/
│   │   └── application.properties     # Application Configuration
│   ├── pom.xml                        # Maven Dependencies
│   └── .env.example                   # Environment Variables Template
│
└── sales_savvy_fr/                    # Frontend (React)
    ├── src/
    │   ├── components/                # Reusable Components
    │   │   ├── auth/                  # Login & Register
    │   │   ├── cart/                  # Cart Components
    │   │   ├── common/                # Header, Footer, Loading
    │   │   ├── orders/                # Order Components
    │   │   └── products/              # Product Components
    │   ├── context/                   # React Context (Auth)
    │   ├── pages/                     # Page Components
    │   ├── services/                  # API Service Layer
    │   ├── App.jsx                    # Main App Component
    │   └── main.jsx                   # Entry Point
    ├── package.json                   # NPM Dependencies
    └── vite.config.js                 # Vite Configuration
```

---

## 📌 Prerequisites

Before running the application, ensure you have the following installed:

- **Java 17+** (JDK)
- **Node.js** (v20.19.0 or v22.12.0+)
- **MySQL** (v8.0+)
- **Maven** (v3.9.9+)
- **Razorpay Account** (for payment integration)

---

## 🚀 Installation & Setup

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/sandeepkrmehta/sales-savvy.git
cd sales-savvy
```

### 2️⃣ Backend Setup (Spring Boot)

#### Step 1: Create MySQL Database
```sql
CREATE DATABASE ecom;
```

#### Step 2: Configure Environment Variables
Copy `.env.example` to `.env` and update with your credentials:

```bash
cd sales-savvy-be
cp .env.example .env
```

Update `.env` file:
```properties
DB_URL=jdbc:mysql://localhost:3306/ecom
DB_USERNAME=root
DB_PASSWORD=your_password

RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret

JWT_SECRET=your_secure_jwt_secret_key
ADMIN_PASSWORD=your_admin_password
```

#### Step 3: Install Dependencies & Run
```bash
# Using Maven Wrapper (Recommended)
./mvnw clean install
./mvnw spring-boot:run

# Or using Maven directly
mvn clean install
mvn spring-boot:run
```

**Backend will run on:** `http://localhost:8080`

---

### 3️⃣ Frontend Setup (React + Vite)

#### Step 1: Install Dependencies
```bash
cd sales_savvy_fr
npm install
```

#### Step 2: Run Development Server
```bash
npm run dev
```

**Frontend will run on:** `http://localhost:5173`

---

## ⚙️ Configuration

### Backend Configuration (`application.properties`)
```properties
# Server Configuration
server.port=8080

# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/ecom
spring.datasource.username=root
spring.datasource.password=1234

# JPA/Hibernate Configuration
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# JWT Configuration
jwt.secret=your_jwt_secret
jwt.expiration=86400000

# Razorpay Configuration
razorpay.key.id=your_razorpay_key_id
razorpay.key.secret=your_razorpay_key_secret
```

### Frontend Configuration (`vite.config.js`)
```javascript
export default defineConfig({
  plugins: [react()],
  server: {
    port: 5173,
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  }
})
```

---

## 🏃 Running the Application

### Option 1: Development Mode
```bash
# Terminal 1 - Backend
cd sales-savvy-be
./mvnw spring-boot:run

# Terminal 2 - Frontend
cd sales_savvy_fr
npm run dev
```

### Option 2: Production Build
```bash
# Build Frontend
cd sales_savvy_fr
npm run build

# Build Backend
cd sales-savvy-be
./mvnw clean package

# Run JAR file
java -jar target/com.salesSavvy-0.0.1-SNAPSHOT.jar
```

---

## 📡 API Endpoints

### Authentication
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/auth/signup` | Register new user |
| POST | `/auth/signin` | Login user |
| GET | `/auth/test` | Test JWT token |

### Products
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/products` | Get all products | ❌ |
| GET | `/products/{id}` | Get product by ID | ❌ |
| POST | `/products` | Add new product | ✅ Admin |
| PUT | `/products/{id}` | Update product | ✅ Admin |
| DELETE | `/products/{id}` | Delete product | ✅ Admin |

### Cart
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/cart/items?username={username}` | Get user cart | ✅ |
| POST | `/cart/add` | Add item to cart | ✅ |
| PUT | `/cart/update` | Update cart item | ✅ |
| DELETE | `/cart/remove` | Remove item from cart | ✅ |
| DELETE | `/cart/clear` | Clear entire cart | ✅ |

### Orders
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/orders/create` | Create new order | ✅ |
| GET | `/orders` | Get all orders | ✅ Admin |
| GET | `/orders/user/{username}` | Get user orders | ✅ |
| PUT | `/orders/{razorpayOrderId}/status` | Update order status | ✅ Admin |

### Payment
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/payment/create-order` | Create Razorpay order | ✅ |
| POST | `/payment/verify` | Verify payment | ✅ |
| GET | `/payment/key` | Get Razorpay key | ❌ |

### Users
| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/users` | Get all users | ✅ Admin |
| GET | `/users/{username}` | Get user by username | ✅ |
| GET | `/users/profile` | Get current user profile | ✅ |
| PUT | `/users/{id}` | Update user | ✅ Admin |
| DELETE | `/users/{id}` | Delete user | ✅ Admin |

---

## 🔑 Default Admin Credentials

```
Username: admin
Password: StrongAdmin123
```

⚠️ **Important:** Change the admin password after first login!

---

## 📸 Screenshots

### Home Page
![Home Page](https://via.placeholder.com/800x400?text=Home+Page)

### Product Listing
![Products](https://via.placeholder.com/800x400?text=Product+Listing)

### Shopping Cart
![Cart](https://via.placeholder.com/800x400?text=Shopping+Cart)

### Admin Dashboard
![Admin Dashboard](https://via.placeholder.com/800x400?text=Admin+Dashboard)

---

## 🐛 Common Issues & Solutions

### Issue 1: MySQL Connection Error
**Solution:** Ensure MySQL service is running and credentials in `.env` are correct.

```bash
# Start MySQL service
sudo systemctl start mysql
```

### Issue 2: Port Already in Use
**Solution:** Change port in `application.properties` (Backend) or `vite.config.js` (Frontend)

### Issue 3: CORS Error
**Solution:** Verify `CorsConfig.java` allows your frontend URL:
```java
corsConfiguration.setAllowedOrigins(Arrays.asList("http://localhost:5173"));
```

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---


## 🙏 Acknowledgments

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [React Documentation](https://react.dev/)
- [Razorpay API Documentation](https://razorpay.com/docs/)
- [Bootstrap Icons](https://icons.getbootstrap.com/)

---


⭐ **If you found this project helpful, please give it a star!** ⭐
