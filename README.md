# RMS (Restaurant Management System)

A comprehensive Restaurant Management System built with Oracle APEX (Application Express) for managing restaurant operations including customer management, menu management, order processing, table reservations, employee management, and user authentication.

## Table of Contents
- Overview
- Features
- Technology Stack
- Prerequisites
- Installation Guide
  - Database Setup
  - Application Import
- System Configuration
- Database Schema
- Default Users
- Application Pages
- Security
- Troubleshooting
- Support

## Overview

RMS (Restaurant Management System) is a full-featured web application that helps restaurants manage their daily operations efficiently. The system provides an intuitive interface for managing customers, menu items, orders, table reservations, and employee information.

## Features

### Core Features
- Customer Management - Add, edit, delete, and view customer information
- Menu Management - Manage food and beverage items with categories and pricing
- Order Processing - Create and track customer orders
- Table Reservation - Manage table bookings and availability
- Employee Management - Staff information and role management
- User Authentication - Secure login with role-based access control

### User Roles
- Admin - Full system access including user management and data editing
- Viewer - Read-only access to view reports and data

## Technology Stack

- Frontend: Oracle APEX (Application Express) 23.2.4
- Database: Oracle Database
- Backend: PL/SQL
- Authentication: Custom authentication with user table
- UI Theme: Universal Theme 42
- Reporting: Interactive Reports

## Prerequisites

Before installing RMS, ensure you have:

1. Oracle Database (11g or higher recommended)
2. Oracle APEX (23.2.0 or higher)
3. Oracle SQL Developer or any SQL client
4. Web Browser (Chrome, Firefox, Edge, Safari)
5. Database user with APEX_ADMINISTRATOR_ROLE or sufficient privileges

## Installation Guide

### Database Setup

1. Clone the repository

git clone https://github.com/yourusername/rms.git
cd rms

2. Run the database setup script

Connect to your Oracle database using SQL*Plus or SQL Developer and execute:

@database_setup.sql

Or copy and paste the complete database setup script from the repository.

The script will:
- Create all necessary tables (CUSTOMER, MENU, ORDERS, RESERVATION, RESTAURANT_TABLE, EMPLOYEES, USERS)
- Create sequences for auto-incrementing IDs
- Insert sample data for testing
- Verify the data insertion

### Application Import

1. Login to Oracle APEX

Navigate to your APEX workspace URL and login with your workspace credentials.

2. Import the Application

- Click on App Builder -> Import
- Select the f128755.sql file from the repository
- Click Next and follow the import wizard
- Set the parsing schema as your database schema
- Click Install Application

3. Verify Installation

- After successful import, you should see the application "RMS" in your App Builder
- Click on the application to open it
- Login using the default credentials (see Default Users section)

## System Configuration

### Authentication Setup

The application uses custom authentication. Ensure the following:

1. The authentication function my_auth is correctly created (included in the import)
2. The USERS table exists with the correct columns
3. User accounts are activated (USER_ACTIVATED = 1)

### Authorization

The application uses two security schemes:
- Administration Rights - For admin-level access
- admin_editor - Checks if the logged-in user has admin privileges

These are configured in the application and reference the USERS table.

## Database Schema

### Tables Structure

Table Name: CUSTOMER
Description: Customer information
Key Columns: CUSTOMER_ID (PK)

Table Name: MENU
Description: Menu items catalog
Key Columns: ITEM_ID (PK)

Table Name: ORDERS
Description: Customer orders
Key Columns: ORDER_ID (PK), CUSTOMER_ID (FK)

Table Name: RESERVATION
Description: Table reservations
Key Columns: RESERVATION_ID (PK), CUSTOMER_ID (FK)

Table Name: RESTAURANT_TABLE
Description: Available tables
Key Columns: TABLE_NUMBER (PK)

Table Name: EMPLOYEES
Description: Staff information
Key Columns: EMPLOYEE_ID (PK)

Table Name: USERS
Description: System users authentication
Key Columns: USER_ID (PK)

### Relationships
- ORDERS.CUSTOMER_ID references CUSTOMER.CUSTOMER_ID
- RESERVATION.CUSTOMER_ID references CUSTOMER.CUSTOMER_ID

## Default Users

The following users are pre-configured for testing:

Username: Asif
Password: asif12
Role: Admin
Status: Active

Username: Ahanaf
Password: ahanaf12
Role: Viewer
Status: Active

Username: Anika
Password: anika12
Role: Viewer
Status: Active

Username: Rayhan
Password: rayhan12
Role: Viewer
Status: Active

NOTE: These are default credentials for testing. Change passwords immediately in a production environment.

## Application Pages

Page ID: 1
Page Name: Home
Access: Public
Description: Landing page

Page ID: 2
Page Name: Customer Form
Access: Authenticated
Description: Add/Edit customers

Page ID: 3
Page Name: Menu
Access: Admin only
Description: Menu management

Page ID: 4
Page Name: Order Form
Access: Authenticated
Description: Create orders

Page ID: 5
Page Name: Reservation Form
Access: Authenticated
Description: Book tables

Page ID: 10
Page Name: Restaurant Table
Access: Admin only
Description: Manage tables

Page ID: 11
Page Name: Restaurant Table List
Access: Authenticated
Description: View tables

Page ID: 12
Page Name: Menu List
Access: Authenticated
Description: View menu items

Page ID: 13
Page Name: Order List
Access: Admin only
Description: View all orders

Page ID: 15
Page Name: Employee Form
Access: Admin only
Description: Manage employees

Page ID: 16
Page Name: Employee List
Access: Admin only
Description: View employees

Page ID: 17
Page Name: Reservation List
Access: Admin only
Description: View reservations

Page ID: 18
Page Name: Customer List
Access: Admin only
Description: View customers

Page ID: 19
Page Name: User Report
Access: Admin only
Description: User management

Page ID: 20
Page Name: User Form
Access: Admin only
Description: Add/Edit users

Page ID: 9999
Page Name: Login
Access: Public
Description: Authentication page

## Security

### Authentication
- Custom authentication function validates against USERS table
- Passwords are stored in plain text (consider implementing encryption in production)
- Session management handled by Oracle APEX

### Authorization
- Admin-only pages protected by security scheme admin_editor
- Viewer role has limited access (view-only for reports)
- All forms require authentication

### Best Practices for Production

1. Encrypt passwords - Modify the authentication to use password hashing
2. Use HTTPS - Ensure the application is served over HTTPS
3. Regular backups - Backup your database regularly
4. Update default passwords - Change all default user passwords
5. Limit admin access - Grant admin privileges only when necessary

## Troubleshooting

### Common Issues and Solutions

Issue: "ORA-00942: table or view does not exist"

Solution: Ensure the parsing schema in the application matches the schema where tables were created. Re-import the application with the correct parsing schema.

Issue: Login fails with valid credentials

Solution: 
1. Check if USER_ACTIVATED = 1 for the user
2. Verify the authentication function exists and is correct
3. Check case sensitivity in username/password

Issue: "Insufficient privileges" when accessing pages

Solution: Verify the user's role in the USERS table. Admin pages require user_type = 'admin'

Issue: Foreign key constraint errors when inserting data

Solution: Ensure referenced records exist before inserting. For example, create customer before creating order.

Issue: Application import fails

Solution: 
1. Verify you have APEX_ADMINISTRATOR_ROLE
2. Check database version compatibility (requires Oracle 11g+)
3. Ensure enough tablespace is available

### Debugging

Enable debugging in APEX:

1. Go to the application
2. Click Edit Application Properties
3. Set Debug to Yes
4. Review debug messages in the application or APEX logs

## Support

For issues, questions, or contributions:

- GitHub Issues: Create an issue in the repository
- Documentation: Refer to Oracle APEX documentation for platform-specific issues

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Oracle APEX team for the amazing low-code platform
- Contributors and testers of the RMS system

---

Version: 1.0
Last Updated: 2024
Application ID: 128755
