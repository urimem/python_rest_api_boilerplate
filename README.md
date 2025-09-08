# Full-Stack FastAPI + Next.js Authentication Boilerplate

A complete full-stack application with FastAPI backend and Next.js frontend, featuring JWT authentication with httpOnly refresh tokens.

## Project Structure

```
├── main.py              # FastAPI backend server
├── requirements.txt     # Python dependencies
├── frontend/           # Next.js frontend application
│   ├── src/
│   │   ├── app/        # Next.js app router pages
│   │   ├── components/ # React components
│   │   ├── contexts/   # React context providers
│   │   └── lib/        # API client utilities
│   ├── package.json    # Node.js dependencies
│   └── ...
└── .venv/              # Python virtual environment
```

## Features

### Backend (FastAPI)
- JWT access tokens (30 minutes expiry)
- HttpOnly refresh tokens (7 days expiry)
- Secure cookie handling
- CORS support
- Password hashing with bcrypt
- Protected API endpoints

### Frontend (Next.js)
- Modern React with TypeScript
- Tailwind CSS for styling
- JWT token management
- Automatic token refresh
- Protected routes
- Clean authentication flow

## Quick Start

### 1. Backend Setup

```bash
# Setup Python virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Install Python dependencies
pip install -r requirements.txt

# Start FastAPI server
python main.py
```

### 2. Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install Node.js dependencies
npm install

# Start Next.js development server
npm run dev
```

### 3. Access the Application

- **Frontend:** http://localhost:3000
- **Backend API:** http://localhost:8000
- **API Documentation:** http://localhost:8000/docs

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

## How to Use

1. **Visit the Frontend:** Go to http://localhost:3000
2. **Login:** Use the demo credentials:
   - Username: `testuser`
   - Password: `secret123`
3. **Dashboard:** After login, you'll see the dashboard with:
   - User information display
   - "Fetch Users" button to test protected API calls
   - Logout functionality

## API Usage Example (cURL)

```bash
# Login via API
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

- **JWT Access Tokens:** Short-lived (30 min), stored in memory on frontend
- **Refresh Tokens:** Long-lived (7 days), stored as httpOnly cookies
- **Automatic Token Refresh:** Seamless token renewal on expiration
- **CORS Configuration:** Properly configured for cross-origin requests
- **Secure Cookies:** httpOnly, secure, sameSite flags enabled
- **Password Hashing:** bcrypt for secure password storage
- **Protected Routes:** Both frontend and backend route protection

## Technology Stack

### Backend
- **FastAPI** - Modern Python web framework
- **Uvicorn** - ASGI server
- **python-jose** - JWT token handling
- **passlib** - Password hashing
- **bcrypt** - Secure password encryption

### Frontend
- **Next.js 15** - React framework with App Router
- **TypeScript** - Type-safe JavaScript
- **Tailwind CSS** - Utility-first CSS framework
- **Axios** - HTTP client with interceptors
- **React Context** - State management for authentication

## Development

Both servers support hot reload during development:
- FastAPI automatically reloads on Python file changes
- Next.js automatically reloads on frontend file changes

## Production Considerations

Before deploying to production:

1. **Update SECRET_KEY** in `main.py` with a secure random key
2. **Configure CORS** origins for your production domain
3. **Set up HTTPS** for secure cookie transmission
4. **Use environment variables** for sensitive configuration
5. **Set up proper logging** and error monitoring