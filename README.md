# 🔐 FastAPI Role-Based Access Control (RBAC) API

A secure, scalable RESTful API built using **FastAPI**, providing user authentication and role-based access control with **JWT** and **MongoDB**.  
The system supports user registration, login, and complete CRUD functionality for projects, all gated by user roles.

---

## ⚙️ Project Setup

Follow these steps to get the project running locally:

1. **Set up a virtual environment:**
   ```bash
   python -m venv venv
   ```

2. **Activate the environment:**
   - **Linux/macOS:**
     ```bash
     source venv/bin/activate
     ```
   - **Windows (Command Prompt):**
     ```cmd
     venv\Scripts\activate
     ```
   - **Windows (PowerShell):**
     ```powershell
     .\venv\Scripts\Activate
     ```

3. **Install required packages:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Start the development server:**
   ```bash
   uvicorn main:app --reload
   ```

---

## 📌 API Endpoints Overview

### 👤 User Endpoints

#### 🔸 Register User
- **Route:** `POST /register`
- **Purpose:** Create a new user with a specified role.
- **Request Example:**
  ```json
  {
    "username": "your_username",
    "password": "your_password",
    "role": "admin"
  }
  ```
- **Response:**
  ```json
  {
    "username": "your_username",
    "role": "admin"
  }
  ```

#### 🔸 User Login
- **Route:** `POST /login`
- **Purpose:** Authenticates user and returns a JWT access token.
- **Request Example:**
  ```json
  {
    "username": "your_username",
    "password": "your_password"
  }
  ```
- **Response:**
  ```json
  {
    "access_token": "JWT_token_here",
    "token_type": "bearer"
  }
  ```

---

### 📁 Project Endpoints

All routes below **require authentication** and certain actions are **restricted to admin users**.

#### 📄 Get All Projects
- **Route:** `GET /projects/`
- **Access:** Authenticated users
- **Response:** List of project objects

#### ➕ Create Project (Admin Only)
- **Route:** `POST /projects/`
- **Access:** Admin
- **Request:**
  ```json
  {
    "name": "Project Name",
    "description": "Detailed description"
  }
  ```
- **Response:** Created project object with timestamps

#### 📝 Update Project (Admin Only)
- **Route:** `PUT /projects/{project_id}`
- **Access:** Admin
- **Request:**
  ```json
  {
    "name": "Updated Name",
    "description": "Updated Description"
  }
  ```
- **Response:** Updated project object

#### ❌ Delete Project (Admin Only)
- **Route:** `DELETE /projects/{project_id}`
- **Access:** Admin
- **Response:**  
  - **Status Code:** `204 No Content`

---

## 🔐 Authentication Requirements

All secured routes require this header with a valid JWT:
```http
Authorization: Bearer <your_jwt_token>
```

---

## 🛠 Technologies Used

- **Framework:** FastAPI  
- **Database:** MongoDB (via MongoEngine)  
- **Authentication:** JWT (JSON Web Tokens)
