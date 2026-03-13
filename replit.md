# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Structure

```text
artifacts-monorepo/
├── artifacts/              # Deployable applications
│   ├── api-server/         # Express API server
│   └── ems-platform/       # Smart EMS React frontend
├── lib/                    # Shared libraries
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   └── db/                 # Drizzle ORM schema + DB connection
├── scripts/                # Utility scripts (single workspace package)
├── pnpm-workspace.yaml     # pnpm workspace
├── tsconfig.base.json      # Shared TS options
├── tsconfig.json           # Root TS project references
└── package.json            # Root package with hoisted devDeps
```

## Application: Smart EMS Platform

AI-powered Smart Emergency Medical Services platform with:
- **7 screens**: Command Center dashboard, Accident Report, Live Map, Ambulance Fleet, AI First Aid chatbot, Hospital Network, Emergency Contacts
- **Dark futuristic UI** with emergency red theme (NEXUS brand)
- **AI injury severity prediction** based on crash intensity, victim status, blood loss
- **AI first aid chatbot** with step-by-step instructions for common emergencies
- **Live simulated ambulance tracking** with ETA countdowns
- **Hospital bed availability dashboard** with real-time updates

## DB Schema

Tables:
- `accidents` - road accident reports with severity classification
- `ambulances` - ambulance fleet with status and location tracking
- `hospitals` - hospital bed availability (ICU/ER) and doctor availability
- `emergency_contacts` - user emergency contacts for notifications

## API Routes

All routes under `/api`:
- `GET /api/stats` - Dashboard statistics
- `GET/POST /api/accidents` - List and report accidents
- `PATCH /api/accidents/:id` - Update accident status
- `GET/POST /api/ambulances` - List and add ambulances
- `PATCH /api/ambulances/:id` - Update ambulance status/location
- `GET/POST /api/hospitals` - List and add hospitals
- `PATCH /api/hospitals/:id` - Update hospital bed availability
- `GET/POST /api/contacts` - Emergency contacts CRUD
- `DELETE /api/contacts/:id` - Delete contact
- `POST /api/ai/predict-severity` - ML injury severity prediction
- `POST /api/ai/first-aid` - First aid chatbot instructions

## Packages (EMS frontend)

- `leaflet` + `react-leaflet` - interactive OpenStreetMap map
- `framer-motion` - UI animations
- `recharts` - dashboard charts
- `date-fns` - date formatting
