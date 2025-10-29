# West Wales Utilities - Visitor Management System

A Spring Boot web application for managing visitor requests, locations, and check-ins with QR code functionality and role-based access control.

## Features

- **User Management**: Registration and authentication with role-based access (Admin, Staff, Visitor)
- **Location Management**: Manage multiple locations with different types
- **Request System**: Visitors can request visits to specific locations
- **QR Code Integration**: Generate and scan QR codes for check-ins
- **Admin Dashboard**: Comprehensive admin interface for managing the system
- **Staff Interface**: Staff can scan QR codes and manage visits
- **Security**: Spring Security with OAuth2 support (Google login)

## Prerequisites

Before running this application, ensure you have the following installed:

- **Java 17** or higher
- **MariaDB** database server
- **Git** (for cloning the repository)

## Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd West-Wales_Utilities
```

### 2. Install Prerequisites

#### Install Java 17 (macOS)
```bash
# Using Homebrew
brew install openjdk@17

# Verify installation
java -version
```

#### Install MariaDB (macOS)
```bash
# Using Homebrew
brew install mariadb

# Start MariaDB service
brew services start mariadb

# Secure installation (optional but recommended)
mysql_secure_installation
```

### 3. Database Setup

#### Start MariaDB
```bash
brew services start mariadb
```

#### Create Database and User
```bash
# Connect to MariaDB as root using "comsc"
mysql -u root -p

# In MariaDB prompt, run:
CREATE DATABASE IF NOT EXISTS client_project_db;
CREATE USER IF NOT EXISTS 'root'@'localhost' IDENTIFIED BY 'comsc';
GRANT ALL PRIVILEGES ON client_project_db.* TO 'root'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

## Running the Application

### Method 1: Using Gradle Wrapper (Recommended)

```bash
# Navigate to project directory
cd West-Wales_Utilities

# Make gradlew executable (if needed)
chmod +x gradlew

# Run the application
./gradlew bootRun
```

### Method 2: Build and Run JAR

```bash
# Build the project
./gradlew build

# Run the JAR file
java -jar build/libs/Client_Project-0.0.1-SNAPSHOT.jar
```

### Method 3: Using IDE

1. Import the project into your IDE (IntelliJ IDEA, Eclipse, VS Code)
2. Run the `ClientProjectApplication.java` main class

## Accessing the Application

Once the application starts successfully, you can access it at:

- **Main URL**: http://localhost:8080
- **Login Page**: http://localhost:8080/login
- **Welcome Page**: http://localhost:8080/welcome

## Default User Accounts

The application comes with pre-configured test users:

| Role | Email | Password |
|------|-------|----------|
| Admin | jane@doe.com | password123 |
| Staff | john@doe.com | password123 |
| Visitor | john@smith.com | password123 |

## Troubleshooting

### Port Already in Use Error

If you get "Port 8080 is already in use":

```bash
# Find the process using port 8080
lsof -ti:8080

# Kill the process (replace PID with actual process ID)
kill -9 <PID>

# Or change the port in application.properties
echo "server.port=8081" >> src/main/resources/application.properties
```

### Database Connection Issues

```bash
# Check if MariaDB is running
brew services list | grep mariadb

# Start MariaDB if not running
brew services start mariadb

# Test database connection
mysql -u root -p -e "SHOW DATABASES;"
```

### Java Version Issues

```bash
# Check Java version
java -version

# Set JAVA_HOME if needed (macOS)
export JAVA_HOME=$(/usr/libexec/java_home -v 17)
```

## Additional Commands

### Run Tests
```bash
./gradlew test
```

### Check Code Style
```bash
./gradlew checkstyleMain checkstyleTest
```

### Clean Build
```bash
./gradlew clean build
```

### View Application Logs
```bash
tail -f logs/application.log
```

## Project Structure

```
src/
├── main/
│   ├── java/uk/ac/cf/spring/client_project/
│   │   ├── ClientProjectApplication.java    # Main application class
│   │   ├── admin/                          # Admin controllers
│   │   ├── location/                       # Location management
│   │   ├── qrcode/                         # QR code functionality
│   │   ├── request/                        # Visit request handling
│   │   ├── security/                       # Security configuration
│   │   ├── staff/                          # Staff interface
│   │   ├── user/                           # User management
│   │   ├── visit/                          # Visit management
│   │   └── visitor/                        # Visitor interface
│   └── resources/
│       ├── application.properties          # Application configuration
│       ├── schema.sql                      # Database schema
│       ├── data.sql                        # Initial data
│       └── templates/                      # Thymeleaf templates
└── test/                                   # Test files
```

## Technology Stack

- **Backend**: Spring Boot 3.3.5, Spring Security, Spring Web MVC
- **Database**: MariaDB with JDBC
- **Frontend**: Thymeleaf templates, HTML, CSS, JavaScript
- **Build Tool**: Gradle 8.10.2
- **Java Version**: 17
- **QR Code**: Google ZXing library
- **Authentication**: Spring Security with OAuth2 support

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support and questions, please contact the development team or create an issue in the repository.
