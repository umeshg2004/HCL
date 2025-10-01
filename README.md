# User Management System

A full-featured user authentication and profile management system built with HTML, CSS, JavaScript, and PHP.

## Project Overview

This is a complete user management system that demonstrates full-stack web development skills with a modern technology stack. The application allows users to register, login, and manage their profile information with a clean, responsive interface.

### Key Features
- **User Registration**: Secure user registration with email validation
- **User Authentication**: Login/logout functionality with session management
- **Profile Management**: Store and update extended profile information (age, date of birth, contact info)
- **Secure Password Handling**: Passwords are securely hashed using PHP's `password_hash()` function
- **Token-based Sessions**: Secure session management using Redis
- **Responsive Design**: Works on desktop and mobile devices

## Technology Stack

### Frontend
- **HTML5**: Semantic markup for all pages
- **CSS3**: Responsive styling with custom design
- **JavaScript**: Client-side interactivity
- **jQuery**: AJAX requests and DOM manipulation

### Backend
- **PHP 7.4+**: Server-side logic and API endpoints
- **MySQL**: User authentication data (email, password)
- **MongoDB**: Extended profile data (age, DOB, contact info)
- **Redis**: Session token storage and management

### Database Usage Policy
- **MySQL**: Used exclusively for registration credentials (email, password)
- **MongoDB**: Used exclusively for extended user profile details (age, DOB, contact)
- **Redis**: Used exclusively for session management

## System Requirements

To run this application, you'll need:

1. **Web Server**: Apache, Nginx, or PHP's built-in server
2. **PHP 7.4 or higher** with the following extensions:
   - `pdo_mysql` (usually built-in)
   - `redis` (version 5.3.7 or higher)
   - `mongodb` (version 1.11.1 or higher)
3. **MySQL 5.7 or higher**
4. **MongoDB 4.0 or higher**
5. **Redis 5.0 or higher**

## Installation Guide

### Step 1: Install Required Software

#### Option A: Using XAMPP (Recommended for Windows)
1. Download and install XAMPP from [apachefriends.org](https://www.apachefriends.org/)
2. Start Apache, MySQL, and Redis services from XAMPP Control Panel

#### Option B: Manual Installation
1. **Install PHP**: Download from [php.net](https://www.php.net/downloads.php)
2. **Install MySQL**: Download from [mysql.com](https://dev.mysql.com/downloads/mysql/)
3. **Install MongoDB**: Download from [mongodb.com](https://www.mongodb.com/try/download/community)
4. **Install Redis**: Download from [redis.io](https://redis.io/download/)

### Step 2: Install PHP Extensions

#### Windows (XAMPP)
1. Download the appropriate DLL files for your PHP version:
   - Redis: [windows.php.net/downloads/pecl/releases/redis/](https://windows.php.net/downloads/pecl/releases/redis/)
   - MongoDB: [windows.php.net/downloads/pecl/releases/mongodb/](https://windows.php.net/downloads/pecl/releases/mongodb/)
2. Extract DLL files to your PHP extensions directory (usually `xampp/php/ext/`)
3. Add these lines to your `php.ini` file:
   ```ini
   extension=php_redis.dll
   extension=php_mongodb.dll
   ```
4. Restart your web server

#### macOS
```bash
# Using Homebrew
brew install php
pecl install redis mongodb
```

#### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install php php-mysql php-redis php-mongodb
```

### Step 3: Start Database Services

#### MySQL
```bash
# Windows (if installed as service)
net start MySQL

# macOS/Linux
sudo systemctl start mysql
# or
sudo service mysql start
```

#### MongoDB
```bash
# Windows (if installed as service)
net start MongoDB

# macOS/Linux
sudo systemctl start mongod
# or
sudo service mongod start
```

#### Redis
```bash
# Windows (if installed as service)
net start Redis

# macOS/Linux
sudo systemctl start redis
# or
redis-server
```

### Step 4: Set Up MySQL Database

1. Connect to MySQL:
   ```bash
   mysql -u root -p
   ```

2. Create the database and table using these SQL commands:
   ```sql
   -- Create database
   CREATE DATABASE IF NOT EXISTS user_auth;
   USE user_auth;
   
   -- Create users table
   CREATE TABLE IF NOT EXISTS users (
       id INT AUTO_INCREMENT PRIMARY KEY,
       email VARCHAR(255) UNIQUE NOT NULL,
       password VARCHAR(255) NOT NULL,
       created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   
   -- Create indexes for better performance
   CREATE INDEX idx_users_email ON users(email);
   
   -- Optional: Insert a test user (password is 'password' hashed)
   -- INSERT INTO users (email, password) VALUES 
   -- ('test@example.com', '$2y$10$Bx4a1Neb.DG8HglVb74q5Ou346/QM8rv5a7DB50HbS8vAJDQH8Ngu');
   ```

### Step 5: Deploy the Application

1. Place the project folder in your web server's document root:
   - **XAMPP**: `xampp/htdocs/user_auth_system/`
   - **Apache**: `/var/www/html/user_auth_system/`
   - **Nginx**: `/usr/share/nginx/html/user_auth_system/`

2. Or use PHP's built-in server:
   ```bash
   cd /path/to/project
   php -S localhost:8000
   ```

### Step 6: Configure Database Connections

Update the database connection settings in each PHP file:

#### php/login.php
```php
// Database configuration
$mysql_host = 'localhost';
$mysql_db = 'user_auth';
$mysql_user = 'root';
$mysql_pass = '';

// Redis configuration
$redis_host = '127.0.0.1';
$redis_port = 6379;
```

#### php/register.php
```php
// Database configuration
$mysql_host = 'localhost';
$mysql_db = 'user_auth';
$mysql_user = 'root';
$mysql_pass = '';
```

#### php/profile.php
```php
// Database configurations
$mysql_host = 'localhost';
$mysql_db = 'user_auth';
$mysql_user = 'root';
$mysql_pass = '';

// MongoDB configuration
$mongo_host = 'mongodb://localhost:27017';
$mongo_db = 'user_profiles';

// Redis configuration
$redis_host = '127.0.0.1';
$redis_port = 6379;
```

## Usage Instructions

1. **Access the Application**: Open your browser and navigate to `http://localhost/user_auth_system/` or `http://localhost:8000`

2. **Register a New User**: 
   - Click "Register" on the homepage
   - Enter your email and password
   - Click "Register"

3. **Login**: 
   - Click "Login" on the homepage
   - Enter your email and password
   - Click "Login"

4. **Manage Profile**: 
   - After logging in, you'll be redirected to the profile page
   - Enter your profile information (age, date of birth, contact number)
   - Click "Update Profile"

5. **Logout**: 
   - Click "Logout" on the profile page

## Project Structure

```
user_auth_system/
├── css/
│   └── style.css          # All styling
├── js/
│   ├── login.js           # Login page functionality
│   ├── profile.js         # Profile page functionality
│   └── register.js        # Registration page functionality
├── php/
│   ├── login.php          # User authentication API
│   ├── profile.php        # Profile management API
│   └── register.php       # User registration API
├── index.html             # Homepage
├── login.html             # Login page
├── profile.html           # Profile management page
├── register.html          # Registration page
└── README.md              # This file
```

## API Endpoints

### User Registration
- **URL**: `/php/register.php`
- **Method**: `POST`
- **Data**: `{ "email": "user@example.com", "password": "userpassword" }`
- **Response**: `{ "success": true/false, "message": "Description" }`

### User Login
- **URL**: `/php/login.php`
- **Method**: `POST`
- **Data**: `{ "email": "user@example.com", "password": "userpassword" }`
- **Response**: `{ "success": true/false, "message": "Description", "token": "session_token" }`

### Get Profile
- **URL**: `/php/profile.php`
- **Method**: `GET`
- **Data**: `{ "token": "session_token" }`
- **Response**: `{ "success": true, "data": { "age": 25, "dob": "1995-01-01", "contact": "123-456-7890" } }`

### Update Profile
- **URL**: `/php/profile.php`
- **Method**: `POST`
- **Data**: `{ "token": "session_token", "age": 25, "dob": "1995-01-01", "contact": "123-456-7890" }`
- **Response**: `{ "success": true/false, "message": "Description" }`

## Security Features

1. **Password Hashing**: All passwords are securely hashed using PHP's `password_hash()` function
2. **Session Management**: Token-based sessions stored in Redis with expiration
3. **Input Validation**: Server-side validation of all user inputs
4. **SQL Injection Prevention**: Prepared statements for all database queries
5. **XSS Prevention**: Proper output escaping and Content Security Policy headers
6. **CORS Protection**: Controlled cross-origin resource sharing

## Troubleshooting

### Common Issues

#### 1. "Redis extension not loaded"
- Ensure the Redis extension is installed and enabled in php.ini
- Restart your web server after making changes

#### 2. "MongoDB extension not loaded"
- Ensure the MongoDB extension is installed and enabled in php.ini
- Restart your web server after making changes

#### 3. "MongoDB error: No suitable servers found"
- Make sure MongoDB is installed and running
- Verify MongoDB is listening on `localhost:27017`
- Check firewall settings

#### 4. "Database error: Access denied"
- Verify MySQL username and password in PHP files
- Ensure the MySQL user has proper permissions

#### 5. "Invalid session token"
- This usually means the session has expired (1 hour)
- Log in again to get a new session token

### Testing Without All Services

The application is designed to work partially if some services are unavailable:
- **Without MongoDB**: Authentication works, but profile management is unavailable
- **Without Redis**: Sessions won't work properly
- **Without MySQL**: Registration and authentication won't work

## Development Notes

### Code Quality
- All PHP files include proper error handling
- Consistent coding style throughout the project
- Meaningful variable and function names
- Comprehensive comments explaining complex logic

### IDE Support
- The project includes stubs for better IDE support
- All classes and methods are properly documented
- Type hints are provided where applicable

## Author
[Your Name]

## License
MIT License

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.