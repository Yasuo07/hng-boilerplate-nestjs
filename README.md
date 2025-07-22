# HNG NestJS Boilerplate

A comprehensive NestJS boilerplate application with authentication, user management, organization management, email functionality, and database integration. This project serves as a foundation for building scalable Node.js applications with TypeScript.

## 🚀 Features

- **Authentication & Authorization**: JWT-based authentication with Passport.js
- **User Management**: Complete user CRUD operations with profile management
- **Organization Management**: Multi-tenant organization support
- **Email System**: Nodemailer integration with Handlebars templates
- **Database Integration**: TypeORM with PostgreSQL support
- **API Documentation**: Swagger/OpenAPI documentation
- **Logging**: Structured logging with Pino
- **Validation**: Request validation with class-validator
- **Testing**: Jest testing framework with e2e tests
- **Code Quality**: ESLint, Prettier, and Husky for git hooks
- **Database Migrations**: TypeORM migrations with seeding
- **Health Checks**: Application health monitoring endpoints

## 🛠️ Tech Stack

- **Framework**: NestJS 10.x
- **Language**: TypeScript 5.x
- **Database**: PostgreSQL with TypeORM
- **Authentication**: JWT with Passport.js
- **Email**: Nodemailer with Handlebars templates
- **Validation**: class-validator & class-transformer
- **Documentation**: Swagger/OpenAPI
- **Logging**: Pino
- **Testing**: Jest
- **Code Quality**: ESLint, Prettier, Husky

## 📋 Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** (v16 or later) - [Download here](https://nodejs.org/)
- **npm** (Node Package Manager, included with Node.js)
- **PostgreSQL** - [Download here](https://www.postgresql.org/download/)
- **NestJS CLI** - Install globally: `npm install -g @nestjs/cli`

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/hngprojects/hng_boilerplate_nestjs.git
cd hng_boilerplate_nestjs
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Create environment files based on your profile:

```bash
# For local development
cp .env.example .env.local

# For other environments
cp .env.example .env.development
cp .env.example .env.production
```

Configure your environment variables:

```env
PROFILE=local
NODE_ENV=development
PORT=3008

# Database Configuration
DB_TYPE=postgres
DB_USERNAME=your_username
DB_PASSWORD=your_password
DB_HOST=localhost
DB_DATABASE=your_database_name
DB_ENTITIES=dist/**/*.entity{.ts,.js}
DB_MIGRATIONS=dist/db/migrations/*{.ts,.js}

# JWT Configuration
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRES_IN=24h

# SMTP Configuration (for email functionality)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASSWORD=your_app_password
```

### 4. Database Setup

Ensure PostgreSQL is running and create your database:

```sql
CREATE DATABASE your_database_name;
```

### 5. Run Migrations

```bash
# Generate migrations (if needed)
npm run migration:generate

# Run migrations
npm run migration:run
```

### 6. Start the Application

```bash
# Development mode with hot reload
npm run start:dev

# Production mode
npm run start:prod
```

The application will be available at `http://localhost:3008`

## 📁 Project Structure

```
src/
├── app.module.ts                 # Main application module
├── main.ts                      # Application entry point
├── health.controller.ts         # Health check endpoints
├── database/
│   ├── data-source.ts          # Database configuration
│   └── seeding/                # Database seeding
├── entities/
│   └── base.entity.ts          # Base entity class
├── guards/
│   └── auth.guard.ts           # Authentication guard
├── helpers/
│   ├── custom-http-filter.ts   # HTTP exception filter
│   ├── skipAuth.ts             # Skip authentication decorator
│   └── SystemMessages.ts       # System message constants
├── modules/
│   ├── auth/                   # Authentication module
│   ├── user/                   # User management module
│   ├── organisations/          # Organization management module
│   └── email/                  # Email functionality module
└── shared/
    └── inteceptors/
        └── response.interceptor.ts  # Response interceptor
```

## 🔧 Available Scripts

### Development
- `npm run start:dev` - Start development server with hot reload
- `npm run start:debug` - Start with debug mode
- `npm run dev` - Start with ts-node-dev for development

### Production
- `npm run build` - Build the application
- `npm run start:prod` - Start production server

### Database
- `npm run migration:generate` - Generate new migration
- `npm run migration:run` - Run pending migrations
- `npm run migration:revert` - Revert last migration
- `npm run seed` - Run database seeding

### Testing
- `npm run test` - Run unit tests
- `npm run test:watch` - Run tests in watch mode
- `npm run test:cov` - Run tests with coverage
- `npm run test:e2e` - Run end-to-end tests

### Code Quality
- `npm run lint` - Run ESLint
- `npm run format` - Format code with Prettier
- `npm run check-format` - Check code formatting
- `npm run check-lint` - Check linting rules

## 🔌 API Endpoints

### Health Check
- `GET /` - Application home
- `GET /health` - Health check endpoint
- `GET /api/v1` - API version info

### Authentication
- `POST /api/v1/auth/register` - User registration
- `POST /api/v1/auth/login` - User login

### Users
- `GET /api/v1/users` - Get all users (protected)
- `GET /api/v1/users/:id` - Get user by ID (protected)

### Organizations
- `GET /api/v1/organisations` - Get all organizations (protected)
- `POST /api/v1/organisations` - Create organization (protected)

### Seeding
- `GET /api/v1/seed/users` - Get seeded user data

## 📚 API Documentation

Once the application is running, you can access the Swagger API documentation at:

```
http://localhost:3008/api/docs
```

## 🧪 Testing

The project includes comprehensive testing setup:

### Unit Tests
```bash
npm run test
```

### E2E Tests
```bash
npm run test:e2e
```

### Test Coverage
```bash
npm run test:cov
```

## 🔐 Authentication

The application uses JWT-based authentication:

1. **Register**: Create a new user account
2. **Login**: Authenticate and receive JWT token
3. **Protected Routes**: Include JWT token in Authorization header

Example usage:
```bash
# Login
curl -X POST http://localhost:3008/api/v1/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email": "user@example.com", "password": "password"}'

# Use protected endpoint
curl -X GET http://localhost:3008/api/v1/users \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

## 📧 Email Functionality

The application includes email functionality with:

- **Templates**: Handlebars-based email templates
- **SMTP Integration**: Configurable SMTP settings
- **Email Types**: Confirmation, newsletter, password reset, waitlist

## 🗄️ Database

### Entities
- **User**: User accounts with profiles
- **Organization**: Multi-tenant organizations
- **Base Entity**: Common fields (id, timestamps)

### Migrations
- Automatic migration generation
- Migration versioning
- Rollback support

### Seeding
- Automatic data seeding on startup
- Sample user data
- Test data generation

## 🚀 Deployment

### Environment Variables
Ensure all required environment variables are set for your deployment environment.

### Database
- Run migrations: `npm run migration:run`
- Ensure database connection is properly configured

### Build & Start
```bash
npm run build
npm run start:prod
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Submit a pull request

## 📄 License

This project is licensed under the UNLICENSED license.

## 🆘 Support

For support and questions:
- Check the [setup guide](setup-guide.md) for detailed setup instructions
- Review the [wiki documentation](wiki_readme/) for additional resources
- Open an issue on GitHub

## 🔄 Version History

- **v0.0.1** - Initial boilerplate with authentication, user management, and database integration

---

**Happy Coding! 🚀**
