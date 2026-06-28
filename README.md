# 🤝 Community Resource Sharing Platform (Phase 1)

Welcome to the **Community Resource Sharing Platform (Phase 1)**! This is a full-stack web application designed to foster local neighborhood connection, collaboration, and sustainability. 

The platform allows residents to:
- **Share Physical Resources:** List items like tools, books, or electronics that others can borrow.
- **Offer Skills & Services:** Advertise capabilities like tutoring, home maintenance, or technical support to help neighbors.
- **Connect & Request:** Request to borrow items or sign up for skill assistance in real-time.

---

## 🚀 Tech Stack

### Frontend
- **Framework:** React 19 (via Vite)
- **Styling:** TailwindCSS (v3), PostCSS
- **Routing:** React Router DOM (v7)
- **Icons:** Lucide React
- **API Client:** Axios

### Backend
- **Runtime:** Node.js (Express framework)
- **Database ODM:** Mongoose (MongoDB)
- **Security:** bcryptjs (password hashing), JSON Web Tokens (JWT) for authentication
- **Development Tool:** Nodemon

---

## ✨ Features

- **🔒 User Authentication:** Secure registration and login using encrypted passwords (bcryptjs) and JWT session tokens.
- **🛠️ Resource Management:**
  - Create, view, update, and delete resource listings.
  - Set category (`Tools`, `Books`, `Equipment`, `Electronics`, `Educational`, `Other`).
  - Track availability (`Available`, `Requested`, `Borrowed`).
  - Send and manage borrow requests.
- **🎓 Skill Sharing Board:**
  - Post skill profiles (`Tutoring`, `Technical Support`, `Home Maintenance`, `Mentorship`, `Other`).
  - Define availability details.
  - Send custom assistance requests.
  - Manage requests (`Pending`, `Accepted`, `Declined`).
- **📱 Responsive UI:** Clean, modern, responsive interface styled with TailwindCSS.

---

## 📁 Directory Structure

```text
phase1-resource-sharing/
├── backend/
│   ├── config/             # Database connection setup
│   ├── middleware/         # Auth verification middleware
│   ├── models/             # Mongoose schemas (User, Resource, Skill)
│   ├── routes/             # Express API endpoints
│   ├── .env                # Backend environment config (Ignored by git)
│   ├── server.js           # Server entrypoint
│   └── package.json
├── frontend/
│   ├── public/             # Static public assets
│   ├── src/
│   │   ├── assets/         # App images and logos
│   │   ├── components/     # Reusable UI components (Navbar, etc.)
│   │   ├── context/        # React Auth Context for global state
│   │   ├── pages/          # Page views (Feed, Login, Register, Profile, etc.)
│   │   ├── App.css
│   │   ├── App.jsx         # App routing setup
│   │   ├── index.css       # Tailwind directives
│   │   └── main.jsx        # React entrypoint
│   ├── tailwind.config.js
│   ├── vite.config.js
│   └── package.json
└── documentation/          # Database schemas and API/Postman docs
```

---

## 🛠️ Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (v16 or higher)
- [MongoDB](https://www.mongodb.com/) (running locally or a MongoDB Atlas URI)

---

### Step-by-Step Installation

#### 1. Clone the Repository & Navigate to Phase 1
```bash
git clone https://github.com/Ishika0424/Phase1-Community-Resource-Sharing-Platform.git
cd Phase1-Community-Resource-Sharing-Platform
```

#### 2. Backend Setup
Navigate to the `backend` folder:
```bash
cd backend
```

Install dependencies:
```bash
npm install
```

Create a `.env` file in the `backend` folder and populate it:
```env
PORT=5001
MONGO_URI=mongodb://127.0.0.1:27017/community_phase1
JWT_SECRET=your_jwt_secret_key_here
```

Start the backend server in development mode:
```bash
npm run dev
```
*The server will start running on `http://localhost:5001`.*

---

#### 3. Frontend Setup
Open a new terminal window, and navigate to the `frontend` folder:
```bash
cd ../frontend
```

Install dependencies:
```bash
npm install
```

Start the Vite development server:
```bash
npm run dev
```
*The frontend application will start running on `http://localhost:5173`.*

---

## 🔌 API Endpoints (Phase 1)

### Authentication (`/api/auth`)
- `POST /api/auth/register` - Register a new resident user.
- `POST /api/auth/login` - Authenticate user and receive JWT.
- `GET /api/auth/me` - Get current logged-in user profile (Requires Authorization Header).

### Resource Management (`/api/resources`)
- `GET /api/resources` - Get all listed resources.
- `POST /api/resources` - Add a new resource listing (Auth required).
- `PUT /api/resources/:id` - Update a resource (Auth required, owner only).
- `DELETE /api/resources/:id` - Delete a resource (Auth required, owner only).
- `POST /api/resources/:id/request` - Request to borrow a resource.

### Skill Sharing (`/api/skills`)
- `GET /api/skills` - Get all skill postings.
- `POST /api/skills` - Post a new skill offering (Auth required).
- `PUT /api/skills/:id` - Update skill posting (Auth required, owner only).
- `DELETE /api/skills/:id` - Delete skill posting (Auth required, owner only).
- `POST /api/skills/:id/request` - Send assistance request to owner.
- `PUT /api/skills/:id/request/:requestId` - Accept or decline a help request.

---

## 🔒 Security Best Practices
- Environment configuration parameters (such as `JWT_SECRET` and `MONGO_URI`) are located inside `backend/.env` which is configured in `.gitignore` so they are never leaked online.
- Password hashes are stored safely using `bcryptjs` encryption.
- Direct API routes for posting and editing require a valid JSON Web Token (`x-auth-token` or `Bearer Token`).