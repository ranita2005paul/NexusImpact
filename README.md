# NexusImpact — Product Requirements Document

## Original Problem Statement
NexusImpact is a humanitarian coordination platform that bridges NGOs, government agencies, and field volunteers via a Smart Resource Map and a proprietary priority algorithm `P = (Urgency·Wu + Time·Wt) / (Distance + 1)`. Goal: precision humanitarianism — cut response times by 40%, eliminate duplicate efforts.

## User Personas
- **NGO Admin** — coordinates organisation operations, sees full ops + AI insights
- **Government Admin** — multi-org oversight, analytics, AI insights
- **Volunteer** — field responder, sees open + assigned tasks

## Core Requirements (Static)
1. Smart Resource Allocation Engine (priority algorithm)
2. Smart Resource Map (Leaflet) with priority-coded markers
3. Mission Control Dashboard with live analytics + heat zones
4. AI Insights (Claude Sonnet 4.5)
5. Role-Based Access Control (3 roles)
6. Anonymized public view for privacy
7. Real-time updates (WebSocket)
8. Offline-first PWA (deferred to next phase)

## Architecture
- **Backend:** FastAPI + MongoDB (motor), JWT auth, bcrypt, emergentintegrations (Claude Sonnet 4.5)
- **Frontend:** React + Tailwind + shadcn/ui + Leaflet + react-leaflet + framer-motion + recharts + sonner
- **Design:** Hybrid — light humanitarian landing + dark Mission Control dashboard, International Orange (#FF4F00) accent, Outfit/IBM Plex Sans/Space Mono fonts

## Implemented (2026-02 — v1)
- ✅ JWT auth with 3 roles (register/login/me)
- ✅ Help Request CRUD with priority computation
- ✅ Self-assign + assignment + status transitions
- ✅ Smart Resource Map (Leaflet, dark theme, priority-coded markers)
- ✅ Mission Control Dashboard (stats, charts, live feed, AI panel)
- ✅ Submit Request page with Leaflet location pin
- ✅ Volunteer Tasks console (Available / Mine / Done tabs)
- ✅ Analytics endpoints (overview, timeline) with RBAC
- ✅ AI Insights via Claude Sonnet 4.5 (admin-only, executive bullet points)
- ✅ WebSocket live feed broadcasting create/assign/update events
- ✅ Anonymized public requests endpoint (jittered coords, no PII)
- ✅ Landing page with bento feature grid + CTA
- ✅ All 17 backend tests passing; frontend smoke tested

## Test Credentials
See `/app/memory/test_credentials.md`

## Backlog
### P0 (next)
- Emergent Google social login (alongside JWT)
- Heat-map overlay layer on dashboard map
- Assign-volunteer flow for admins (currently self-assign only)

### P1
- Offline-first PWA with service worker + IndexedDB sync queue
- Public anonymized map page (`/public-map`)
- Trend prediction (LLM-driven 7-day forecast)
- WebSocket auth + per-org channels

### P2
- End-to-end encryption for contact PII at rest
- Volunteer profile with skills + availability
- Multi-language support (i18n)
- Mobile native shell

## Notes for Future Iterations
- `server.py` is 479 lines — split into routers (auth/requests/analytics/ai/ws) before it exceeds 700.
- `list_public_requests` jitter uses Python `hash()` — switch to deterministic `hashlib.md5(id)` for stable anonymisation.
- `JWT_SECRET` should raise on missing env in production mode.
"## NexusImpact Test Credentials

### NGO Admin
- Email: admin@nexus.com
- Password: Admin123!
- Role: ngo_admin

### Government Admin
- Email: gov@nexus.com
- Password: Gov123!
- Role: gov_admin

### Volunteer
- Email: volunteer@nexus.com
- Password: Volunteer123!
- Role: volunteer
