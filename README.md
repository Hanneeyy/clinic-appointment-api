# Clinic Appointment API

This project is a simple Clinic Appointment API built using FastAPI and Docker.

## Laboratory Context

This project was developed in an offline Windows 11 laboratory environment.

Python was not installed directly on the computer. The application was executed using Docker and a
prebuilt Docker image named clinic-fastapi-base:1.0.

## Features

- Create clinic appointments
- View all appointments
- View one appointment
- Update appointment details
- Cancel appointments
- Bearer token authentication for protected endpoints

## Technologies Used

- Python
- FastAPI
- Docker
- Git

## How to Run

```bash
docker compose up --build
```

Open http://localhost:8000/docs.

## Authentication

### Test Account

- **Username:** admin
- **Password:** clinic123
- **Token:** clinic-secret-token

### Login Endpoint

Send a POST request to `/login` with your credentials to obtain a bearer token.

### Protected Endpoints

The following endpoints require bearer token authentication:

- `GET /me` - View current user
- `GET /appointments` - View all appointments
- `GET /appointments/{appointment_id}` - View one appointment
- `POST /appointments` - Create appointment
- `PUT /appointments/{appointment_id}` - Update appointment
- `DELETE /appointments/{appointment_id}` - Cancel appointment

### Public Endpoints

These endpoints do not require authentication:

- `GET /` - Welcome message
- `POST /login` - Obtain access token

### How to Use

1. Log in at `/login` using the test account credentials
2. Copy the returned `access_token`
3. In Swagger UI, click **Authorize** and paste the token
4. Test protected endpoints

### Educational Limitations
 
This is just for learning. The username, password, and token are hardcoded in the code. Tokens never expire. There's no real security. A real app needs password hashing, a database, HTTPS, and token expiration.

### Why No Logout Endpoint?

There's no logout endpoint in this API because it uses stateless bearer tokens. Once you get a token, the server doesn't track it. The token is valid as long as you send it in the header.

To "logout", just stop sending the token. The server has no way to know if the token is still being used or not.

**In production**, logout works differently:
1. Server keeps a "blacklist" of logged-out tokens
2. When you logout, your token gets added to the blacklist
3. On every request, the server checks if the token is blacklisted
4. If it's blacklisted, the request is rejected

Or they use token expiration - tokens automatically expire after 15 minutes, so you can't use an old token forever.