# EstateHub

EstateHub is a full-stack real estate marketplace portfolio project for Bangladesh. It includes a React + TypeScript + Vite client and an Express + TypeScript + MongoDB API. Public sample cards are explicitly marked demo content; only approved database properties are public API results.

## Local setup

Requirements: Node.js 20+, npm, MongoDB 6+ (local or Atlas).

1. Copy `.env.example` to `server/.env`; set `MONGODB_URI`, strong JWT access secret and client origin. Optional SMTP and Cloudinary settings are documented.
2. Copy `client/.env.example` to `client/.env` and set `VITE_API_BASE_URL`.
3. Install: `npm install`, `npm --prefix server install`, `npm --prefix client install`.
4. Run `npm run dev`; client is at `http://localhost:5173`, API at `http://localhost:4000/api`.
5. Check `GET /api/health`. To create an administrator, set `ADMIN_EMAIL` and `ADMIN_PASSWORD`, then run `npm --prefix server run seed:admin`.

## API

Auth: register, login, logout, current user. Listings: paginated server-side search and filters, details, create/edit/delete, owner listings. Favorites: add/remove/list. Inquiries: public create, user list, owner list and status/response. Appointments: request, list, confirm/reject/reschedule. Admin: database stats, listing review/moderation, user list/suspension, reports. Health: `/api/health`.

All endpoints are under `/api`; Zod validates request payloads, APIs use JSON, access JWT is stored in an HTTP-only cookie, and server routes enforce roles and ownership. Public search returns approved listings only. New owner/agent listings need admin approval. Admin registration is disabled; seed an admin with environment credentials.

## Environment and deployment

Set production secrets in the host's secret store. Use MongoDB Atlas, strong independent JWT secrets, `NODE_ENV=production`, exact `CORS_ORIGINS`, `CLIENT_URL`, and HTTPS cookie domain as appropriate. Configure SMTP and Cloudinary credentials before enabling those integrations. Build with `npm run build`; run API with `npm --prefix server start`; serve `client/dist` with SPA route fallback to `index.html`. Verify `/api/health` and client deep links. No deployment was performed.

## Known integration gaps

The current baseline implements cookie access JWT, but not refresh rotation, email verification, forgot/reset password, profile editing, image upload or SMTP delivery. Image URLs can be stored through listing API, but no upload handler exists. The API models include image metadata, comparisons, categories, locations, notifications, reports, audit logs and settings, but their full management UI/routes are not complete. The UI does not yet expose saved-property dashboard, compare persistence, appointment workflows, full owner inquiry response flows or location CRUD. Do not treat these as production-ready. The demo cards are illustrative; they do not claim to be real listings or verified-agent records.

Run `npm test` and `npm run build`. Database-backed flows require MongoDB. Tests currently cover only lightweight configuration invariants; add isolated integration tests before production use.
