# 🛒 MyStore - Enterprise E-Commerce Platform

A full-featured, production-ready e-commerce platform built with Java Servlets, JSP, MySQL, and modern frontend technologies. MyStore provides a comprehensive shopping experience with advanced features including image upload, search functionality, real-time logging, and role-based access control.

---

## 👥 Team Members

- **MAYANK SOLANKI**
- **MONU KUMAR**
- **BHUPESH DUBEY**

---

## ✨ Features

### 🔐 Authentication & Authorization
- Secure user registration with comprehensive validation
- SHA-256 password hashing
- Role-based access control (Admin, Seller, Buyer)
- Session management with automatic redirection
- Admin registration requires secret key: `SuperSecret123`
- Client-side and server-side validation

### 👔 Admin Module
- **Dashboard**: Real-time platform statistics
  - Total users, products, and orders
  - Platform-wide analytics
- **User Management**: 
  - View all users (excluding admins)
  - Delete users with cascade operations
- **Product Management**: 
  - Monitor all products with images
  - Soft delete products
- **Order Management**: 
  - Update order processing status
  - Track payment status
  - View detailed order information

### 🏪 Seller Module
- **Dashboard**: Business overview
  - Product count
  - Low stock alerts (< 5 units)
  - Quick access to key features
- **Product Management**
  - Add new products with image upload
  - Edit product details with image update
  - Soft delete products
  - Real-time stock monitoring
  - Image preview in product listings
- **Inventory Overview**: 
  - Visual stock monitoring with Chart.js
  - Low stock alerts
  - Color-coded stock levels
- **Order History**: Track all items sold with detailed breakdown
- **Sales Performance Analytics**
  - Monthly sales trends (last 12 months)
  - Product-wise analytics
  - Top-selling products
  - Revenue tracking

### 🛒 Buyer Module
- **Dashboard**: Personalized shopping experience with sidebar navigation
- **Product Browsing**: 
  - Modern grid layout with Tailwind CSS
  - Live search with autocomplete suggestions
  - Product images with fallback placeholders
  - Stock status indicators
  - Animated search bar (desktop)
  - Responsive mobile design
- **Product Details Page**:
  - Full-size product images
  - Complete product descriptions
  - Stock availability
  - Add to cart with quantity selection
  - Wishlist integration
- **Shopping Cart**:
  - Advanced cart with Tailwind CSS
  - Stock validation
  - Real-time quantity updates
  - Remove items
  - Order summary with totals
  - Empty cart messaging
- **Wishlist**: 
  - Save favorite products
  - Add to cart from wishlist
  - Remove items
- **Checkout System**:
  - Multi-step checkout process
  - Shipping address management
  - Multiple payment options (COD, Card, UPI)
  - Payment validation
  - Order confirmation
- **Order History**: 
  - Track past purchases
  - Payment status tracking
  - Processing stage tracking
  - View detailed invoices
- **Profile Management**: 
  - Update personal information
  - Manage shipping addresses
  - Sidebar navigation

---

## 🛠️ Technology Stack

### Backend
- **Java Servlets** (javax.servlet 4.0.1)
- **JSP** with JSTL
- **JDBC** for database operations
- **HikariCP 5.1.0** for connection pooling
- **SHA-256** for password hashing
- **Gson 2.10.1** for JSON processing
- **SLF4J + Logback** for logging

### Frontend
- **Bootstrap 5** for responsive UI
- **Tailwind CSS 3** for modern styling
- **jQuery 3.6.0** for AJAX operations
- **Chart.js** for data visualization
- **Font Awesome 6** for icons
- **Google Fonts** (Poppins, Inter)

### Database
- **MySQL 8.0+**

### Build & Server
- **Apache Maven**
- **Apache Tomcat 9+**

---

## 📦 Prerequisites

Before you begin, ensure you have:

- **Java JDK 11** or higher
- **MySQL 8.0** or higher
- **Apache Tomcat 9+**
- **Maven** (for dependency management)
- **IDE** (IntelliJ IDEA or Eclipse recommended)

---

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd ecommerce-enterprise
```

### Step 2: Database Setup

1. Open MySQL and create the database:

```sql
CREATE DATABASE ecommerce_db;
```

2. Run the schema script:

```bash
mysql -u root -p ecommerce_db < sql/schema.sql
```

**Note**: The schema includes:
- `users` table with shipping information fields
- `products` table with `image` and `is_active` columns
- `orders` table with `status` and `process` tracking
- `order_items`, `wishlist`, and `cart` tables

### Step 3: Configure Database Connection

Edit `src/main/resources/application.properties`:

```properties
db.url=jdbc:mysql://localhost:3306/ecommerce_db?useSSL=false&serverTimezone=UTC&allowPublicKeyRetrieval=true
db.user=your_mysql_username
db.pass=your_mysql_password
```

### Step 4: Create Product Images Directory

Create the directory for product images in your webapp:

```bash
mkdir -p src/main/webapp/product_images
```

Add a default product image:
- Save a default image as `src/main/webapp/product_images/default.jpg`

### Step 5: Import Project to IDE

#### For IntelliJ IDEA:

1. **File → Open** → Select project folder
2. Right-click on `pom.xml` → **Maven → Reload Project**
3. **File → Project Structure** → Set JDK to 11+
4. Wait for Maven dependencies to download

#### For Eclipse:

1. **File → Import → Existing Maven Project**
2. Select project folder
3. Right-click project → **Maven → Update Project**

### Step 6: Configure Tomcat Server

#### IntelliJ IDEA:

1. **Run → Edit Configurations**
2. Click **+** → **Tomcat Server → Local**
3. Configure Tomcat home directory
4. **Deployment** tab → Click **+** → **Artifact** → Select WAR exploded
5. Set Application context to `/ecommerce-enterprise`
6. Click **Apply** and **OK**

#### Eclipse:

1. **Window → Preferences → Server → Runtime Environments**
2. Click **Add** → Select **Apache Tomcat v9.0**
3. Browse to Tomcat installation directory
4. Right-click project → **Run As → Run on Server**

### Step 7: Configure Logging (Optional)

The application uses Logback for logging. Logs are stored in:
- Console output (during development)
- `logs/ecommerce.log` (in production)

You can modify `src/main/resources/logback.xml` to adjust logging levels.

### Step 8: Run the Application

1. Start Tomcat server from your IDE
2. Open browser and navigate to:

```
http://localhost:8080/ecommerce-enterprise/
```

3. You should see the MyStore landing page

### Step 9: Create Admin Account

1. Navigate to registration page
2. Fill in all required fields
3. Select **Admin** role
4. Enter admin secret key: `SuperSecret123`
5. Complete registration

---

## 📁 Project Structure

```
ecommerce-enterprise/
├── sql/
│   ├── schema.sql              # Database schema with all tables
│   └── seed.sql                # Sample data (optional)
├── src/main/
│   ├── java/com/ecomm/
│   │   ├── dao/                # Data Access Objects
│   │   │   ├── CartDAO.java
│   │   │   ├── DBPool.java    # HikariCP connection pooling
│   │   │   ├── OrderDAO.java  # Transaction management
│   │   │   ├── ProductDAO.java # Image & search support
│   │   │   ├── UserDAO.java
│   │   │   └── WishlistDAO.java
│   │   ├── exception/          # Custom Exceptions
│   │   │   ├── InsufficientStockException.java
│   │   │   ├── InvalidUserInputException.java
│   │   │   └── PaymentProcessingException.java
│   │   ├── filter/             # Servlet Filters
│   │   │   └── AuthFilter.java # Role-based security
│   │   ├── model/              # Domain Models
│   │   │   ├── CartItem.java
│   │   │   ├── Order.java
│   │   │   ├── Product.java   # Includes image field
│   │   │   └── User.java
│   │   ├── service/            # Business Logic Layer
│   │   │   ├── CartService.java
│   │   │   ├── CheckoutService.java
│   │   │   └── OrderService.java
│   │   ├── servlet/            # HTTP Servlets
│   │   │   ├── AdminServlet.java
│   │   │   ├── AuthServlet.java
│   │   │   ├── BuyerServlet.java
│   │   │   ├── CartServlet.java
│   │   │   ├── CheckoutServlet.java
│   │   │   ├── InventoryServlet.java
│   │   │   ├── LogoutServlet.java
│   │   │   ├── OrderServlet.java
│   │   │   ├── PaymentServlet.java
│   │   │   ├── PaymentSuccessServlet.java
│   │   │   ├── ProductServlet.java # Image upload support
│   │   │   ├── ProfileServlet.java
│   │   │   ├── RegisterServlet.java
│   │   │   ├── SalesServlet.java
│   │   │   ├── SellerServlet.java
│   │   │   └── WishlistServlet.java
│   │   └── util/
│   │       ├── PasswordUtil.java
│   │       └── ValidationUtil.java # Input validation
│   ├── resources/
│   │   ├── application.properties
│   │   └── logback.xml         # Logging configuration
│   └── webapp/
│       ├── WEB-INF/
│       │   ├── jsp/            # JSP Pages
│       │   │   ├── admin/      # Admin pages
│       │   │   │   ├── dashboard.jsp
│       │   │   │   ├── orders.jsp
│       │   │   │   ├── products.jsp
│       │   │   │   └── users.jsp
│       │   │   ├── buyer/      # Buyer pages
│       │   │   │   ├── dashboard.jsp # With sidebar
│       │   │   │   ├── profile.jsp
│       │   │   │   └── wishlist.jsp
│       │   │   ├── order/      # Order pages
│       │   │   │   ├── Checkout.jsp
│       │   │   │   ├── history.jsp
│       │   │   │   ├── invoice.jsp
│       │   │   │   ├── payment.jsp
│       │   │   │   └── success.jsp
│       │   │   ├── product/    # Product pages
│       │   │   │   ├── list.jsp # With search
│       │   │   │   └── product_details.jsp
│       │   │   └── seller/     # Seller pages
│       │   │       ├── dashboard.jsp
│       │   │       ├── inventory.jsp
│       │   │       ├── orders.jsp
│       │   │       ├── products.jsp # With image upload
│       │   │       └── salesPerformance.jsp
│       │   └── web.xml
│       ├── product_images/     # Product images directory
│       │   └── default.jpg
│       ├── cart.jsp            # Advanced cart with Tailwind
│       ├── error.jsp
│       ├── index.jsp
│       ├── login.jsp
│       └── register.jsp        # With validation
├── logs/                       # Application logs
│   └── ecommerce.log
├── pom.xml
└── README.md
```

---

## 🎯 User Roles & Access

### Admin Access
- **Registration**: Requires secret key `SuperSecret123`
- **URL**: `/admin/dashboard`
- **Features**:
  - View all users (excluding admins)
  - View all products with images
  - Delete users and products
  - Update order status and processing stage
  - Platform-wide analytics

### Seller Access
- **Registration**: Select "Seller" role during signup
- **URL**: `/seller/dashboard`
- **Features**:
  - Product management with image upload
  - Inventory monitoring with charts
  - Sales history and analytics
  - Monthly performance reports
  - Low stock alerts

### Buyer Access
- **Registration**: Select "Buyer" role during signup
- **URL**: `/buyer/dashboard`
- **Features**:
  - Browse products with search
  - View product details
  - Shopping cart management
  - Wishlist functionality
  - Order history with invoices
  - Profile management

---

## 🔍 Key Features Explained

### 1. Image Upload System

**Product Images**:
- Sellers can upload product images during creation
- Images are stored in `webapp/product_images/`
- Supported formats: JPG, PNG, GIF
- Maximum file size: 10MB
- Default fallback image for products without images

### 2. Advanced Search Functionality

**Features**:
- Live search with autocomplete
- AJAX-powered suggestions
- Animated search bar (desktop only)
- Mobile-responsive search
- Product name matching
- Instant results display

### 3. Comprehensive Validation

**Client-Side Validation** (JavaScript):
- Real-time field validation
- Password strength checking
- Email format validation
- Phone number validation (10 digits)
- Pincode validation (6 digits)
- Immediate user feedback

### 4. Transaction Management

**Order Processing**:
- ACID-compliant transactions
- Atomic operations for:
  - Order creation
  - Inventory reduction
  - Payment processing
- Rollback on failure
- Database integrity maintained

### 5. Logging System

**Logback Configuration**:
- Console logging for development
- File logging for production
- Log rotation (daily)
- 30-day log retention
- DEBUG level for application code
- INFO level for libraries

**Key UI Components**:
- Animated search bar with smooth transitions
- Product cards with hover effects
- Stock indicators with color coding
- Loading states and error messages
- Toast notifications (future enhancement)

---

## 🔌 API Endpoints

### Authentication
- `POST /login` - User login
- `POST /register` - User registration with validation
- `GET /logout` - User logout

### Admin
- `GET /admin/dashboard` - Admin dashboard with stats
- `GET /admin/users` - View all users
- `POST /admin/users/action` - User management (delete)
- `GET /admin/products` - View all products
- `POST /admin/products/action` - Product management (delete)
- `GET /admin/orders` - View all orders
- `POST /admin/orders/action` - Update order status/process

### Seller
- `GET /seller/dashboard` - Seller dashboard
- `GET /seller/products` - Manage products
- `POST /product/action` - Add/Edit/Delete products with images
- `GET /seller/orders` - Sales history
- `GET /seller/inventory` - Inventory overview with chart
- `GET /seller/salesPerformance` - Sales analytics

### Buyer
- `GET /buyer/dashboard` - Buyer dashboard with sidebar
- `GET /buyer/profile` - View/edit profile
- `POST /buyer/profile` - Update profile
- `GET /product/list` - Browse products with search
- `GET /product/search` - Search products (AJAX)
- `GET /product/suggest` - Autocomplete suggestions (AJAX)
- `GET /product/product_details` - View product details
- `POST /cart/add` - Add to cart
- `POST /cart/remove` - Remove from cart
- `GET /cart` - View cart
- `POST /buyer/wishlist` - Add/remove wishlist items
- `GET /buyer/wishlist` - View wishlist
- `GET /order/Checkout` - Checkout page
- `POST /order/Checkout` - Submit shipping info
- `GET /order/payment` - Payment page
- `POST /order/payment` - Process payment
- `GET /order/success` - Payment success page
- `GET /order/history` - Order history
- `GET /order/invoice?id={orderId}` - View invoice PDF

---

## 🔒 Security Features

### Authentication & Authorization
- **Password Hashing**: SHA-256 encryption
- **Session Management**: Secure HttpSession with timeout
- **Role-Based Access Control**: Servlet filter enforcement
- **Admin Protection**: Secret key requirement


### Data Validation
- **Client-Side**: JavaScript validation for immediate feedback
- **Server-Side**: Comprehensive validation in ValidationUtil

### Error Handling
- **Custom Error Page**: User-friendly error messages
- **Exception Logging**: Detailed logs for debugging
- **Transaction Rollback**: Data integrity on failures
- **Graceful Degradation**: Fallback for missing images

---


## 🚀 Future Enhancements

- [ ] Email notifications
- [ ] Product reviews and ratings
- [ ] Advanced search and filters
- [ ] Payment gateway integration (Razorpay, Stripe)
- [ ] Multi-language support
- [ ] Product image upload
- [ ] Coupon and discount system
- [ ] Real-time chat support


---

## 📄 License

This project is licensed under the MIT License.

---


## 📞 Support & Contact

For issues, questions, or contribution
- **Email**: support@mystore.com

---




**Built with ❤️ by Team MyStore**

