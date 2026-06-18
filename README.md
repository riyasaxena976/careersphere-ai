# Smart CareerSphere AI – Your Personal Career Coach 🚀

Smart CareerSphere AI is a complete production-grade MERN Stack web application designed to serve as an AI-powered career coach. Users can upload their resumes in PDF format, calculate real-time ATS scores, compare their experience against target job descriptions, discover missing skills, generate structured career roadmaps, simulate mock interviews question-by-question, and receive detailed qualitative feedback from the AI coach.

---

## Key Features

1. **Secure JWT Authentication**:
   - Register, login, and profile validation using secure bcrypt hashing and JWT tokens.
   - Built-in System Admin Dashboard to check global stats (Total Users, Resumes, Mock Interviews, AI Requests) and manage user accounts cascadingly.

2. **Resume ATS Analyzer**:
   - Direct PDF file uploading with automated text extraction.
   - Core keyword extraction, parsing of projects, education, and bullet-point assessments highlighting candidate strengths and flags/weaknesses.

3. **Job Description Matching**:
   - Compare resume text against any pasted job requirements.
   - Return visual match percentages, matched skills, missing skills, and step-by-step improvements.

4. **Career Roadmap Engine**:
   - Identify skills gaps based on target profiles.
   - Generate multi-phase roadmap milestones and suggest curated learning resources (courses, documentation, tutorials).

5. **AI Mock Interview Simulator**:
   - Generate 10 tailored interview questions covering Technical, Behavioral, HR, and Project Based topics.
   - Interactive chat simulator allowing candidates to submit answers one-by-one.
   - Evaluation breakdown covering Technical Knowledge, Communication, Problem Solving, and Confidence with individual question feedback.

---

## Tech Stack

- **Frontend**: React.js, Vite, Tailwind CSS (v3), Recharts, Lucide React, React Hot Toast
- **Backend**: Node.js, Express.js, Mongoose, Multer (Memory Storage), PDF-Parse, Groq SDK
- **Database**: MongoDB Atlas
- **AI Models**: Groq Llama-3.3-70b-versatile (API-key optional, includes automated Mock fallbacks!)

---

## Folder Structure

```text
smart-careersphere-ai/
 ├── backend/
 │    ├── config/          # Database configuration
 │    ├── controllers/     # Route handlers (auth, resume, match, interview, stats)
 │    ├── middleware/      # Auth protection and global error handling
 │    ├── models/          # User, Resume, JobMatch, and Interview Mongoose Schemas
 │    ├── routes/          # Express API endpoints mapping
 │    ├── services/        # PDF-Parse text parser and Groq AI prompts
 │    ├── server.js        # Server entry point
 │    └── .env.example     # Environment template
 ├── frontend/
 │    ├── src/
 │    │    ├── components/ # Header, Sidebar, ProtectedRoute wrappers
 │    │    ├── context/    # AuthContext states
 │    │    ├── pages/      # Landing, Login, Dashboard, Analyzer, Interview pages
 │    │    ├── services/   # Fetch client API wrapper
 │    │    ├── App.jsx     # Route router trees
 │    │    └── index.css   # Tailwind directives & glass panels styling
 │    ├── index.html       # Entry template
 │    └── tailwind.config.js
 └── README.md
```

---

## Quick Start Guide

### Prerequisites
Make sure you have [Node.js](https://nodejs.org/) (v16+) and [MongoDB](https://www.mongodb.com/try/download/community) (running locally or a MongoDB Atlas URI cluster) ready.

### 1. Configure the Backend
1. Open a terminal and navigate to the `backend/` directory:
   ```bash
   cd backend
   ```
2. Create your `.env` file from `.env.example`:
   ```bash
   cp .env.example .env
   ```
3. Edit the `.env` file with your credentials:
   - Provide your `MONGODB_URI` (defaults to local `mongodb://127.0.0.1:27017/careersphere`).
   - Provide your `GROQ_API_KEY`. *If left empty, the application falls back gracefully to Mock Mode allowing full user navigation!*
   - Set `ADMIN_SECRET_KEY` (e.g., `super_secret_admin_key_for_setup`) for admin registers.
4. Install dependencies and start server:
   ```bash
   npm install
   npm run dev
   ```
   *The backend server will launch on port 5000.*

### 2. Configure the Frontend
1. Open a separate terminal and navigate to the `frontend/` directory:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the development server:
   ```bash
   npm run dev
   ```
   *The frontend dev server will launch on port 3000, proxying all `/api` requests to the backend.*

---

## Deployment Instructions

### Frontend Deployment → Vercel
1. Install Vercel CLI globally: `npm install -g vercel` or link your repo to GitHub.
2. In the `frontend/` directory, create a `vercel.json` file to manage React routing fallbacks:
   ```json
   {
     "rewrites": [
       { "source": "/(.*)", "destination": "/index.html" }
     ]
   }
   ```
3. Run `vercel` and follow prompt instructions to deploy. Provide environment variable overrides if needed.

### Backend Deployment → Render
1. Create a Web Service on Render.
2. Link your GitHub repository.
3. Configure settings:
   - **Environment**: `Node`
   - **Build Command**: `cd backend && npm install`
   - **Start Command**: `cd backend && node server.js`
4. In Render's dashboard, navigate to **Environment** and add:
   - `MONGODB_URI`
   - `JWT_SECRET`
   - `GROQ_API_KEY`
   - `NODE_ENV=production`
   - `PORT=10000`
5. Click deploy. Render will yield a public backend URL. Make sure to update the frontend's API target URL when moving to production deployments.
