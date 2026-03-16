# TeachPortalWeb

A React web application for managing teachers and their students. Built as a full-stack project with a .NET backend API and a React frontend.

## Live Features

- **Authentication** — JWT-based login and registration with token expiry handling and automatic redirect on 401/403
- **Dashboard** — Add students, search and sort the student list, paginate results
- **Teacher Overview** — Browse all teachers, view each teacher's assigned students in a side-by-side panel layout
- **Responsive Design** — Mobile-first layout with a collapsible hamburger navigation menu

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, React Router v7 |
| HTTP Client | Axios (with request/response interceptors) |
| Auth | JWT stored in localStorage, parsed client-side for claims |
| Styling | Plain CSS with CSS custom properties (design tokens) |
| Backend API | ASP.NET Core (separate repo) |

## Project Structure

```
src/
├── Components/
│   ├── Layout.js          # Sticky navbar with hamburger menu
│   ├── Layout.css
│   ├── AuthLayout.js
│   └── PrivateRoute.js    # Route guard using AuthService.isAuthenticated()
├── Pages/
│   ├── Login/             # Sign-in form with client-side validation
│   ├── Signup/            # Registration form with password strength meter
│   ├── Dashboard/         # Add students + sortable/paginated table
│   └── TeacherOverview/   # Teacher list + student panel (side-by-side)
├── Services/
│   ├── AuthService.js     # Login, logout, JWT claims, token expiry check
│   └── api.js             # Axios instance with auth header + 401 redirect
└── Validation/
    └── validation.js      # Reusable field validators
```

## Getting Started

### Prerequisites

- Node.js 18+
- The backend API running at `https://localhost:7251` (or configure `REACT_APP_API_URL`)

### Installation

```bash
git clone https://github.com/nivigot/TeachPortalWeb.git
cd TeachPortalWeb
npm install
npm start
```

The app opens at `http://localhost:3000`.

### Environment Variables

Create a `.env` file in the project root to override the default API URL:

```
REACT_APP_API_URL=https://your-api-url/api
```

### Build for Production

```bash
npm run build
```

The optimised output is in the `build/` folder, ready to deploy to any static host (Netlify, Vercel, Azure Static Web Apps, etc.).

## Key Implementation Details

**JWT Auth Flow** — `AuthService` stores the token in `localStorage`, parses it to extract teacher ID and expiry, and exposes `isAuthenticated()` which checks the `exp` claim. The Axios interceptor automatically attaches `Authorization: Bearer <token>` on every request and redirects to `/login` on 401/403.

**Protected Routes** — `PrivateRoute` wraps authenticated pages and redirects unauthenticated users before the component mounts.

**Design System** — All colors, spacing, border radii, and shadows are defined as CSS custom properties in `index.css`, giving a single source of truth for the visual language across the app.

**Form Validation** — Both `Login` and `Signup` run client-side validation before any API call, with per-field inline error messages and a password strength meter on signup.

## Author

Gothai — [GitHub](https://github.com/nivigot)
