# PlacementHub — Campus Placement & Internship Management System

PlacementHub is a full-stack Web Application (MERN Stack) designed to streamline the campus recruitment process for educational institutes. It bridges the gap between **Students**, **Recruiters / Companies**, and the **Institute Placement Cell (TPO)** through role-based access control, eligibility filtering, application tracking, and recruiter verification workflows.

---

## 🚀 Key Features

### 🎓 1. Student Portal
* **Profile Management**: Build a comprehensive academic & professional profile (Roll Number, Branch, CGPA, 10th/12th percentage, Skills, Resume link, LinkedIn & GitHub profiles).
* **Eligibility-Based Opportunities**: Browse job & internship opportunities automatically filtered based on student's branch, CGPA, and deadline.
* **One-Click Application**: Apply directly to eligible job listings after completing profile setup.
* **Application Tracker**: Real-time status tracking for applied jobs (`Applied`, `Shortlisted`, `Selected`, `Rejected`).

### 💼 2. Recruiter Portal
* **Company Onboarding**: Register company details and HR contact information.
* **Verification Workflow**: Accounts remain in pending state until reviewed and approved by the Institute Placement Cell.
* **Job & Internship Posting**: Post detailed job/internship openings with specific eligibility criteria (Minimum CGPA, Target Branches, Stipend/CTC, Application Deadline).
* **Applicant Management**: View detailed applicant profiles for posted listings and update candidate hiring stages (`Shortlisted`, `Selected`, `Rejected`).
* **Active Status Control**: Toggle opportunities active/inactive as needed.

### 🏛️ 3. Institute / TPO Portal
* **Analytics Dashboard**: Real-time stats on total students, placement rate, active recruiters, pending approvals, and total selections.
* **Recruiter Verification**: Review and approve or reject newly registered recruiter profiles.
* **Student Directory**: View all registered students and their placement readiness.
* **Centralized Application Monitoring**: Oversee all student applications and recruitment progress across all companies.

---

## 🛠️ Tech Stack

### Frontend
* **Framework**: [React 18](https://react.dev/) + [Vite](https://vitejs.dev/)
* **Routing**: [React Router DOM v6](https://reactrouter.com/)
* **HTTP Client**: [Axios](https://axios-http.com/)
* **Styling**: Vanilla CSS (Modern CSS variables, Responsive Flexbox & Grid layouts)

### Backend
* **Runtime**: [Node.js](https://nodejs.org/)
* **Framework**: [Express.js](https://expressjs.com/)
* **Database**: [MongoDB](https://www.mongodb.com/) via [Mongoose ORM](https://mongoosejs.com/)
* **Authentication & Security**: Password hashing with `bcryptjs`, CORS middleware
* **Session Management**: Lightweight User ID passing with Axios request interceptors

---

## 📁 Project Structure

```
placementmanagement/
├── Backend/
│   ├── middleware/
│   │   └── auth.js          # Authentication & Role-based Access Control middleware
│   ├── models/
│   │   ├── User.js              # Central User collection (student, recruiter, institute)
│   │   ├── StudentProfile.js    # Academic & placement data for students
│   │   ├── RecruiterProfile.js  # Company profiles & verification status
│   │   ├── Opportunity.js       # Job and Internship postings
│   │   └── Application.js       # Student application tracking
│   ├── routes/
│   │   ├── auth.js              # Registration & Login routes
│   │   ├── student.js           # Student profiles, eligible opportunities & applications
│   │   ├── recruiter.js         # Recruiter profile, job postings & applicant management
│   │   ├── institute.js         # Institute dashboard stats, recruiter verification & reports
│   │   └── opportunity.js       # Public/Detail opportunity routes
│   ├── package.json
│   └── server.js                # Express app entry point & MongoDB connection
│
├── Frontend/
│   ├── src/
│   │   ├── api/
│   │   │   └── axios.js         # Pre-configured Axios instance with request interceptor
│   │   ├── components/
│   │   │   ├── Header.jsx       # Universal Navigation Bar
│   │   │   └── Sidebar.jsx      # Portal navigation sidebar
│   │   ├── context/
│   │   │   └── AuthContext.jsx   # Global React Auth Context (localStorage sync)
│   │   ├── pages/
│   │   │   ├── auth/            # Login & Register views
│   │   │   ├── student/         # Student Dashboard, Opportunities, Applications & Profile
│   │   │   ├── recruiter/       # Recruiter Dashboard, Post Job, Opportunities & Profiles
│   │   │   ├── institute/       # TPO Dashboard, Verification, Student & Recruiter lists
│   │   │   ├── HomePage.jsx     # Landing page
│   │   │   ├── AboutPage.jsx    # Project background & info
│   │   │   └── TeamPage.jsx     # Team information
│   │   ├── App.jsx              # App routing & protected route wrappers
│   │   ├── index.css            # Core design system & CSS styling
│   │   └── main.jsx             # React DOM root entry
│   ├── index.html
│   ├── package.json
│   └── vite.config.js           # Vite dev server configuration & API proxy
└── README.md
```

---

## ⚙️ Setup & Installation

### Prerequisites
* [Node.js](https://nodejs.org/) (v16.x or higher)
* [MongoDB](https://www.mongodb.com/try/download/community) running locally or a MongoDB Atlas connection URI.

### 1. Clone & Setup Backend

```bash
cd Backend
npm install
```

Create a `.env` file in the `Backend/` directory:
```env
PORT=5000
MONGO_URI=mongodb://localhost:27017/placementhub
```

Start the Backend Server:
```bash
# Development mode with live reload
npm run dev

# Production mode
npm start
```
*The server will run on `http://localhost:5000`.*

### 2. Setup Frontend

```bash
cd ../Frontend
npm install
```

Start the Vite Development Server:
```bash
npm run dev
```
*The frontend will run on `http://localhost:5173`.*

---

## 🔌 API Endpoints Summary

### Authentication (`/api/auth`)
* `POST /api/auth/register` — Register a new account (`student`, `recruiter`, `institute`)
* `POST /api/auth/login` — Authenticate existing user

### Student Routes (`/api/student`)
* `GET /api/student/profile` — Fetch student profile details
* `PUT /api/student/profile` — Update student profile
* `GET /api/student/opportunities` — View eligible open opportunities
* `POST /api/student/apply/:opportunityId` — Apply for an opportunity
* `GET /api/student/applications` — View student application history

### Recruiter Routes (`/api/recruiter`)
* `GET /api/recruiter/profile` — Fetch company profile
* `PUT /api/recruiter/profile` — Update company profile
* `POST /api/recruiter/opportunity` — Post new job/internship (Requires approval)
* `GET /api/recruiter/opportunities` — List posted opportunities
* `PATCH /api/recruiter/opportunity/:id/toggle` — Toggle opportunity status
* `GET /api/recruiter/opportunity/:id/applicants` — View applicants for an opportunity
* `PATCH /api/recruiter/application/:id/status` — Update candidate status (`shortlisted`, `selected`, `rejected`)

### Institute Routes (`/api/institute`)
* `GET /api/institute/stats` — Real-time placement metrics
* `GET /api/institute/recruiters` — View recruiter listings (filterable by status)
* `PATCH /api/institute/recruiter/:id/verify` — Approve or Reject recruiters
* `GET /api/institute/students` — View list of registered students
* `GET /api/institute/applications` — Monitor all applications platform-wide

---

## 📝 License

This project is open-source and available for educational and institutional placement management purposes.
