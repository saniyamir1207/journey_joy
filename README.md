# Journey Joy

Journey Joy is a railway services prototype that brings passenger-facing journeys and railway operations tools together in one web application. The interface explores a connected experience for booking, passenger rewards, cleanliness reporting, lost and found, and railway intelligence.

> **Project status:** This repository is a prototype. Several screens and service integrations are demonstrative; the included FastAPI routes currently return basic placeholder responses. Review and connect production services before using the application with real passenger or operational data.

## What’s included

- A responsive web interface built with Next.js App Router and React.
- Passenger flows for sign-in, train booking, passenger details, payment, and confirmation.
- Pages for bookings, rewards, cleanliness reports, and lost and found.
- Railway intelligence screens for planning, operations, monitoring, insights, and assets.
- A FastAPI backend with starter route groups for booking, cleanliness, rewards, and lost and found.
- Health and configuration endpoints in the Next.js application.

## Technology

- **Web:** Next.js 16, React 19, TypeScript, Tailwind CSS 4
- **UI:** Lucide React, Framer Motion
- **API:** Python, FastAPI, Uvicorn
- **Backend utilities:** pandas, openpyxl, python-multipart

## Requirements

- Node.js compatible with Next.js 16 and npm
- Python 3.10 or later

## Run locally

### 1. Start the web application

From the repository root:

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### 2. Start the API backend

In a second terminal:

```bash
cd backend
python -m venv .venv
```

Activate the virtual environment, then install the dependencies and run the API:

```bash
# Windows PowerShell
.venv\Scripts\Activate.ps1
pip install -r requirement.txt
uvicorn main:app --reload --port 8000
```

```bash
# macOS / Linux
source .venv/bin/activate
pip install -r requirement.txt
uvicorn main:app --reload --port 8000
```

The API root is available at [http://localhost:8000](http://localhost:8000), and the interactive API documentation is at [http://localhost:8000/docs](http://localhost:8000/docs).

## Configuration

The frontend reads optional configuration from a `.env.local` file in the repository root. Do not commit real credentials or secrets.

| Variable | Purpose | Default |
| --- | --- | --- |
| `NEXT_PUBLIC_APP_NAME` | Display name reported by configuration | `Journey Joy` |
| `API_BASE_URL` | Configured API base URL | `http://localhost:3000` |
| `MAX_UPLOAD_SIZE_MB` | Upload size limit setting | `10` |
| `DATABASE_URL` | Database connection configuration | Unset |
| `AUTH_SECRET`, `SESSION_SECRET` | Authentication/session configuration | Unset |
| `AI_SERVICE_URL`, `AI_API_KEY` | AI service configuration | Unset |
| `OPENCV_SERVICE_URL` | Computer vision service configuration | Unset |
| `STORAGE_URL`, `STORAGE_ACCESS_KEY`, `STORAGE_SECRET_KEY` | Object storage configuration | Unset |
| `RAILWAY_AI_SERVICE_URL` | Railway intelligence service configuration | Unset |

For example, local development can use:

```dotenv
NEXT_PUBLIC_APP_NAME=Journey Joy
API_BASE_URL=http://localhost:8000
MAX_UPLOAD_SIZE_MB=10
```

Only configure credentials for services that are actually deployed and connected. The configuration endpoint reports whether selected settings are present; it does not verify that external services are reachable.

## Available scripts

| Command | Description |
| --- | --- |
| `npm run dev` | Start the Next.js development server |
| `npm run build` | Build the web application for production |
| `npm run start` | Serve a production build |
| `npm run lint` | Run ESLint |

## API routes

The FastAPI application currently exposes starter GET routes:

- `GET /` — API welcome/status message
- `GET /booking/`
- `GET /cleanliness/`
- `GET /rewards/`
- `GET /lost-found/`

The Next.js application also provides:

- `GET /api/health` — application health response
- `GET /api/config` — non-secret configuration status flags

Use `/docs` on the running FastAPI server to inspect its OpenAPI schema. The starter endpoints do not yet implement complete booking, reporting, authentication, payment, or AI workflows.

## Project structure

```text
app/                  Next.js pages, layouts, and API routes
  booking/             Booking flow screens
  railway-intelligence/Operations and planning screens
  api/                 Health and configuration endpoints
backend/               FastAPI application and route modules
  routes/              Booking, cleanliness, rewards, lost and found
lib/config/            Frontend environment and routing configuration
public/                Static assets
```

## Deployment

Build and run the frontend with `npm run build` and `npm run start`, or deploy it to a platform that supports Next.js. Deploy the FastAPI backend as a separate Python service and set the appropriate service URLs in the frontend environment. Configure secrets through the deployment platform’s secret manager, and enable only the external integrations the deployment actually uses.

## Contributing

1. Create a focused branch for your change.
2. Keep secrets and local environment files out of version control.
3. Run `npm run lint` and `npm run build` for frontend changes.
4. Include a concise description of behavior and any required configuration in your change.

## License

No license is currently specified. Contact the project maintainers before redistributing or reusing this code.
