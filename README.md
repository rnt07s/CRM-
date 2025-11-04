# CRM System for Student Enquiries

A Customer Relationship Management (CRM) system designed for educational institutions to manage student enquiries and counselor interactions. Built with Node.js, Express, and MongoDB.

## Features

- 🔐 Employee/Counselor Authentication
- 📝 Public Enquiry Form
- 👥 Public & Private Lead Management
- 🔄 Lead Claiming System
- 🎯 Course Interest Tracking

## Tech Stack

- Backend: Node.js + Express.js
- Database: MongoDB
- Authentication: JWT (JSON Web Tokens)
- Security: bcrypt for password hashing

## Project Structure

```
server/
├── app.js              # Express app configuration
├── server.js           # Server entry point
├── config/
│   └── db.js          # Database configuration
├── controllers/
│   ├── authController.js    # Authentication logic
│   └── enquiryController.js # Enquiry management logic
├── middleware/
│   └── authMiddleware.js    # JWT authentication middleware
├── models/
│   ├── Employee.js         # Employee schema
│   └── Enquiry.js         # Enquiry schema
├── routes/
│   ├── authRoutes.js      # Authentication routes
│   └── enquiryRoutes.js   # Enquiry routes
└── utils/
    └── generateToken.js    # JWT token generation
```

## Setup & Installation

1. Clone the repository
   ```bash
   git clone [repository-url]
   cd [repository-name]
   ```

2. Install dependencies
   ```bash
   cd server
   npm install
   ```

3. Set up environment variables
   Create a `.env` file in the server directory with:
   ```
   MONGO_URI=your_mongodb_connection_string
   JWT_SECRET=your_jwt_secret
   PORT=5000
   ```

4. Start the server
   ```bash
   npm start
   ```

## API Documentation

### Authentication Endpoints

#### Register Employee
- **POST** `/api/auth/register`
- Public route
- Request body:
  ```json
  {
    "name": "Counselor Name",
    "email": "counselor@example.com",
    "password": "securepassword"
  }
  ```

#### Login Employee
- **POST** `/api/auth/login`
- Public route
- Request body:
  ```json
  {
    "email": "counselor@example.com",
    "password": "securepassword"
  }
  ```

### Enquiry Endpoints

#### Submit Public Enquiry
- **POST** `/api/enquiries/public`
- Public route
- Request body:
  ```json
  {
    "name": "Student Name",
    "email": "student@example.com",
    "phone": "1234567890",
    "courseInterest": "Computer Science"
  }
  ```

#### Get Unclaimed Enquiries
- **GET** `/api/enquiries/unclaimed`
- Protected route (requires JWT)

#### Claim an Enquiry
- **POST** `/api/enquiries/claim/:id`
- Protected route (requires JWT)

#### Get My Claimed Enquiries
- **GET** `/api/enquiries/my`
- Protected route (requires JWT)

## Authentication

The system uses JWT (JSON Web Tokens) for authentication. To access protected routes:
1. Login to receive a JWT token
2. Include the token in the Authorization header:
   ```
   Authorization: Bearer your_jwt_token
   ```

## Business Logic

1. Each counselor has their own CRM account linked to their email
2. Public enquiry form can be:
   - Shared online for lead capture
   - Used by counselors after initial student contact
3. All counselors can view unclaimed enquiries
4. Once claimed, an enquiry becomes private to the claiming counselor

## Error Handling

The API includes comprehensive error handling for:
- Invalid credentials
- Duplicate email registration
- Missing required fields
- Invalid JWT tokens
- Unauthorized access attempts

## Security Features

- Password hashing using bcrypt
- JWT-based authentication
- Protected routes middleware
- Email validation
- Mongoose schema validation

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## License

[MIT License](LICENSE)