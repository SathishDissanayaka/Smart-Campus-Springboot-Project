# Smart Campus Operations Hub

A comprehensive full-stack web application designed to streamline campus operations, resource management, and student services. Built with modern technologies including Spring Boot, React, and PostgreSQL.

**Status**: Active Development (April 2026)  
**Version**: 0.0.1-SNAPSHOT

---

## Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
  - [Docker Setup (Recommended)](#docker-setup-recommended)
  - [Manual Setup](#manual-setup)
- [Development](#development)
- [API Documentation](#api-documentation)
- [Database](#database)
- [Configuration](#configuration)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Team & Contribution](#team--contribution)

---

## Overview

The Smart Campus Operations Hub is a unified platform that enables:

- **Students** to book facilities, check timetables, manage appeals, and track notifications
- **Faculty** to manage schedules and resource allocation
- **Administrators** to oversee campus operations, approve requests, and generate analytics
- **Campus** to efficiently allocate resources and track utilization

The system integrates modern authentication mechanisms (OAuth, OTP), real-time notifications, file uploads, and comprehensive analytics capabilities.

---

## Key Features

### 🔐 Authentication & Security
- **OAuth 2.0 Integration**: Google/Microsoft SSO support
- **Two-Factor Authentication (2FA)**: OTP-based verification
- **JWT Token Management**: Secure API endpoints
- **Role-Based Access Control (RBAC)**: Admin, Staff, Student roles

### 📅 Booking & Reservations
- **Facility Booking System**: Reserve venues, equipment, and resources
- **Slot Management**: Time-based availability and conflict prevention
- **Admin Approval Workflow**: Review and approve bookings
- **Booking History & Analytics**: Track usage patterns

### 👥 User Management
- **Profile Management**: Update personal and academic information
- **User Directory**: Search and view campus members
- **Account Settings**: Preferences and notification controls

### 📊 Timetable & Schedule Management
- **Smart Timetable Engine**: Display student schedules
- **Conflict Detection**: Prevent schedule overlaps
- **Class Updates**: Real-time schedule modifications
- **Calendar Integration**: View in calendar format

### 🎫 Ticket Management System
- **Issue Reporting**: Submit technical and operational tickets
- **Ticket Tracking**: Monitor resolution status
- **Priority-Based Queue**: Urgent issues handled first
- **Automated Notifications**: Status updates to reporters

### 🔔 Notification System
- **Real-Time Alerts**: Instant notifications for important events
- **Multi-Channel Delivery**: Email and in-app notifications
- **Smart Filtering**: Customizable notification preferences
- **Email Templates**: Professionally formatted messages

### 🎯 Geofencing & Check-In
- **QR Code Check-In**: Generate and scan QR codes for events
- **Geofencing**: Location-based check-in verification
- **Attendance Tracking**: Automatic attendance recording

### 📈 Analytics & Reporting
- **Usage Analytics**: Track resource utilization
- **Performance Dashboards**: Visual insights for admins
- **Custom Reports**: Generate ad-hoc reports
- **Data Export**: Download analytics in multiple formats

### 📝 Appeals & Requests
- **Suspension Appeals**: Submit and track appeal requests
- **Admin Review Interface**: Process appeals with comments
- **Appeal History**: View past submissions and decisions

### 📁 File Management
- **File Upload/Download**: Support for various document types
- **Image Thumbnails**: Auto-generated preview images
- **Organized Storage**: Categorized upload folders
- **Access Control**: Secure file permissions

---

## Technology Stack

### Backend
- **Framework**: Spring Boot 4.0.4
- **Java Version**: 21
- **Build Tool**: Maven
- **Database**: PostgreSQL 15
- **Authentication**: Spring Security, JWT (JJWT 0.11.5)
- **API Documentation**: Springdoc OpenAPI/Swagger
- **Email**: Spring Mail (MailDev for testing)
- **ORM**: Spring Data JPA, Hibernate
- **Validation**: Bean Validation (Jakarta)

### Frontend
- **Framework**: React 19.2.4
- **Build Tool**: Vite 8.0.1
- **Styling**: Tailwind CSS 4.2.2
- **HTTP Client**: Axios 1.12.2
- **Routing**: React Router DOM 7.9.6
- **Authentication**: @react-oauth/google
- **QR Code**: qrcode.react 4.2.0
- **Notifications**: react-toastify 11.0.5
- **PDF Generation**: jsPDF 4.2.1
- **Screenshot**: html2canvas 1.4.1

### Infrastructure
- **Containerization**: Docker & Docker Compose
- **Database Persistence**: PostgreSQL with named volumes
- **Email Testing**: MailDev
- **Orchestration**: Docker Compose

---

## Project Structure

```
paf_assignment/
├── backend/
│   └── api/
│       ├── src/main/java/com/sliitreserve/api/
│       │   ├── controllers/         # REST API endpoints
│       │   │   ├── admin/
│       │   │   ├── auth/
│       │   │   ├── bookings/
│       │   │   ├── facilities/
│       │   │   ├── notifications/
│       │   │   ├── tickets/
│       │   │   ├── users/
│       │   │   ├── appeals/
│       │   │   └── analytics/
│       │   ├── models/              # JPA entities
│       │   ├── repositories/        # Data access layer
│       │   ├── services/            # Business logic
│       │   ├── dto/                 # Data Transfer Objects
│       │   ├── security/            # JWT & Auth config
│       │   └── config/              # Application configuration
│       ├── src/main/resources/
│       │   ├── application.yaml    # Main config
│       │   ├── db/migration/       # Flyway/Liquibase migrations
│       │   └── templates/          # Email templates
│       ├── pom.xml                 # Maven dependencies
│       ├── mvnw & mvnw.cmd         # Maven wrapper
│       └── Dockerfile              # Container image
│
├── frontend/
│   ├── src/
│   │   ├── components/             # Reusable UI components
│   │   ├── pages/                  # Page components
│   │   ├── features/               # Feature modules
│   │   │   ├── bookings/
│   │   │   ├── auth/
│   │   │   ├── timetable/
│   │   │   ├── tickets/
│   │   │   ├── appeals/
│   │   │   └── analytics/
│   │   ├── services/               # API service clients
│   │   ├── contexts/               # React Context providers
│   │   ├── utils/                  # Utility functions
│   │   ├── assets/                 # Images, icons
│   │   ├── App.jsx                 # Main App component
│   │   └── main.jsx                # Entry point
│   ├── public/                     # Static assets
│   ├── package.json                # npm dependencies
│   ├── vite.config.js              # Vite configuration
│   ├── tailwind.config.js          # Tailwind CSS config
│   ├── eslint.config.js            # ESLint rules
│   ├── Dockerfile                  # Container image
│   └── nginx.conf                  # Nginx server config
│
├── infra/
│   └── docker-compose.yml          # Multi-service orchestration
│
├── docs/
│   └── architecture/               # System architecture docs
│
├── uploads/                        # File storage
│   ├── original/                   # Original uploaded files
│   └── thumbnails/                 # Generated thumbnails
│
└── [Documentation Files]           # Setup & implementation guides
    ├── QUICK_START_CHECKLIST.md
    ├── DB_SETUP_AND_TESTING_GUIDE.md
    ├── OAUTH_SETUP_GUIDE.md
    ├── OTP_CONFIGURATION_GUIDE.md
    ├── TESTING_PLAN.md
    └── ...
```

---

## Prerequisites

### System Requirements
- **Docker & Docker Compose**: For containerized setup (recommended)
  - Docker Desktop 4.0+
  - Docker Compose 1.29+

OR for manual setup:
- **Java 21**: [Download from Oracle](https://www.oracle.com/java/technologies/downloads/#java21)
- **Maven 3.8+**: [Download here](https://maven.apache.org/download.cgi)
- **Node.js 18+**: [Download from nodejs.org](https://nodejs.org/)
- **npm 8+**: Comes with Node.js
- **PostgreSQL 15**: [Download here](https://www.postgresql.org/download/)

### Accounts & Keys
- **Google OAuth Credentials**: [Create at Google Cloud Console](https://console.cloud.google.com/)
- **Microsoft OAuth Credentials** (optional): [Create at Azure Portal](https://portal.azure.com/)

---

## Quick Start

### Docker Setup (Recommended)

The fastest way to get everything running with a single command.

#### 1. Start All Services

```bash
# Navigate to project root
cd paf_assignment

# Start all services (frontend, backend, database, mail)
cd infra
docker compose up --build -d
```

This starts:
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8080
- **Swagger UI**: http://localhost:8080/swagger-ui.html
- **Mail UI**: http://localhost:1080
- **PostgreSQL**: localhost:5432

⏳ **Wait 20-40 seconds** for the backend to initialize and run database migrations.

#### 2. Access the Application

- Open your browser to **http://localhost:5173**
- Use test credentials (see [Testing](#testing) section)

#### 3. Stop All Services

```bash
cd infra
docker compose down
```

#### 4. Fresh Database Reset

To start with a clean database:

```bash
cd infra
docker compose down
docker volume rm -f infra_postgres_data
docker compose up --build -d
```

### Manual Setup

If you prefer running services locally without Docker:

#### 1. Database Setup

```bash
# Ensure PostgreSQL is running
# Create database and user
psql -U postgres

psql> CREATE DATABASE smartcampus;
psql> CREATE USER smartcampus WITH PASSWORD 'smartcampus';
psql> ALTER ROLE smartcampus WITH CREATEDB;
psql> GRANT ALL PRIVILEGES ON DATABASE smartcampus TO smartcampus;
psql> \q
```

#### 2. Backend Setup

```bash
cd backend/api

# Build the project
mvn clean install

# Run the application
mvn spring-boot:run

# Backend will start on http://localhost:8080
# Swagger docs available at http://localhost:8080/swagger-ui.html
```

#### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev

# Frontend will start on http://localhost:5173
```

#### 4. Email Testing (Optional)

For development email testing:

```bash
# Using Docker for MailDev only
docker run -d -p 1080:1080 -p 1025:1025 --name maildev maildev/maildev:latest

# Mail UI will be available at http://localhost:1080
```

---

## Development

### Backend Development

#### Running in IDE

1. Open `backend/api` as a Maven project in your IDE (IntelliJ, VS Code, Eclipse)
2. Create a run configuration for `ApiApplication` main class
3. Set JVM arguments if needed: `-Xmx512m`
4. Run the configuration

#### Build Commands

```bash
cd backend/api

# Clean and build
mvn clean install

# Run tests
mvn test

# Run with hot reload (requires spring-boot-devtools)
mvn spring-boot:run

# Build WAR for deployment
mvn package -DskipTests
```

#### Code Structure

- **Controllers**: REST endpoints in `com.sliitreserve.api.controllers.*`
- **Services**: Business logic in `com.sliitreserve.api.services.*`
- **Models**: JPA entities in `com.sliitreserve.api.models.*`
- **DTOs**: Data transfer objects in `com.sliitreserve.api.dto.*`
- **Repositories**: Spring Data JPA repositories

#### Hot Reload Development

For faster development cycles:

```bash
# Terminal 1: Start backend with devtools enabled
cd backend/api
mvn clean spring-boot:run

# Make code changes - they'll auto-reload
# Alternatively, in IDE, use "Build > Rebuild Project"
```

### Frontend Development

```bash
cd frontend

# Start dev server with hot reload
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Run linter
npm run lint

# Fix linting issues
npm run lint -- --fix
```

#### Hot Reload Features

- **Automatic refresh** on code changes
- **Preserved app state** during updates
- **Error overlay** for quick debugging

#### Styling

The project uses **Tailwind CSS** with a custom color scheme:

```jsx
// Example component styling
<div className="bg-gradient-to-r from-blue-600 to-blue-800 text-white p-4 rounded-lg">
  Content here
</div>
```

### IDE Configuration

#### VS Code Extensions (Recommended)

- **Extension Pack for Java**: `ms-vscode.extension-pack-for-java`
- **Prettier**: `esbenp.prettier-vscode`
- **Tailwind CSS IntelliSense**: `bradlc.vscode-tailwindcss`
- **REST Client**: `humao.rest-client`
- **Thunder Client**: API testing

#### IntelliJ IDEA

- Built-in Spring Boot support
- Automatic Gradle/Maven recognition
- React plugin for frontend development

---

## API Documentation

### Swagger UI

Once the backend is running, access interactive API documentation:

```
http://localhost:8080/swagger-ui.html
```

### Main API Endpoints

#### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login with credentials
- `POST /api/auth/oauth/google` - Google OAuth callback
- `POST /api/auth/refresh` - Refresh JWT token

#### Bookings
- `GET /api/bookings` - List user's bookings
- `POST /api/bookings` - Create new booking
- `PUT /api/bookings/{id}` - Update booking
- `DELETE /api/bookings/{id}` - Cancel booking
- `GET /api/bookings/admin/pending` - List pending approvals (admin)

#### Facilities
- `GET /api/facilities` - List all facilities
- `GET /api/facilities/{id}` - Get facility details
- `GET /api/facilities/{id}/availability` - Check availability

#### Tickets
- `GET /api/tickets` - List tickets
- `POST /api/tickets` - Create new ticket
- `PUT /api/tickets/{id}` - Update ticket
- `GET /api/tickets/admin/queue` - View ticket queue (admin)

#### Users
- `GET /api/users/profile` - Get current user profile
- `PUT /api/users/profile` - Update profile
- `GET /api/users/{id}` - Get user details

#### Analytics
- `GET /api/analytics/dashboard` - Dashboard metrics
- `GET /api/analytics/bookings/usage` - Booking usage stats
- `GET /api/analytics/facilities/utilization` - Facility utilization

See [Swagger UI](#swagger-ui) for complete endpoint specifications.

---

## Database

### Schema Overview

#### Core Entities
- **Users**: Student, Staff, Admin accounts
- **Facilities**: Bookable resources (rooms, equipment, etc.)
- **Bookings**: Facility reservations
- **Tickets**: Support/issue tracking
- **Notifications**: User notifications
- **Files**: Uploaded documents and images

#### Key Relationships
```
User (1) ──── (M) Booking
User (1) ──── (M) Ticket
User (1) ──── (M) Appeal
Facility (1) ──── (M) Booking
Booking (1) ──── (M) Notification
```

### Database Migrations

Migrations are automatically applied on backend startup using Flyway:

```
src/main/resources/db/migration/
├── V1__initial_schema.sql
├── V2__add_oauth_fields.sql
├── V3__add_notifications.sql
└── ...
```

To manually apply migrations:

```bash
# Using the backend (auto-executed)
mvn spring-boot:run

# View migration status
SELECT * FROM flyway_schema_history;
```

### Backup & Restore

#### Backup Database

```bash
# Docker container
docker exec smartcampus-postgres pg_dump -U smartcampus smartcampus > backup.sql

# Local PostgreSQL
pg_dump -U smartcampus -d smartcampus > backup.sql
```

#### Restore Database

```bash
# Docker container
docker exec -i smartcampus-postgres psql -U smartcampus smartcampus < backup.sql

# Local PostgreSQL
psql -U smartcampus -d smartcampus < backup.sql
```

---

## Configuration

### Backend Configuration

Edit `backend/api/src/main/resources/application.yaml`:

```yaml
# Server Configuration
server:
  port: 8080
  servlet:
    context-path: /api

# Database Configuration
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/smartcampus
    username: smartcampus
    password: smartcampus
    driver-class-name: org.postgresql.Driver

  jpa:
    hibernate:
      ddl-auto: validate  # or update for development
    show-sql: false
    properties:
      hibernate.dialect: org.hibernate.dialect.PostgreSQLDialect

# JWT Configuration
app:
  jwt:
    secret: your-secret-key-here-min-256-chars-recommended
    expiration: 86400000  # 24 hours in ms

# OAuth Configuration
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${GOOGLE_CLIENT_ID}
            client-secret: ${GOOGLE_CLIENT_SECRET}

# Mail Configuration
  mail:
    host: localhost
    port: 1025
    username: user
    password: pass
    properties:
      mail.smtp.auth: false
      mail.smtp.starttls.enable: false
```

### Environment Variables

```bash
# .env file (create in project root)
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
MICROSOFT_CLIENT_ID=your-microsoft-client-id  # Optional
MICROSOFT_CLIENT_SECRET=your-microsoft-client-secret  # Optional
JWT_SECRET=your-long-secret-key-min-256-chars
DB_PASSWORD=smartcampus
```

### Frontend Configuration

Edit `frontend/vite.config.js`:

```javascript
export default defineConfig({
  plugins: [react()],
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '/api')
      }
    }
  }
})
```

---

## Testing

### Test Credentials

Once the application is running, use these test accounts:

| Email | Password | Role | Purpose |
|-------|----------|------|---------|
| `student@smartcampus.edu` | `student123` | STUDENT | Test student features |
| `staff@smartcampus.edu` | `staff123` | STAFF | Test staff features |
| `admin@smartcampus.edu` | `admin123` | ADMIN | Test admin features |

### Testing Endpoints

#### With cURL

```bash
# Get auth token
curl -X POST http://localhost:8080/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"student@smartcampus.edu","password":"student123"}'

# Use token in requests
curl -X GET http://localhost:8080/api/bookings \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

#### With Postman

1. Import `Smart_Campus_API.postman_collection.json`
2. Set `{{base_url}}` to `http://localhost:8080`
3. Login to get JWT token
4. Use token in subsequent requests

#### With REST Client (VS Code)

Create `test.http` file:

```http
### Login
POST http://localhost:8080/api/auth/login
Content-Type: application/json

{
  "email": "student@smartcampus.edu",
  "password": "student123"
}

### Get Bookings
GET http://localhost:8080/api/bookings
Authorization: Bearer {{token}}
```

### Running Tests

```bash
# Backend unit tests
cd backend/api
mvn test

# Backend specific test class
mvn test -Dtest=BookingServiceTest

# Frontend tests (if configured)
cd frontend
npm test
```

---

## Troubleshooting

### Common Issues & Solutions

#### Backend Won't Start

```bash
# Check if port 8080 is in use
netstat -ano | findstr :8080  # Windows
lsof -i :8080  # macOS/Linux

# Kill process on port 8080
taskkill /PID <PID> /F  # Windows
kill -9 <PID>  # macOS/Linux

# Check database connectivity
psql -U smartcampus -d smartcampus -h localhost
```

#### Database Connection Error

```bash
# Verify PostgreSQL is running
# Windows: Services → PostgreSQL should be running
# macOS: brew services list
# Linux: sudo systemctl status postgresql

# Check credentials in application.yaml
# Ensure username/password are correct
```

#### Docker Issues

```bash
# View service logs
docker compose logs backend
docker compose logs postgres
docker compose logs frontend

# Rebuild images
docker compose down
docker compose build --no-cache

# Check disk space
docker system df

# Clean up unused resources
docker system prune -a
```

#### Frontend Not Loading

```bash
# Clear browser cache
# Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

# Check frontend logs
npm run dev

# Verify Vite dev server is running
# Should show: "VITE v8.x.x ready in X ms"
```

#### Mail Not Sending

```bash
# Check MailDev is running
curl http://localhost:1080

# Verify SMTP port
netstat -ano | findstr :1025

# Check backend email config
# In application.yaml: mail.host should be localhost
```

#### CORS Errors

```bash
# Error: "Access to XMLHttpRequest blocked by CORS policy"

# Solution: Check backend CORS configuration
# Should be in WebSecurityConfig or application.yaml

# Add to backend if needed:
@Configuration
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
            .allowedOrigins("http://localhost:5173")
            .allowedMethods("GET", "POST", "PUT", "DELETE", "OPTIONS");
    }
}
```

#### Port Already in Use

```bash
# If port 5173 (frontend) is in use
cd frontend
npm run dev -- --port 5174

# Update proxy in vite.config.js if needed
```

### Getting Help

1. Check relevant documentation files in root:
   - `QUICK_START_CHECKLIST.md`
   - `DB_SETUP_AND_TESTING_GUIDE.md`
   - `OAUTH_SETUP_GUIDE.md`

2. Check backend logs:
   ```bash
   docker compose logs backend -f
   ```

3. Check frontend browser console:
   - Open DevTools (F12)
   - Check Console tab for errors

4. Check Swagger API docs:
   - http://localhost:8080/swagger-ui.html

---

## Performance Tips

### Backend Optimization
- Enable query caching: `spring.jpa.properties.hibernate.cache.use_second_level_cache=true`
- Use `@Transactional(readOnly=true)` for read operations
- Implement pagination for large result sets
- Use database indexes on frequently queried columns

### Frontend Optimization
- Build for production: `npm run build`
- Enable gzip compression
- Lazy load components with React.lazy()
- Optimize images before upload
- Use CDN for static assets

### Database Optimization
- Regular VACUUM and ANALYZE: `VACUUM ANALYZE;`
- Monitor slow queries: Enable `log_statement = 'all'`
- Create indexes on foreign keys and search columns
- Archive old data periodically

---

## Deployment

### Docker Container Build

```bash
# Build backend image
cd backend/api
docker build -t smartcampus-backend:latest .

# Build frontend image  
cd ../../frontend
docker build -t smartcampus-frontend:latest .

# Push to registry
docker tag smartcampus-backend:latest yourregistry/smartcampus-backend:latest
docker push yourregistry/smartcampus-backend:latest
```

### Production Deployment Checklist

- [ ] Set strong JWT secret in environment
- [ ] Enable HTTPS with SSL certificates
- [ ] Configure CORS for production domain
- [ ] Set up proper logging and monitoring
- [ ] Configure automated backups
- [ ] Set up CI/CD pipeline
- [ ] Enable authentication rate limiting
- [ ] Configure email service (SendGrid/AWS SES)
- [ ] Set up monitoring alerts
- [ ] Document deployment procedure

---

## Team & Contribution

### Development Team

This is a group assignment for the SLIIT Professional Advancement Framework (PAF) program.

### Contributing

1. Create a feature branch: `git checkout -b feature/your-feature`
2. Commit changes: `git commit -am 'Add new feature'`
3. Push to branch: `git push origin feature/your-feature`
4. Submit pull request

### Code Standards

- **Java**: Follow Google Java Style Guide
- **JavaScript/React**: Use Airbnb JavaScript Style Guide
- **Naming**: Clear, descriptive names for classes, methods, variables
- **Comments**: Document complex logic and business rules
- **Tests**: Write unit tests for services and critical logic

---

## License

This project is developed as part of the SLIIT PAF curriculum.

---

## Additional Resources

### Documentation Files

- [Quick Start Checklist](./QUICK_START_CHECKLIST.md)
- [Database Setup & Testing Guide](./DB_SETUP_AND_TESTING_GUIDE.md)
- [OAuth Setup Guide](./OAUTH_SETUP_GUIDE.md)
- [OTP Configuration Guide](./OTP_CONFIGURATION_GUIDE.md)
- [Booking Features Guide](./BOOKING_FEATURES_REBUILD.md)
- [Notification Testing Plan](./NOTIFICATION_TESTING_PLAN.md)
- [Testing Plan](./TESTING_PLAN.md)

### External Resources

- [Spring Boot Documentation](https://spring.io/projects/spring-boot)
- [React Documentation](https://react.dev)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Docker Documentation](https://docs.docker.com/)
- [Tailwind CSS](https://tailwindcss.com/docs)
- [Vite Documentation](https://vitejs.dev/)

### API Tools

- [Postman](https://www.postman.com/) - API testing
- [Thunder Client](https://www.thunderclient.com/) - VS Code extension
- [Swagger UI](http://localhost:8080/swagger-ui.html) - Interactive docs
- [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) - VS Code extension

---

## Support

For issues, questions, or suggestions:

1. Check the troubleshooting section
2. Review existing documentation
3. Check backend logs: `docker compose logs backend`
4. Check frontend console (F12 in browser)
5. Contact the development team

---

**Last Updated**: April 20, 2026  
**Current Version**: 0.0.1-SNAPSHOT

