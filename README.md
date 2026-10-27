# Alumni Management System (AMS)

A GitHub-ready college DBMS project based on the supplied report. It manages alumni profiles, events and registrations, fundraising campaigns and donations, job postings and applications, mentorship requests, and audit records.

## Stack
- Python + FastAPI REST API
- SQLite for a zero-configuration local demo (easy to switch to MySQL/PostgreSQL later)
- HTML, CSS and JavaScript frontend served by FastAPI
- JWT-based login and role checks
- SQL constraints, indexes, transactions, views and triggers

> This is a runnable prototype. The supplied report describes a React frontend and MySQL/PostgreSQL deployment; this ZIP uses a lightweight browser frontend and SQLite so it can be started locally without installing a database server. Do not claim performance metrics until you run and record tests.

## Requirements
- Python 3.10+
- Internet only for the first `pip install` (dependencies)

## Run on Windows
```powershell
cd Alumni_Management_System
py -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
copy .env.example .env
uvicorn app.main:app --reload
```

## Run on macOS/Linux
```bash
cd Alumni_Management_System
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --reload
```

Open:
- App: http://127.0.0.1:8000
- API docs: http://127.0.0.1:8000/docs

## Demo accounts
Seeded on first run:
- Administrator: `admin@ams.local` / `Admin@123`
- Coordinator: `coordinator@ams.local` / `Coord@123`
- Alumnus: `alumnus@ams.local` / `Alumni@123`

Change demo passwords and `JWT_SECRET` before any real deployment. Demo accounts are for local coursework only.

## Main features
- Login with JWT and role-based permissions (Administrator, Coordinator, Alumnus)
- Alumni profile listing, search and creation
- Create events; alumni can register/cancel; capacity is checked in a transaction
- Create fundraising campaigns and record donations; triggers maintain campaign totals
- Post jobs and apply; job owner/admin can review applications
- Request mentorship and approve/close requests
- Reports and audit log
- Database views, indexes and triggers in `database/schema.sql`

## API quick examples
After logging in at the UI, use `/docs` to explore endpoints. API authentication expects:
`Authorization: Bearer <access_token>`

Example login:
```bash
curl -X POST http://127.0.0.1:8000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"admin@ams.local","password":"Admin@123"}'
```

## GitHub upload
1. Extract the ZIP.
2. Create a new empty GitHub repository.
3. In this folder run:
```bash
git init
git add .
git commit -m "Initial Alumni Management System project"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```
Never commit real passwords, tokens, or personal alumni data. `.env` and the SQLite database are ignored by Git.

## Project structure
```text
Alumni_Management_System/
├── app/
│   ├── main.py
│   └── static/ (UI)
├── database/schema.sql
├── tests/test_smoke.py
├── .env.example
├── .gitignore
├── requirements.txt
└── README.md
```

## Limitations / next steps
- SQLite is configured for a single-machine academic prototype; use PostgreSQL/MySQL for production.
- Email/SMS notifications, password reset, production HTTPS, advanced audit immutability and full load testing are not implemented.
- Use only synthetic or authorized data.
