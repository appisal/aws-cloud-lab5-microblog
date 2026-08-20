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

`
---

# Assignment 2 — DynamoDB Integration

## Application Details

**Application:** Microblog  
**Database:** Amazon DynamoDB  
**DynamoDB Table:** `MicroblogPosts`  
**AWS Region:** `ap-south-1`  
**Partition Key:** `id`  
**EC2 Application URL:** `http://3.111.37.11`

---

## 1. Architecture

For Assignment 2, Amazon DynamoDB was used as the NoSQL database.

```text
Internet
   |
   v
AWS EC2 — Microblog Application
   |
   | AWS DynamoDB API
   v
Amazon DynamoDB
   |
   v
MicroblogPosts Table


2. DynamoDB Table Configuration

| Property      | Value            |
| ------------- | ---------------- |
| Table Name    | `MicroblogPosts` |
| AWS Region    | `ap-south-1`     |
| Table Status  | `ACTIVE`         |
| Partition Key | `id`             |
| Key Type      | `HASH`           |


3. DynamoDB Attribute Types
| Attribute  | DynamoDB Type    | Example                                             |
| ---------- | ---------------- | --------------------------------------------------- |
| `id`       | String (`S`)     | `"1"`                                               |
| `username` | String (`S`)     | `"aditya"`                                          |
| `age`      | Number (`N`)     | `21`                                                |
| `active`   | Boolean (`BOOL`) | `true`                                              |
| `tags`     | List (`L`)       | `["cloud","aws","dynamodb"]`                        |
| `profile`  | Map (`M`)        | `{"city":"Mumbai","course":"Computer Engineering"}` |


4. DynamoDB CRUD Operations
CREATE

A new item was created in the MicroblogPosts table.

The item contained:
id       = "1"
username = "aditya"
age      = 21
active   = true
tags     = ["cloud", "aws", "dynamodb"]
profile  = {"city": "Mumbai", "course": "Computer Engineering"}

READ

The created item was retrieved using the partition key:

id = "1"

The get-item operation successfully returned the stored item.

UPDATE

The existing item was updated using the update-item operation.

The following values were changed:

age    : 21 → 22
active : true → false

The updated item was successfully returned after the update.

DELETE

The item was deleted using the delete-item operation.

A final DynamoDB scan was performed after deletion and confirmed that the item was no longer present.

5. Application CRUD Demonstration

The Microblog application running on EC2 was also tested through the application interface.

Operation	Application Action	Result
Create	Submitted a new Microblog post	Post appeared successfully
Read	Viewed the created post	Post was displayed
Update	Edited the created post	Updated post was displayed
Delete	Deleted the updated post	Post was removed

The CRUD operations were tested using the running Microblog application.

6. EC2 Application

The Microblog application is deployed on AWS EC2 and was successfully accessed through the public endpoint.

EC2 Application URL:

http://3.111.37.11

The application was tested by logging in, creating a post, viewing the post, editing the post, and deleting the post.

7. DynamoDB Verification

The DynamoDB table was verified using AWS CLI commands.

Table Verification
aws dynamodb describe-table \
  --table-name MicroblogPosts \
  --region ap-south-1

The table status was confirmed as:

ACTIVE
Data Verification

The item was verified using:

aws dynamodb scan \
  --table-name MicroblogPosts \
  --region ap-south-1

The scan displayed the stored item and demonstrated the required DynamoDB attribute types.

Final Delete Verification

After deleting the item, a final scan confirmed that the deleted item was no longer present.

8. Evidence Submitted

The following evidence was collected during the implementation:

DynamoDB table MicroblogPosts shown as ACTIVE.
DynamoDB item showing the required attribute types.
DynamoDB READ operation.
DynamoDB UPDATE operation.
DynamoDB DELETE operation.
Final DynamoDB scan confirming deletion.
Microblog application running on EC2.
Application CREATE and READ demonstration.
Application UPDATE demonstration.
Application DELETE demonstration.
9. Assignment 2 Summary

Assignment 2 demonstrates the use of Amazon DynamoDB as a NoSQL database with the Microblog application.

The implementation includes:

DynamoDB table deployment
Partition key configuration
String attribute
Number attribute
Boolean attribute
List attribute
Map attribute
CREATE operation
READ operation
UPDATE operation
DELETE operation
EC2 application testing
Application-level CRUD testing
10. Assignment 2 Deliverables

GitHub Repository:

https://github.com/appisal/aws-cloud-lab5-microblog

EC2 Application:

http://3.111.37.11

DynamoDB Table:

MicroblogPosts

AWS Region:

ap-south-1

Database Type:

Amazon DynamoDB

CRUD Operations:

Create, Read, Update, Delete

DynamoDB Attribute Types:

String, Number, Boolean, List, Map



