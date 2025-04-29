
# 🚀 Serverless Student Data Manager (AWS Project)

A simple serverless web application that allows users to add and view student data using **DynamoDB**, **AWS Lambda**, **API Gateway**, and a **static S3-hosted frontend**.

---

## 🧰 Tech Stack

- **Frontend**: HTML, JavaScript
- **Backend**: AWS Lambda (Python)
- **Database**: Amazon DynamoDB
- **API Management**: Amazon API Gateway
- **Hosting**: Amazon S3 (Static Website)

---

## 🗂️ Features

- Add student records (name & email)
- View all student records
- Serverless architecture
- Fully deployed on AWS

---

## 📌 Architecture Diagram

![Architecture Diagram](./assets/architecture-diagram.png)

---

## 🛠️ Setup Instructions

### 1. Create DynamoDB Table

- Go to **DynamoDB** → Create table
  - **Table name**: `studentData`
  - **Primary key**: `id` (String)

---

### 2. Create Lambda Functions

- **PostStudentData**: Handles POST requests to add data
- **GetStudentData**: Handles GET requests to retrieve data

Both Lambda functions are available in the repo under the `lambda/` directory.

> ✅ Ensure both functions are configured with **AmazonDynamoDBFullAccess** and **AWSLambdaBasicExecutionRole** permissions.

---

### 3. Setup API Gateway

- Create an **HTTP API** with the following routes:
  - `POST /addStudent` → integrates with `PostStudentData`
  - `GET /getStudents` → integrates with `GetStudentData`

> 💡 Note the **Invoke URL** of the API for use in the frontend.

---

### 4. Configure S3 Bucket for Frontend Hosting

- Create an S3 bucket (e.g., `student-data-app`)
- **Uncheck**: Block all public access
- Enable **Static Website Hosting**
- Upload:
  - `index.html`
  - `scripts.js`

---

### 5. Add Bucket Policy for Public Access

```json
{
  "Id": "Policy1745909252201",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1745909251307",
      "Action": ["s3:GetObject"],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::your-bucket-name/*",
      "Principal": "*"
    }
  ]
}
