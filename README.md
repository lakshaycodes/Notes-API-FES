# 🛡️ JWT Auth + Notes API

A simple RESTful API built with Django and Django REST Framework that allows users to register, authenticate using JWT, and manage personal notes. All notes are private and user-specific, with full token-based authentication and secure access to protected routes.

---

## 🛠️ Tech Stack

- Python 3.x
- Django 4.x
- Django REST Framework
- SimpleJWT (`djangorestframework-simplejwt`)
- SQLite3 (default DB)

---

## ⚙️ Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/lakshaycodes/notes-api-fes.git
cd note-api-fes
```

### 2. Create a Virtual Environment

```bash
pip install uv
uv venv
source .venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
uv pip install -r requirements.txt
cd notes
```

### 4. Run Migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Start the Development Server

```bash
python manage.py runserver
```

Server will run at: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

---

## 🔐 API Endpoints

### 🔑 Authentication

| Method | Endpoint                | Description                     |
|--------|-------------------------|---------------------------------|
| POST   | `/api/register/`        | Register a new user             |
| POST   | `/api/login/`           | Obtain access and refresh token |
| POST   | `/api/token/refresh/`   | Refresh access token            |
| POST   | `/api/logout/`          | Logout (blacklist refresh token)|

### 📝 Notes (Protected)

| Method | Endpoint       | Description              |
|--------|----------------|--------------------------|
| GET    | `/api/notes/`  | Get all user's notes     |
| POST   | `/api/notes/`  | Create a new note        |

> ⚠️ All `/notes/` routes require JWT authentication.

---

## 🧪 Postman Testing Guide

### 🔧 Base URL
```
http://127.0.0.1:8000/api/
```

### 🌐 Set Headers for Protected Routes
```http
Authorization: Bearer {{accessToken}}
Content-Type: application/json
```

### 📌 Register
- **POST** `/register/`
```json
{
  "username": "john",
  "password": "mypassword123"
}
```

### 📌 Login
- **POST** `/login/`
```json
{
  "username": "john",
  "password": "mypassword123"
}
```
**Response:**
```json
{
  "refresh": "<refresh_token>",
  "access": "<access_token>"
}
```

> Save `access_token` in Postman environment as `accessToken`

### 🔄 Refresh Token
- **POST** `/token/refresh/`
```json
{
  "refresh": "<your_refresh_token>"
}
```

### 🚪 Logout (Blacklist Token)
- **POST** `/logout/`
```json
{
  "refresh": "<your_refresh_token>"
}
```

### 📝 Create Note
- **POST** `/notes/`
```json
{
  "title": "Shopping List",
  "content": "Milk, Bread, Eggs"
}
```

### 📄 Get Notes
- **GET** `/notes/`

**Returns:**
```json
[
  {
    "id": 1,
    "user": 1,
    "title": "Shopping List",
    "content": "Milk, Bread, Eggs",
    "created_at": "2025-06-30T18:30:00Z"
  }
]
```

---


## ✅ Postman Environment Setup (Optional)

Create a Postman environment named **JWT Notes API** with the following variable:
| Variable     | Initial Value             |
|--------------|----------------------------|
| `baseUrl`    | `http://127.0.0.1:8000/api` |
| `accessToken`| _(Set after login)_         |

Use the variable in endpoints like:
```
{{baseUrl}}/register/
Authorization: Bearer {{accessToken}}
```


---

## 📜 License

This project is licensed under the MIT License.

---

## 👨‍💻 Author

Made with ❤️ by [Lakshay](https://github.com/lakshaycodes)
