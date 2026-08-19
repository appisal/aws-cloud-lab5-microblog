# aws-cloud-lab5-microblog
# AWS Cloud Computing Lab 5 - Assignment 1: RDS Integration

**Application Name:** Microblog  
**Live EC2 URL:** `http://3.111.37.11`  
**Database Engine:** AWS RDS (PostgreSQL)  
**DB Instance Identifier:** `microblog-lab5-rds`  

---

## 📌 Architecture & Database Configuration
- **Compute:** AWS EC2 Instance running Microblog (Python/Flask backend).
- **Database:** Amazon RDS PostgreSQL (db.t4g.micro, Single-AZ).
- **Security Rule:** RDS port 5432 is restricted to inbound traffic from the EC2 Security Group ID only.

---

## 🗄️ Database Schema Design (2 Relational Tables)

### 1. `users` Table
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(64) UNIQUE NOT NULL,
    email VARCHAR(120) UNIQUE NOT NULL,
    password_hash VARCHAR(256) NOT NULL
);
