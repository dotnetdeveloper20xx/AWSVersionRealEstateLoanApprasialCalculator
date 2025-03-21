# Real Estate Loan Management System

## Project Overview
The **Real Estate Loan Management System** is an **ASP.NET Core 8 Web API** microservice-based application that enables real estate developers to perform financial appraisals by inputting financial parameters and generating multiple calculated financial models. Users can experiment with different interest rates, term lengths, and purchase prices to obtain optimal financial projections. 

The system follows **Clean Architecture, CQRS, Repository Pattern, and EF Core** and is built using **AWS Serverless Services** for scalability and performance.

---

## **Architecture Overview**

### **What is this project?**
This project allows users to:
- Input real estate project costs, values, rental income, and loan parameters.
- Generate financial appraisal models based on input values.
- Experiment with financial parameters to compare different models.
- Persist input and calculated models in **Amazon RDS (PostgreSQL/MySQL)** and **Amazon DynamoDB**.
- Securely access and manage loan models via **JWT authentication & role-based access control**.
- Deploy and scale using **AWS Serverless Services**.

---

### **Why this architecture?**
- **Microservices-based Design**: Enables modular development and scaling.
- **Clean Architecture**: Ensures separation of concerns, maintainability, and testability.
- **CQRS & Event-Driven Architecture**: Enhances performance and decouples reads/writes.
- **AWS Serverless Services**: Reduces infrastructure overhead and optimizes costs.
- **Secure Web API**: Implements industry-best security practices (JWT, Role-Based Access Control, AWS Secrets Manager).
- **Centralized Logging & Monitoring**: Uses **AWS CloudWatch** for tracking.
- **Automated CI/CD Pipelines**: Implements **AWS CodePipeline** for seamless deployment.

---

## **System Design & Architecture**

### **High-Level Architecture**
- **Frontend (Future Consideration)**: Angular/Blazor (optional).
- **Backend Microservices**:
  - **Loan Management API** (Handles user input storage & retrieval).
  - **Financial Appraisal API** (Performs financial calculations).
  - **User Management API** (Manages authentication & security).
- **Databases**:
  - **Amazon RDS (PostgreSQL/MySQL)** (Structured Data - Financial Inputs & Models).
  - **Amazon DynamoDB** (Unstructured Data - Historical Models & Logs).
- **Messaging & Background Processing**:
  - **Amazon SQS (Simple Queue Service)** (For asynchronous event-based processing).
  - **AWS Lambda** (For long-running calculations).
- **Security & Authentication**:
  - **JWT-based Auth & Role-Based Access Control (RBAC).**
  - **AWS Secrets Manager** (For securing credentials).
- **Deployment & Monitoring**:
  - **AWS CodePipeline** (Automated CI/CD pipelines for deployment).
  - **AWS CloudWatch** (Real-time logging & monitoring).

---

### **Microservices Breakdown**

#### **1. Loan Management API**
Handles **user authentication, loan input storage, and retrieval**.

- **Endpoints**:
  - `POST /loans/create` → Submit input model.
  - `GET /loans/{id}` → Retrieve loan input model.
  - `GET /loans/{id}/calculated-models` → Retrieve previous models.
  - `PUT /loans/{id}` → Update loan model.
  - `DELETE /loans/{id}` → Delete loan model.
- **Tech Stack**:
  - **ASP.NET Core 8 Web API**
  - **EF Core with Amazon RDS (PostgreSQL/MySQL)**
  - **Amazon DynamoDB for historical data**

#### **2. Financial Appraisal API**
Handles **financial calculations based on user inputs**.

- **Endpoints**:
  - `POST /calculations/generate` → Generate financial appraisal model.
  - `GET /calculations/{id}` → Retrieve a specific calculated model.
  - `POST /calculations/experiment` → Test different financial parameters.
- **Tech Stack**:
  - **ASP.NET Core 8 Web API**
  - **CQRS Pattern**
  - **AWS Lambda** (Async calculations)
  - **Fluent Validation** (Validates user input)

#### **3. User Management API**
Handles **authentication and security**.

- **Endpoints**:
  - `POST /auth/register` → Register new users.
  - `POST /auth/login` → Authenticate user & return JWT token.
  - `GET /auth/userinfo` → Fetch logged-in user details.
- **Tech Stack**:
  - **ASP.NET Core 8 Web API**
  - **JWT Authentication & Role-Based Authorization**
  - **AWS Secrets Manager** (Securing credentials)

---

### **Database Design**

#### **Amazon RDS (Structured Data)**
- **Loan Table** (Stores user input models).
- **CalculatedModels Table** (Stores calculated financial results).

#### **Amazon DynamoDB (Unstructured Data)**
- Stores historical models, logs, and previous user experiments.

---

## **Security & Best Practices**
- **Secure Web API**: Implements JWT-based authentication & RBAC.
- **AWS Secrets Manager**: Protects API keys, database credentials.
- **Centralized Exception Handling**: Uses Middleware-based logging.
- **Fluent Validation**: Ensures valid user inputs.
- **Logging & Monitoring**: Uses AWS CloudWatch for tracking.

---

## **Deployment & CI/CD Strategy**
- **AWS CodePipeline (CI/CD Pipeline)**:
  - Automates **build, test, and deployment**.
  - Deploys microservices as **AWS Fargate (ECS)** or **AWS Lambda**.
- **Infrastructure as Code (IaC)**:
  - Uses **AWS CloudFormation** or **Terraform** for AWS resource provisioning.

---

## **Future Enhancements**
1. **GraphQL API Support** - Enables flexible data fetching.
2. **Machine Learning Integration** - Advanced financial analysis.
3. **Real-time Loan Monitoring Dashboard** - Uses **AWS AppSync & WebSockets**.
4. **Mobile Application** - Extend service to mobile users.
5. **Multi-Tenancy Support** - Serve multiple real estate firms.
6. **Enhanced Loan Analytics** - Amazon QuickSight for advanced reporting.

---

## **Conclusion**
This project delivers a **scalable, secure, and high-performance** Real Estate Loan Management System using the best industry practices and AWS cloud ecosystem. The architecture ensures **modularity, maintainability, and ease of future enhancements** while optimizing cloud cost and performance.


