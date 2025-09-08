# FastAPI JWT Authentication Boilerplate

A FastAPI REST API with JWT authentication using httpOnly refresh tokens.

## Features

- JWT access tokens (30 minutes expiry)
- HttpOnly refresh tokens (7 days expiry)
- Secure cookie handling
- CORS support
- Two sample protected endpoints
- Password hashing with bcrypt

## Quick Start

1. **Setup virtual environment:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

2. **Install dependencies:**
```bash
pip install -r requirements.txt
```

3. **Run the server:**
```bash
python main.py
```

The API will be available at `http://localhost:8000`

## API Endpoints

### Authentication
- `POST /auth/login` - Login with username/password
- `POST /auth/refresh` - Refresh access token using httpOnly cookie
- `POST /auth/logout` - Logout (clears refresh token cookie)
- `GET /auth/me` - Get current user info

### Protected Endpoints
- `GET /api/users` - Get list of users (requires JWT)
- `GET /api/products` - Get list of products (requires JWT)

## Test User

- Username: `testuser`
- Password: `secret123`

## Usage Example

```bash
# Login
curl -X POST "http://localhost:8000/auth/login" \
     -H "Content-Type: application/json" \
     -d '{"username": "testuser", "password": "secret123"}' \
     -c cookies.txt

# Use the returned access_token in Authorization header
curl -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
     "http://localhost:8000/api/users"

# Refresh token (uses httpOnly cookie)
curl -X POST "http://localhost:8000/auth/refresh" \
     -b cookies.txt
```

## Security Features

- Access tokens stored in memory (frontend)
- Refresh tokens in httpOnly cookies
- CORS configured for localhost:3000
- Secure cookie settings (httpOnly, secure, sameSite)
- Password hashing with bcrypt
- JWT expiration handling