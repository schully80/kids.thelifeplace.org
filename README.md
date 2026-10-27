# The Life Place Kids

Production-oriented children’s ministry operations platform scaffold for The Life Place (Johannesburg).

## Stack
- Next.js (App Router)
- TypeScript (strict)
- Tailwind CSS
- Supabase PostgreSQL + Supabase Auth
- Zod + React Hook Form
- Lucide icons
- Vitest + Playwright

## Phase status
Phase 1 foundations are implemented:
- Project scaffold and design system shell
- Core route map (public + protected placeholders)
- Supabase client/server setup
- Initial schema migration with RLS and audit foundations
- Baseline unit/e2e tests scaffolding

Phase 2 has started:
- Functional family registration form (`/register`)
- API endpoint for registration persistence (`/api/register`)
- Additional migration for guardians, emergency contacts, authorized collectors, and consents
- Staff sign-in route (`/staff-login`)

Phase 3 has started:
- Classroom management API and UI (`/admin/classrooms`)
- Returning check-in API and kiosk flow (`/check-in`, `/api/check-in`)
- Volunteer handover queue and confirmation flow (`/handover`, `/api/handover/*`)
- Capacity and volunteer coverage enforcement in handover confirmation

Phase 4 has started:
- Collection credential generation during handover confirmation
- Secure check-out verification flow (`/check-out`, `/api/check-out/verify`)
- Pending collection queue API (`/api/check-out/pending`)
- Lost credential escalation API (`/api/check-out/lost-credential`)

Phase 5 has started:
- Volunteer operations dashboard (`/volunteer`, `/api/volunteer/dashboard`)
- Safeguarding incident logging + review (`/safeguarding/incidents`, `/api/safeguarding/incidents`)
- Admin attendance analytics (`/admin/attendance`, `/api/admin/attendance/summary`)

Phase 6 has started:
- Endpoint hardening with request throttling on registration, check-in, handover, check-out, and safeguarding APIs
- Strengthened HTTP security headers in middleware (CSP baseline + transport/cross-origin hardening)
- Rate-limit utility unit tests (`tests/unit/rate-limit.test.ts`)

## Local development
1. Copy `.env.example` to `.env.local` and fill Supabase values.
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run dev server:
   ```bash
   npm run dev
   ```
4. Run checks:
   ```bash
   npm run lint
   npm run typecheck
   npm run test
   npm run test:e2e
   ```

## Cloudflare Workers preparation

The Kids application has a separate OpenNext/Cloudflare Workers build path.
It does not configure or deploy the existing The Life Place website.

```bash
npm run build:cloudflare
npm run preview:cloudflare
```

See `CLOUDFLARE_DEPLOYMENT.md` for GitHub source configuration, Cloudflare and
Supabase environment variables, isolation requirements, and the mandatory
security and safeguarding gates. No automated deployment is configured.

## Supabase migration
Initial migration is in:

- `supabase/migrations/20261022170000_phase1_init.sql`

Apply through your Supabase workflow (CLI or dashboard SQL editor) to provision schema, enums, and policies.

## Security posture (Phase 1)
- Environment secrets externalized via `.env.local`
- Row-level security enabled on core tables
- Role-based route guards in server components
- Basic HTTP security headers in middleware

## Security posture (Phase 6 additions)
- In-memory rate limiting added for sensitive API operations
- Additional response hardening headers for browser isolation and content control

## Operational docs
- Deployment readiness checklist: `DEPLOYMENT_CHECKLIST.md`
- Security operations runbook: `SECURITY_RUNBOOK.md`
- Production environment template: `PRODUCTION_ENV_TEMPLATE.md`
- Phase 6 release notes: `RELEASE_NOTES_PHASE6.md`
- Go-live execution run sheet: `GO_LIVE_RUN_SHEET.md`
- UAT role-based signoff script: `UAT_TEST_SCRIPT.md`
- Rollback decision and comms playbook: `ROLLBACK_PLAYBOOK.md`
- Phase 6 leadership closeout: `PHASE6_CLOSEOUT.md`

## Next phase
Complete Phase 6 validation and deployment preparation.
# kids.thelifeplace.org
