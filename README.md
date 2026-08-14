# 🔐 Login Authentication System

A full-stack registration and login flow with hashed passwords, server-side sessions, and a protected dashboard route — themed as a vault: register for a key, log in to unlock it.

Built for the **Oasis Infobyte SIP — Web Development & Designing, Level 2**.

`Node.js` `Express` `SQLite` `bcrypt` `express-session`

🔗 **Repository:** [github.com/marium230-pixel/OIBSIP/tree/main/WebDev-L2-LoginAuth](https://github.com/marium230-pixel/OIBSIP/tree/main/WebDev-L2-LoginAuth)
🌐 **Live Demo:** [login-auth-app.bonto.run/login.html](https://login-auth-app.bonto.run/login.html)

---

## 📌 Task Objective

Build a client-or-full-stack authentication system with registration, login validation, and a protected page reachable only after a real login — with passwords never stored in plain text.

## 💡 Approach — Why Full-Stack (Option B)

Chose the Node.js + Express + SQLite path over a `localStorage`-only version because it's the option that actually enforces security server-side: a front-end-only "auth" system can always be bypassed by editing `localStorage` in dev tools. Here, session state lives server-side in an HTTP-only cookie, and the dashboard route checks that session before ever sending the page — not just before showing it.

Passwords are hashed with `bcrypt` (cost factor 10) before they ever touch the database. Login failures return one identical, generic error message regardless of whether the email or the password was wrong, so the system doesn't leak which accounts exist.

## ✨ Features

- 📝 Registration page — email + password fields, live client-side validation mirrored server-side
- 🔢 Password rule enforced both client- and server-side: minimum 8 characters, at least 1 number
- 🚫 Duplicate email check — clear error if the account already exists
- 🔑 Login page — email + password, generic error on any mismatch (never reveals which field was wrong)
- 🛡️ Protected `/dashboard` route — checked server-side via session; direct access without login redirects straight to `/login.html`
- 🚪 Logout clears the session and cookie, then returns to login
- 🔒 Passwords hashed with `bcrypt` — never stored or transmitted in plain text after registration
- ✅ Form validation blocks empty submissions on both pages

## 🛠️ Tech Stack

| Layer | Choice |
|---|---|
| Server | Node.js + Express |
| Sessions | `express-session` (HTTP-only cookie, 2-hour expiry) |
| Database | SQLite via `better-sqlite3` |
| Password hashing | `bcryptjs` |
| Frontend | Vanilla HTML/CSS/JS, `fetch` against a small JSON API |

## 🎨 Design Notes

Vault theme — deep emerald green paired with brass/copper accents, evoking a bank vault door rather than a generic login form. The dashboard's unlock icon and the "key to the vault" copy tie the visual metaphor to what an auth system is actually for: gatekeeping something behind a lock only the right credentials open.

## 📂 Project Structure

```
WebDev-L2-LoginAuth/
├── server.js              # Express app — routes, session middleware, validation
├── package.json
├── public/
│   ├── register.html
│   ├── login.html
│   ├── dashboard.html      # Protected — checks session before rendering
│   └── style.css
├── data/                   # SQLite database lives here at runtime (gitignored)
└── README.md
```

## 🚀 Running It Locally

```bash
git clone https://github.com/marium230-pixel/OIBSIP.git
cd OIBSIP/WebDev-L2-LoginAuth
npm install
npm start
```

Then open **http://localhost:3000** — it'll route you to `/login.html` (or `/dashboard` if already logged in). Register a new account, and the SQLite database is created automatically in `data/` on first run.

## 👩‍⚖️ Notes for Evaluators

- Try registering with a password under 8 characters or with no digit — both client and server reject it.
- Register the same email twice to confirm the duplicate check.
- Log in with a wrong password, then check the error message doesn't say which field was wrong.
- Visit `http://localhost:3000/dashboard` directly in a private/incognito window (no session) — it redirects straight to login rather than showing the page.
- Passwords are never visible anywhere — check the `data/users.db` file (or the `/api/register` network request) to confirm only the bcrypt hash is stored/sent back.

## 🔮 Possible Next Steps

- Forgot-password flow with a time-limited reset token
- Rate limiting on login attempts to slow brute-force guessing
- Email verification before first login

---

*#oasisinfobyte #webdevelopment #internship #nodejs*
