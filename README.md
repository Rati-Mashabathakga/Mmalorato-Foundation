# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.


# Mmalorato Foundation — Web (React + Vite + Firebase)

**Last updated:** 09 Sep 2025

Public-facing website for the Mmalorato Foundation. Users can browse projects, learn about the mission, sign up / sign in, volunteer, and get involved.

---

## ✨ Features
- React 18/19 + Vite dev server
- Firebase **Auth** + **Firestore** (email/password, Google)
- AuthContext with protected routes
- Project grid, detail pages & “Get Involved” flows
- Framer Motion animations; Tailwind utilities
- Accessible, responsive layout (Navbar, Footer, Hero, LatestProjects, Blog)

---

## 🧱 Tech Stack
- **Frontend:** React, Vite, Tailwind CSS
- **Auth/DB:** Firebase Authentication, Cloud Firestore
- **Animations:** framer-motion

---

## 📦 Project Structure (key files)
```
/ (vite)
  index.html
  vite.config.js
  package.json
  /src
    main.jsx
    App.jsx
    index.css
    firebase.js
    AuthContext.jsx
    # Pages & sections
    Home.jsx
    About.jsx
    Contact.jsx
    GetInvolved.jsx
    Projects.jsx
    # Project detail pages
    CommunityGarden.jsx
    SolarEnergyAccess.jsx
    TechBootcamp.jsx
    WasteRecycling.jsx
    YouthLeadership.jsx
    NeighborhoodCleanup.jsx
    LiteracyCampaign.jsx
    CommunityArtMural.jsx
    AfterSchoolTutoring.jsx
    # UI components
    Navbar.jsx
    Hero.jsx
    AboutSection.jsx
    LatestProjects.jsx
    Blog.jsx
    Footer.jsx
    ProjectCard.jsx
    # Auth pages
    Login.jsx
    Signup.jsx
    # Utilities
    TestFirebase.jsx
```

---

## 🔐 Environment Variables
Create **.env.local** at the project root (never commit real keys).

```
VITE_FIREBASE_API_KEY=<<REDACTED>>
VITE_FIREBASE_AUTH_DOMAIN=<<REDACTED>>
VITE_FIREBASE_PROJECT_ID=<<REDACTED>>
VITE_FIREBASE_STORAGE_BUCKET=<<REDACTED>>
VITE_FIREBASE_MESSAGING_SENDER_ID=<<REDACTED>>
VITE_FIREBASE_APP_ID=<<REDACTED>>
VITE_FIREBASE_MEASUREMENT_ID=<<optional>>
```

Ensure `firebase.js` reads from `import.meta.env.*`.

---

## ▶️ Getting Started
```bash
# 1) Install
npm install

# 2) Run dev server
npm run dev

# 3) Build for production
npm run build

# 4) Preview production build
npm run preview
```

---

## 🔒 Firebase Security (high-level)
- Authenticated users may read published `projects`.
- Users may create their own `volunteers` records.
- Admin-only writes to `projects`. Enforce via Firestore security rules or Functions.
- Use `serverTimestamp()` for created/updated times.

Add your draft rules to `/firebase/firestore.rules` and reference them in docs.

---

## 🧪 Testing
Use the repo’s `/docs/Testing_Checklist.md` to track:
- Signup/Login (AuthContext)
- Projects grid filtering + detail pages
- Volunteer form write to Firestore
- Responsive checks (navbar collapse, cards stack)
- Lighthouse: Accessibility ≥ 90, Performance ≥ 80

Paste screenshots/evidence into the Phase 4 Word doc.

---

## 🧭 Coding Standards & POPIA
- Follow `/docs/Coding_Standards.md` (naming, structure, error-handling, formatting).
- Show consent before any data processing that identifies a person.
- Provide a **Delete My Data** path and document it.

---

## 🛠 Troubleshooting
- **Blank screen / auth loop?** Check `.env.local` and Firebase web origin settings.
- **Firestore permission denied?** Re-check security rules & user role.
- **Assets not showing in prod?** Use `/`-prefixed URLs or import images.

---

## 📸 Screenshots (to add before submission)
- Home/Hero, Projects grid, Project detail, Get Involved, Login/Signup, Contact/Footer

---

## 📄 License & Attribution
- Internal student project for assessment.
