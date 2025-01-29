# MERN Stack Admin Dashboard

## Overview
A full-featured admin dashboard with advanced image handling, role-based authentication, and comprehensive data management.

## Tech Stack

### Frontend
- React.js 18 with Vite
- Tailwind CSS
- React Router v6
- React Icons
- React Toastify
- Context API
- Swiper.js
- Base64 image encoding/decoding

### Backend
- Node.js & Express.js
- MongoDB with Mongoose
- JWT authentication
- Bcrypt for password hashing
- Multer for file handling
- Cloudinary SDK
- Express-validator

## Core Features

### Authentication & Authorization
- Multi-role user system (Admin/Moderator/User)
- JWT-based session management
- Secure password hashing
- Protected routes

### Admin Features
- Dashboard with statistics
- User management (CRUD)
- Service management
- Contact form submissions
- File management
- Query handling

### User Features
- Profile management
- File uploads
- Service browsing
- Contact submission
- Security settings

## Environment Variables

### Frontend (.env)
```env
VITE_BASE_URL=http://localhost:5000/api/
VITE_CLOUD_NAME=your_cloudinary_cloud_name
VITE_UPLOAD_PRESET=your_upload_preset
VITE_API_KEY=your_cloudinary_api_key
```

### Backend (.env)
```env
PORT=5000
MONGODB_URI=mongodb+srv://your_connection_string
JWT_SECRET=your_jwt_secret
SALT_ROUNDS=10
CLOUD_NAME=your_cloudinary_name
API_KEY=your_cloudinary_api_key
API_SECRET=your_cloudinary_api_secret
MAX_FILE_SIZE=5242880
ALLOWED_FILE_TYPES=jpeg,jpg,png,gif
```

## API Routes Documentation

### Authentication Routes
```
POST /api/auth/register       - Register new user
POST /api/auth/login         - User login
GET /api/auth/logout         - User logout
GET /api/auth/user          - Get user profile
PATCH /api/auth/update-password - Update password
PATCH /api/auth/update-email    - Update email
PATCH /api/auth/update-phone    - Update phone
```

### Admin Routes
```
# User Management
GET /api/admin/users         - Get all users
GET /api/admin/users/:id     - Get single user
POST /api/admin/users/add    - Add new user
PATCH /api/admin/users/update/:id - Update user
DELETE /api/admin/users/delete/:id - Delete user

# Service Management
GET /api/admin/services      - Get all services
POST /api/admin/services/add - Add new service
PATCH /api/admin/services/update/:id - Update service
DELETE /api/admin/services/delete/:id - Delete service

# Contact Management
GET /api/admin/contacts      - Get all contacts
GET /api/admin/contacts/:id  - Get single contact
GET /api/admin/contacts/count - Get contacts count
```

### Service Routes
```
GET /api/services           - Get all services
GET /api/services/:id       - Get single service
POST /api/services         - Create service
PATCH /api/services/:id    - Update service
DELETE /api/services/:id   - Delete service
```

### File Routes
```
POST /api/file/upload      - Upload file
GET /api/file/files        - Get all files
DELETE /api/file/:id       - Delete file
POST /api/file/service-image - Upload service image
```

## Project Structure
```
project/
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Layouts/
│   │   │   │   ├── components/
│   │   │   │   │   ├── AdminSidebar.jsx
│   │   │   │   │   ├── QueryApprove.jsx
│   │   │   │   │   └── QueryPending.jsx
│   │   │   │   └── Pages/
│   │   │   │       ├── Admin-AddService.jsx
│   │   │   │       ├── Admin-AddUsers.jsx
│   │   │   │       ├── Admin-ContactView.jsx
│   │   │   │       ├── Admin-Contacts.jsx
│   │   │   │       ├── Admin-Queries.jsx
│   │   │   │       ├── Admin-ServiceUpdate.jsx
│   │   │   │       ├── Admin-Services.jsx
│   │   │   │       ├── Admin-Update.jsx
│   │   │   │       └── Admin-Users.jsx
│   │   │   └── Navbar.jsx
│   │   ├── pages/
│   │   │   ├── About.jsx
│   │   │   ├── Contact.jsx
│   │   │   ├── Home.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── Profile.jsx
│   │   │   ├── Security.jsx
│   │   │   ├── Services.jsx
│   │   │   └── SingleService.jsx
│   │   ├── store/
│   │   │   └── Auth.jsx
│   │   └── App.jsx
├── server/
│   ├── Controllers/
│   │   ├── admin-controller.js
│   │   ├── auth-controller.js
│   │   └── service-controller.js
│   ├── Models/
│   │   ├── contact-model.js
│   │   ├── image-model.js
│   │   ├── service-model.js
│   │   └── user-model.js
│   ├── Routes/
│   │   ├── admin-router.js
│   │   ├── auth-router.js
│   │   └── service-route.js
│   ├── Middleware/
│   │   ├── auth-middleware.js
│   │   ├── error-middleware.js
│   │   └── validate-middleware.js
│   └── server.js
```

## Installation & Setup

1. **Clone Repository**
```bash
git clone <repository-url>
cd MERN-Stack-project
```

2. **Install Dependencies**
```bash
# Frontend
cd client
npm install

# Backend
cd ../server
npm install
```

3. **Run Application**
```bash
# Backend
cd server
npm run dev

# Frontend
cd client
npm run dev
```

## Features Implementation

### Authentication System
```javascript
// User Authentication Flow
1. JWT-based authentication
2. Role-based access (Admin/Moderator/User)
3. Password hashing with bcrypt
4. Token validation middleware
5. Protected routes
```

### Admin Dashboard Features
1. **User Management**
   - CRUD operations for users
   - Role assignment
   - Profile management
   - Activity tracking

2. **Service Management**
   - Service creation and editing
   - Image upload integration
   - Service categorization
   - Pricing management

3. **Query System**
   - Status tracking (Approved/Pending)
   - File attachment handling
   - User request management
   - Response system

### Image Handling System

1. **Cloudinary Integration**
```javascript
// Image Upload Configuration
const cloudinary = require('cloudinary').v2;
cloudinary.config({
  cloud_name: process.env.CLOUD_NAME,
  api_key: process.env.API_KEY,
  api_secret: process.env.API_SECRET
});
```

2. **File Upload Implementations**
```javascript
// Multiple Upload Methods
- Direct file upload
- Base64 image conversion
- URL-based image handling
- Image optimization
```

## Database Models

### User Model
- username: String (required)
- email: String (unique, required)
- password: String (required)
- phone: String
- role: String (enum: ['admin', 'moderator', 'user'])
- avatar: String
- privateNote: String

### Service Model
- name: String (required)
- description: String (required)
- price: Number
- image: String
- provider: String

### Contact Model
- name: String (required)
- email: String (required)
- message: String (required)
- phone: String
- createdAt: Date

### Image Model
```javascript
{
  firstName: String,
  lastName: String,
  email: String,
  personalDetails: String,
  city: String,
  province: String,
  country: String,
  image: {
    public_id: String,
    url: String
  },
  userId: ObjectId (ref: 'User'),
  timestamps: true
}
```

## Security Implementation
- Password hashing using bcrypt
- JWT token authentication
- Protected API routes
- Role-based access control
- Input validation and sanitization
- Secure file upload handling

## Error Handling
- Global error middleware
- Custom error responses
- Request validation
- File upload restrictions

## Image Handling

### Cloudinary Integration
```javascript
// Cloudinary Configuration
cloudinary.config({
  cloud_name: process.env.CLOUD_NAME,
  api_key: process.env.API_KEY,
  api_secret: process.env.API_SECRET
});

// Upload Function
const uploadImage = async (file) => {
  return await cloudinary.uploader.upload(file, {
    folder: 'your_folder',
    resource_type: 'auto'
  });
};
```

### Base64 Image Handling
```javascript
// Convert to Base64
const toBase64 = file => new Promise((resolve, reject) => {
  const reader = new FileReader();
  reader.readAsDataURL(file);
  reader.onload = () => resolve(reader.result);
  reader.onerror = error => reject(error);
});

// Server-side Base64 handling
const handleBase64Upload = async (base64String) => {
  const uploadResponse = await cloudinary.uploader.upload(base64String, {
    resource_type: "auto"
  });
  return uploadResponse.secure_url;
};
```

## MongoDB Data Models

### User Schema
```javascript
const userSchema = new mongoose.Schema({
  username: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  role: { type: String, enum: ['admin', 'moderator', 'user'] },
  avatar: { type: String },
  privateNote: { type: String }
}, { timestamps: true });
```

### Service Schema
```javascript
const serviceSchema = new mongoose.Schema({
  name: { type: String, required: true },
  description: { type: String, required: true },
  price: Number,
  image: String,
  provider: String
}, { timestamps: true });
```

## MongoDB Operations

### Connection Setup
```javascript
mongoose.connect(process.env.MONGODB_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
  useCreateIndex: true
});
```

### Common Operations
```javascript
// Create
const doc = new Model(data);
await doc.save();

// Read
const items = await Model.find(query).sort({ createdAt: -1 });

// Update
await Model.findByIdAndUpdate(id, update, { new: true });

// Delete
await Model.findByIdAndDelete(id);

// Aggregation
const stats = await Model.aggregate([
  { $group: { _id: '$category', total: { $sum: 1 } } }
]);
```

## Image Upload Implementation

### Frontend Upload Component
```jsx
const ImageUpload = () => {
  const handleUpload = async (file) => {
    const base64 = await toBase64(file);
    const formData = new FormData();
    formData.append('file', base64);
    
    const response = await fetch('/api/file/upload', {
      method: 'POST',
      body: formData
    });
    return response.json();
  };
};
```

### Backend Upload Handler
```javascript
const upload = multer({
  storage: multer.memoryStorage(),
  limits: {
    fileSize: process.env.MAX_FILE_SIZE
  },
  fileFilter: (req, file, cb) => {
    const allowedTypes = process.env.ALLOWED_FILE_TYPES.split(',');
    const isAllowed = allowedTypes.includes(file.mimetype.split('/')[1]);
    cb(null, isAllowed);
  }
});
```

## Error Handling
```javascript
const errorHandler = (err, req, res, next) => {
  console.error(err.stack);
  res.status(err.status || 500).json({
    success: false,
    message: err.message || 'Internal Server Error'
  });
};
```

## Security Implementations
- CORS configuration
- Rate limiting
- XSS protection
- Helmet security headers
- Input sanitization
- File type validation
- Size restrictions

## Contributing
Mian Ali Khalid

## License
MIT License
