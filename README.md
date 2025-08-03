# SQL Playground

A simple MySQL database environment for practicing SQL queries and experimenting with database operations.

## Overview

This project provides a containerized MySQL database with sample data for learning and testing SQL commands. It includes a basic e-commerce schema with users and orders tables.

## Features

- **MySQL 8** database running in Docker
- **Pre-configured schema** with users and orders tables
- **Sample data** for immediate experimentation
- **Easy setup** with Docker Compose

## Database Schema

### Users Table
- `id` - Auto-incrementing primary key
- `name` - User's full name (VARCHAR 100)
- `email` - User's email address (VARCHAR 100, UNIQUE)
- `created_at` - Timestamp of user creation

### Orders Table
- `id` - Auto-incrementing primary key
- `user_id` - Foreign key referencing users table
- `product` - Product name (VARCHAR 100)
- `amount` - Order amount (DECIMAL 10,2)
- `created_at` - Timestamp of order creation

## Getting Started

### Prerequisites
- Docker
- Docker Compose

### Setup

1. Clone this repository:
   ```bash
   git clone <repository-url>
   cd sql-playground
   ```

2. Start the MySQL database:
   ```bash
   docker-compose up -d
   ```

3. Connect to the database using your preferred MySQL client with these credentials:
   - **Host:** localhost
   - **Port:** 3306
   - **Database:** playground
   - **Username:** dev
   - **Password:** dev

   Or connect as root:
   - **Username:** root
   - **Password:** root

### Using the Command Line

Connect using the MySQL command line client:
```bash
mysql -h localhost -P 3306 -u dev -p playground
# Enter password: dev
```

## Sample Queries

Once connected, try these sample queries:

```sql
-- View all users
SELECT * FROM users;

-- View all orders with user information
SELECT u.name, u.email, o.product, o.amount, o.created_at
FROM users u
JOIN orders o ON u.id = o.user_id;

-- Find total spending per user
SELECT u.name, SUM(o.amount) as total_spent
FROM users u
JOIN orders o ON u.id = o.user_id
GROUP BY u.id, u.name;
```

## Managing the Environment

### Start the database
```bash
docker-compose up -d
```

### Stop the database
```bash
docker-compose down
```

### View logs
```bash
docker-compose logs mysql
```

### Reset the database
```bash
docker-compose down
docker-compose up -d
```

## File Structure

```
sql-playground/
├── docker-compose.yml    # Docker Compose configuration
├── README.md            # This file
└── init/
    ├── schema.sql       # Database schema definition
    └── seed.sql         # Sample data insertion
```

## Contributing

Feel free to add more tables, sample data, or modify the schema to suit your learning needs. The `init/` directory contains the SQL files that are automatically executed when the database starts.

## License

This project is open source and available under the [MIT License](LICENSE).