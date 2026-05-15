# WorkSync — Team Task Management App

Worksync is a robust, full-stack team task management application built using the MERN stack. It features role-based access control (RBAC), project administration, task tracking, and dynamic dashboards designed for high productivity.

## 🚀 Features

- **Authentication & Security:** Secure JWT-based authentication via HTTP-only cookies.
- **Role-Based Access Control (RBAC):** Distinct `ADMIN` and `MEMBER` roles ensure that only authorized users can create projects, assign tasks, or manage team members.
- **Project Management:** Admins can create projects, update details, and add or remove team members.
- **Task Tracking:** 
  - Admins can create tasks, assign them to project members, set priorities, and establish due dates.
  - Members can view their assigned tasks and securely update task statuses (`TODO`, `IN_PROGRESS`, `DONE`).
- **Dynamic Dashboard:** A centralized overview displaying key metrics: total projects, total/pending/completed tasks, recent activities, and a highlighted list of overdue tasks requiring immediate attention.
- **Responsive UI:** Built with React and Tailwind CSS, featuring a beautiful, dark-themed, premium UI with smooth loading states, inline validations, and contextual empty states.

## 🛠️ Tech Stack

### Frontend
- **Framework:** React.js (Vite)
- **Routing:** React Router DOM v6
- **Styling:** Tailwind CSS
- **Form Handling:** React Hook Form
- **Validation:** Zod
- **HTTP Client:** Axios (with interceptors for auth)
- **Toast Notifications:** React Hot Toast

### Backend
- **Framework:** Node.js, Express.js
- **Database:** MongoDB (Mongoose)
- **Authentication:** JSON Web Tokens (JWT), bcryptjs
- **Validation:** express-validator
- **Security:** HTTP-only cookies, Helmet, CORS

## 📁 Architecture & Folder Structure

The application strictly adheres to a clean architecture with clear separation of concerns:

```
├── backend/
│   ├── src/
│   │   ├── config/       # Database & environment configurations
│   │   ├── constants/    # Centralized enums (ROLES)
│   │   ├── controllers/  # Thin controllers handling req/res routing
│   │   ├── middlewares/  # Auth, Validation, and Global Error handlers
│   │   ├── models/       # Mongoose Schemas (User, Project, Task)
│   │   ├── routes/       # Express Route definitions
│   │   ├── services/     # Heavy business logic and database interactions
│   │   ├── utils/        # Async handlers, ApiError wrappers
│   │   └── app.js & server.js
├── frontend/
│   ├── src/
│   │   ├── api/          # Axios instance configuration
│   │   ├── components/   # Reusable UI elements (Cards, Forms, Badges)
│   │   ├── constants/    # Frontend enums matching backend
│   │   ├── context/      # React Context (AuthContext)
│   │   ├── layouts/      # Dashboard Sidebar & Shell
│   │   ├── pages/        # Main view components (Dashboard, Projects, Tasks, Auth)
│   │   └── routes/       # Protected & Public route guards
```

## ⚙️ Installation & Setup

### Prerequisites
- Node.js (v18+ recommended)
- MongoDB running locally or a MongoDB Atlas URI.

### 1. Clone the repository
```bash
git clone <repository-url>
cd <project-folder>
```

### 2. Backend Setup
```bash
cd backend
npm install
```
Create a `.env` file in the `backend/` directory:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/task-manager
JWT_SECRET=your_super_secret_jwt_key
JWT_EXPIRE=30d
NODE_ENV=development
CLIENT_URL=http://localhost:5173
```
Start the backend server:
```bash
npm run dev
```

### 3. Frontend Setup
Open a new terminal window:
```bash
cd frontend
npm install
```
Start the Vite development server:
```bash
npm run dev
```

The application will be running at `http://localhost:5173`.

## 🌐 API Overview

| Route | Method | Description | Access |
|---|---|---|---|
| `/api/auth/signup` | POST | Register new user (defaults to `MEMBER`) | Public |
| `/api/auth/login` | POST | Authenticate user & issue cookie | Public |
| `/api/auth/logout` | POST | Clear auth cookie | Public |
| `/api/auth/me` | GET | Retrieve currently authenticated user | Protected |
| `/api/projects` | GET | List all accessible projects | Protected |
| `/api/projects` | POST | Create a new project | Admin Only |
| `/api/projects/:id` | GET | Get project details | Project Members / Admin |
| `/api/tasks` | POST | Create a new task | Admin Only |
| `/api/tasks/:id` | PATCH | Update task status (or full task) | Assignee / Admin |
| `/api/dashboard` | GET | Retrieve aggregated dashboard statistics | Protected |

## 🚀 Deployment Instructions

### Backend (e.g., Railway / Render)
1. Provision a MongoDB Atlas cluster and get the connection string.
2. Deploy the `backend/` folder.
3. Set the production environment variables: `PORT`, `MONGODB_URI`, `JWT_SECRET`, and `CLIENT_URL` (pointing to your deployed frontend).
4. Build Command: `npm install`
5. Start Command: `node src/server.js`

### Frontend (e.g., Vercel / Netlify)
1. Deploy the `frontend/` folder.
2. Set the build command to `npm run build` and publish directory to `dist`.
3. In `frontend/vite.config.js`, ensure requests to `/api` are handled properly, or hardcode the production `baseURL` in `frontend/src/api/axios.js` to point to your live backend API URL instead of relative `/api`.

---

*TaskFlow — Elevating team productivity through clean architecture and intuitive design.*
