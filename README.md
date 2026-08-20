# AWS Cloud Computing Lab 5 — Assignment 1: RDS Integration

## Application Details

**Application:** Microblog
**Database:** Amazon RDS PostgreSQL
**RDS Instance:** `microblog-lab5-rds`
**EC2 URL:** `http://3.111.37.11`
**AWS Region:** `ap-south-1`

---

## 1. Architecture

The Microblog Flask application is deployed on an AWS EC2 instance and connected to an Amazon RDS PostgreSQL database.

**Architecture:**

```text
Internet
   |
   v
AWS EC2 — Microblog Flask Application
   |
   | PostgreSQL : 5432
   v
Amazon RDS PostgreSQL
```

The RDS security configuration restricts database access to the EC2 Security Group rather than allowing unrestricted internet access.

---

## 2. RDS Database Configuration

| Setting         | Value                |
| --------------- | -------------------- |
| Database Engine | PostgreSQL           |
| DB Instance     | `microblog-lab5-rds` |
| Instance Class  | `db.t4g.micro`       |
| Availability    | Single-AZ            |
| Port            | `5432`               |
| Region          | `ap-south-1`         |

### Security

The RDS inbound rule allows PostgreSQL traffic on port `5432` from the EC2 Security Group only.

No unrestricted `0.0.0.0/0` database access is used.

---

## 3. Database Schema

The Assignment 1 database contains relational tables for the application data.

### Users

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(64) UNIQUE NOT NULL,
    email VARCHAR(120) UNIQUE NOT NULL,
    password_hash VARCHAR(256) NOT NULL
);
```

### Posts

```sql
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    body TEXT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INT REFERENCES users(id) ON DELETE CASCADE
);
```

The `posts.user_id` column establishes a relationship with the `users` table.

---

## 4. Deployment and Connection

1. Created the PostgreSQL RDS instance `microblog-lab5-rds`.
2. Configured the RDS Security Group for PostgreSQL traffic on port `5432`.
3. Restricted the inbound database rule to the EC2 Security Group.
4. Connected the Microblog application running on EC2 to the RDS PostgreSQL database.
5. Applied the required database migrations/schema.
6. Verified that the application could communicate with the database.

---

## 5. CRUD Demonstration

The Microblog application demonstrates the required CRUD operations.

| Operation  | Application Action          | Result                       |
| ---------- | --------------------------- | ---------------------------- |
| **Create** | Register user / create post | New record is created        |
| **Read**   | Open the feed/dashboard     | Stored records are displayed |
| **Update** | Edit an existing record     | Record is updated            |
| **Delete** | Delete an existing record   | Record is removed            |

### CRUD Evidence

Screenshots/evidence are included with the lab submission to demonstrate the operations from the running EC2 application.

---

## 6. EC2 Application

The deployed Microblog application is available at:

**EC2 URL:** `http://3.111.37.11`

The application was tested from the public endpoint after deployment.

---

## 7. Assignment 1 Deliverables

* GitHub Repository: `https://github.com/appisal/aws-cloud-lab5-microblog`
* EC2 Application URL: `http://3.111.37.11`
* Database: Amazon RDS PostgreSQL
* CRUD: Create, Read, Update, Delete
* Security: RDS PostgreSQL access restricted to the EC2 Security Group
* Evidence: Screenshots submitted with the lab report
* Report: 1–2 page Assignment 1 report

---

## 8. Security Note

Database passwords, AWS access keys, secret keys, and other sensitive credentials are not stored in this GitHub repository.

The application database connection credentials should remain in the EC2 environment/configuration and must not be committed to source control.

---

## 9. Lab Reference

This implementation follows the requirements of Cloud Computing Lab 5 — Study and Implementation of AWS RDS and NoSQL Databases.
