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
2. posts Table
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    body TEXT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INT REFERENCES users(id) ON DELETE CASCADE
);

🚀 Connection & Deployment Steps
Launched PostgreSQL RDS instance named microblog-lab5-rds.

Configured RDS inbound rule on port 5432 to only allow the EC2 Security Group.

Connected the Microblog Flask application on EC2 using the database endpoint.

Ran database migrations to create the users and posts tables.


Follow these simple, step-by-step instructions. Do one step at a time:

---

### Step 1: Create a Repository on GitHub

1. Open your browser and go to [github.com](https://github.com).
2. Log in and click the **+** (plus icon) in the top-right corner $\rightarrow$ click **New repository**.
3. Name your repository: `aws-cloud-lab5-microblog`.
4. Keep it **Public**.
5. Check the box that says **Add a README file**.
6. Click the green **Create repository** button at the bottom.

---

### Step 2: Add Your Content to the README file

1. On your new repository page, click the **pencil icon** (Edit this file) on the right side of `README.md`.
2. Delete everything inside the editor.
3. Copy and paste the exact text below:

```markdown
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

```

### 2. `posts` Table

```sql
CREATE TABLE posts (
    id SERIAL PRIMARY KEY,
    body TEXT NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    user_id INT REFERENCES users(id) ON DELETE CASCADE
);

```

---

## 🚀 Connection & Deployment Steps

1. Launched PostgreSQL RDS instance named `microblog-lab5-rds`.
2. Configured RDS inbound rule on port `5432` to only allow the EC2 Security Group.
3. Connected the Microblog Flask application on EC2 using the database endpoint.
4. Ran database migrations to create the `users` and `posts` tables.

---

## 🧪 Demonstration of CRUD Operations

| Operation | User Action in UI | Endpoint / Action | Evidence Status |
| --- | --- | --- | --- |
| **Create** | Register user / Submit new post | Form Submit | Verified (New post appears) |
| **Read** | Fetch user dashboard | `GET /index` | Verified (Feed shows posts) |
| **Update** | Edit post text | Edit Post modal | Verified ("Your post has been updated") |
| **Delete** | Click delete button & confirm | Delete action | Verified ("Your post has been deleted") |

```

4. Scroll down and click **Commit changes...** $\rightarrow$ click **Commit changes**.

---



Copy these two links to submit for Assignment 1[cite: 1]:
* **Live EC2 URL:** `[http://3.111.37.11](http://3.111.37.11)`
* **GitHub Repo URL:** `[https://github.com/](https://github.com/)<appisal>/aws-cloud-lab5-microblog`

---

Let me know once you have finished this, and we will move to **Assignment 2 (DynamoDB)**[cite: 1].

```
