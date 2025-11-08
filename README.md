# 📚 Note Organizer

A modern, secure, and responsive full-stack web application for uploading and accessing academic notes organized by departments, years, and subjects.

## 🌟 Features

- **Department-wise Organization**: 10 engineering departments with year-wise classification
- **Theory & Lab Sections**: Separate organization for theory subjects and lab practicals
- **Unit-wise Notes**: Each subject organized into units (Unit 1-6)
- **Role-based Access**: Separate dashboards for teachers and students
- **Secure Authentication**: Firebase Authentication with email/password
- **Cloud Storage**: Reliable Firebase Storage for file uploads
- **Modern UI**: Clean white-blue theme with smooth animations
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile

## 🏗️ Architecture

### Tech Stack

**Frontend:**
- HTML5, CSS3, JavaScript (ES6+)
- Firebase SDK (Web)
- Responsive Design with CSS Grid & Flexbox

**Backend:**
- Node.js with Express.js
- Firebase Admin SDK
- Multer for file uploads

**Database & Storage:**
- Firebase Realtime Database
- Firebase Storage
- Firebase Authentication

## 📁 Project Structure

```
note-organizer/
├── frontend/
│   ├── index.html                    # Landing page
│   ├── login.html                    # Authentication page
│   ├── departments.html              # Departments browser
│   ├── dashboard_teacher.html        # Teacher dashboard
│   ├── dashboard_student.html        # Student dashboard
│   ├── css/
│   │   └── style.css                 # Main stylesheet
│   └── js/
│       └── main.js                   # Frontend logic
├── backend/
│   ├── server.js                     # Express server
│   ├── routes/
│   │   ├── auth.js                   # Authentication routes
│   │   └── notes.js                  # Notes CRUD routes
│   └── middleware/
│       └── verifyRole.js             # Role verification
├── config/
│   ├── firebaseConfig.js             # Firebase configuration
│   └── seedDatabase.js               # Database seeding script
├── .env.example                      # Environment variables template
├── package.json                      # Dependencies
└── README.md                         # This file
```

## 🚀 Setup Instructions

### Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Firebase account

### 1. Clone the Repository

```bash
cd note-organizer
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Firebase Setup

#### A. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" and follow the setup wizard
3. Enable **Authentication** (Email/Password provider)
4. Enable **Realtime Database** (Start in test mode for development)
5. Enable **Storage** (Start in test mode for development)

#### B. Get Firebase Credentials

**For Web App (Frontend):**
1. Go to Project Settings → General
2. Scroll down to "Your apps"
3. Click on Web icon `</>`
4. Register your app and copy the Firebase config

**For Admin SDK (Backend):**
1. Go to Project Settings → Service Accounts
2. Click "Generate new private key"
3. Download the JSON file

#### C. Configure Environment Variables

Create a `.env` file in the project root:

```bash
cp .env.example .env
```

Edit `.env` and add your Firebase credentials:

```env
# Firebase Admin SDK (from service account JSON)
FIREBASE_PROJECT_ID=your-project-id
FIREBASE_PRIVATE_KEY="-----BEGIN PRIVATE KEY-----\nYOUR_PRIVATE_KEY\n-----END PRIVATE KEY-----\n"
FIREBASE_CLIENT_EMAIL=firebase-adminsdk-xxxxx@your-project.iam.gserviceaccount.com
FIREBASE_DATABASE_URL=https://your-project-id.firebaseio.com
FIREBASE_STORAGE_BUCKET=your-project-id.appspot.com

# Server Configuration
PORT=5000
NODE_ENV=development

# Firebase Web Config (for frontend)
FIREBASE_API_KEY=your-api-key
FIREBASE_AUTH_DOMAIN=your-project-id.firebaseapp.com
FIREBASE_APP_ID=your-app-id
```

#### D. Update Frontend Firebase Config

Edit `frontend/js/main.js` and replace the Firebase config (lines 2-10):

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
    databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT_ID.appspot.com",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### 4. Seed the Database

Initialize the database with all departments, years, and subjects:

```bash
npm run seed
```

This will create the complete department structure with:
- 10 departments
- Multiple years per department (FirstYear, SY, TY, FY)
- Theory and Lab sections
- Subjects with units

### 5. Start the Backend Server

```bash
npm start
```

Or for development with auto-reload:

```bash
npm run dev
```

The server will run on `http://localhost:5000`

### 6. Serve the Frontend

You can use any static file server. Options:

**Option A: Live Server (VS Code Extension)**
- Install "Live Server" extension in VS Code
- Right-click `frontend/index.html` → "Open with Live Server"

**Option B: Python HTTP Server**
```bash
cd frontend
python -m http.server 8000
```

**Option C: Node.js HTTP Server**
```bash
npx http-server frontend -p 8000
```

Access the app at `http://localhost:8000`

## 📚 Database Structure

```
notes-organizer/
├── Departments/
│   ├── applied-science/
│   │   └── FirstYear/
│   │       ├── Theory/
│   │       │   ├── Engineering Mathematics I/
│   │       │   │   ├── Unit 1/
│   │       │   │   │   └── {noteId}/
│   │       │   │   │       ├── title
│   │       │   │   │       ├── fileUrl
│   │       │   │   │       ├── uploadedBy
│   │       │   │   │       └── uploadedAt
│   │       │   └── ...
│   │       └── Labs/
│   │           └── ...
│   ├── it/
│   │   └── SY/ (Only Second Year for IT)
│   ├── computer/
│   │   ├── SY/
│   │   ├── TY/
│   │   └── FY/
│   └── ... (other departments)
└── Users/
    └── {userId}/
        ├── email
        ├── role (teacher/student)
        ├── department
        ├── year
        ├── division
        └── createdAt
```

## 🎓 Departments & Years

### 1. **Applied Science & Humanities**
- First Year (Common for all branches)
- No Open Elective

### 2. **Information Technology (IT)**
- Second Year only (SY1, SY2 divisions)

### 3. **Artificial Intelligence & Data Science (AIDS)**
- Second Year only (SY1, SY2 divisions)

### 4. **Computer Engineering**
- SY, TY, FY (3 divisions each)

### 5. **Electronics & Telecommunication (ENTC)**
- SY, TY, FY (2 divisions each)

### 6-10. **AIML, DS, Electrical, Mechanical, Civil**
- SY, TY, FY (varying divisions)

## 👥 User Roles

### Teacher
- Upload notes (file or external link)
- Organize notes by department, year, section, subject, and unit
- View upload history

### Student
- Browse all departments and subjects
- Download/view notes
- Quick access to their department

## 🔐 Firebase Security Rules

### Realtime Database Rules

```json
{
  "rules": {
    "Departments": {
      ".read": "auth != null",
      ".write": "auth != null && root.child('Users').child(auth.uid).child('role').val() === 'teacher'"
    },
    "Users": {
      "$uid": {
        ".read": "auth != null && auth.uid === $uid",
        ".write": "auth != null && auth.uid === $uid"
      }
    }
  }
}
```

### Storage Rules

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /{allPaths=**} {
      allow read: if request.auth != null;
      allow write: if request.auth != null;
    }
  }
}
```

## 🎨 Design Theme

- **Background**: #f8fafc
- **Primary Blue**: #2563eb
- **Hover Blue**: #1d4ed8
- **Text Dark**: #111827
- **Text Gray**: #6b7280
- **Gradient**: #e0e7ff → #fef9c3
- **Font**: Poppins
- **Animations**: 0.3s ease transitions

## 📱 Pages Overview

### 1. Landing Page (`index.html`)
- Hero section with call-to-action
- Features showcase
- Departments preview

### 2. Login/Register (`login.html`)
- Tab-based authentication
- Email/password authentication
- Role selection (Teacher/Student)
- Department and year selection

### 3. Departments Browser (`departments.html`)
- Sidebar with all departments
- Expandable year selections
- Theory/Lab tab switcher
- Subject cards with modal details
- Unit-wise notes display

### 4. Teacher Dashboard (`dashboard_teacher.html`)
- Upload form with file/link options
- Department, year, section, subject selection
- Unit selection
- Recent uploads view

### 5. Student Dashboard (`dashboard_student.html`)
- Quick access to own department
- Recent notes overview
- Browse all departments link

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Authenticate user

### Notes
- `POST /api/notes/upload` - Upload note (Teacher only)
- `GET /api/notes/:department/:year/:section` - Get notes
- `GET /api/notes/subjects/:department/:year` - Get subjects
- `DELETE /api/notes/:noteId` - Delete note (Teacher only)

## 🧪 Testing

### Create Test Users

**Teacher Account:**
- Email: teacher@test.com
- Password: test123
- Role: Teacher
- Department: Computer Engineering
- Year: TY

**Student Account:**
- Email: student@test.com
- Password: test123
- Role: Student
- Department: Computer Engineering
- Year: SY

### Test Upload Flow

1. Login as teacher
2. Navigate to dashboard
3. Fill upload form
4. Upload file or paste link
5. Verify note appears in database

### Test Download Flow

1. Login as student
2. Browse departments
3. Select department → year → section → subject
4. Click subject card to view units
5. Download notes

## 🚀 Deployment

### Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize hosting
firebase init hosting

# Deploy
firebase deploy
```

### Netlify

1. Connect repository to Netlify
2. Set build command: `npm install`
3. Set publish directory: `frontend`
4. Deploy backend separately (Heroku, Railway, etc.)

## 🐛 Troubleshooting

### Common Issues

**Firebase Authentication Error:**
- Verify Firebase config in `main.js`
- Check if Email/Password auth is enabled

**Upload Fails:**
- Check Firebase Storage rules
- Verify file size (max 50MB)
- Check storage bucket name in `.env`

**Database Read/Write Error:**
- Verify Realtime Database rules
- Check if database URL is correct

**Server Won't Start:**
- Verify all environment variables
- Check if port 5000 is available
- Ensure Firebase Admin SDK JSON is correct

## 📄 License

MIT License - Feel free to use this project for educational purposes.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Support

For issues or questions, please open an issue in the repository.

---

**Built with ❤️ for academic excellence**
