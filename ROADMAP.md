
# 📅 B2B Bakery App Roadmap (React + Vite + Nest)

Interesting pro/con - an app like this would require every baker to have a login and possibly use in on their phone, similar to square payroll. Not the worst, but something to keep in mind.

## ✅ Phase 1: Project Planning & Setup  
📅 Week 1  
- [X] Create a place to hold all design docs, plans and schemas
- [X] Define MVP scope and user roles (e.g., baker, manager)  
- [X] Set up GitHub monorepo or separate frontend/backend repos  
- [X] Set up Prettier, ESLint, commit linting  
- [X] Create shared style guide + component design plan  
- [X] Choose secrets management strategy (e.g., Doppler, `.env`, GitHub Actions)  
- [X] Draft a minimal privacy policy for test users  

## ✅ Phase 2: Tooling & Environment  
📅 Week 2  
- [X] Set up Vite + React + Tailwind CSS frontend  
- [X] Set up NestJS backend project 
- [X] Set up Postgresql Instance for dev env, decide on where to host in production
- [X] Use Prisma or TypeORM for DB layer  
- [X] Set up API docs using Swagger (Nest)  
- ~~[ ] Set up Docker for local dev (backend, db)~~, skipping for now  
- [ ] Set up CI pipeline for test/lint/build on push
- [ ] Add HTTPS support for local dev (e.g., mkcert)
- [X] Write out basic user stories to inform db schema

## ✅ Phase 3: Core Architecture  
📅 Weeks 3–4  
- [ ] Design frontend folder structure (e.g., pages, components, hooks, routes)  
- [ ] Create database schema: Users, Bakeries, Items, Quotas  
- [ ] Design backend modules (e.g., AuthModule, InventoryModule, BakeryModule)  
- [ ] Set up REST endpoints in NestJS (Auth, User, Inventory)  
- [ ] Implement global auth guard and roles guard (RBAC)  
- [ ] Define basic threat model (who might misuse the system?)
- [ ] Add helmet and CORS configuration in NestJS
- [ ] Sanitize and validate incoming requests (e.g., class-validator)  
- [ ] Add structured logging (e.g., pino, Winston) with request IDs  
- [ ] Write seed scripts for sample data  

## ✅ Phase 4: Auth & RBAC  
📅 Week 5  
- [ ] Add JWT-based login/register endpoint (NestJS)  
- [ ] Create frontend login + auth context  
- [ ] Protect routes on frontend (role-aware)  
- [ ] Secure backend with Passport strategies and decorators  
- [ ] Add logout, refresh tokens, and session storage (securely)  
- [ ] Set HttpOnly, SameSite, and Secure flags on cookies 🛡️  
- [ ] Hash passwords with bcrypt/argon2 🛡️  
- [ ] Add brute-force protection (e.g., rate limiting on login) 🛡️  
- [ ] Set up transactional email service (e.g., Resend, Mailgun, Postmark) ✉️  
- [ ] Implement password reset flow (request link, validate token, update password) ✉️  
- [ ] Implement bakery account invite email flow (optional) ✉️  

## ✅ Phase 5: MVP Features — Inventory Quota System  
📅 Weeks 6–7  
- [ ] CRUD: Create/Update/Delete inventory items  
- [ ] Set daily baking quota per item  
- [ ] Predict inventory run-out (based on usage rate)  
- [ ] Show upcoming low inventory warnings  
- [ ] Create responsive UI for inventory dashboard  
- [ ] Encrypt sensitive data at rest (e.g., bakery metadata) 🔍  
- [ ] Add database constraints + Prisma schema validations 🛡️  
- [ ] Write unit + integration tests for API endpoints 🧪  

## ✅ Phase 6: Mobile Responsiveness & UX Polish  
📅 Week 8  
- [ ] Responsive layout for mobile/tablet (Tailwind breakpoints)  
- [ ] UX polish (empty states, loading indicators, errors)  
- [ ] Accessibility pass (ARIA, keyboard nav)  
- [ ] Add unit tests (React Testing Library, Jest) 🧪  
- [ ] Add backend integration tests (Supertest) 🧪  
- [ ] Add basic Cypress E2E tests 🧪  

## ✅ Phase 7: Deployment & Hosting  
📅 Week 9  
- [ ] Deploy backend (e.g., Render, Fly.io, Railway)  
- [ ] Deploy frontend (e.g., Netlify, Cloudflare Pages, Vercel)  
- [ ] Set up domain name and SSL  
- [ ] Add staging + production environments  
- [ ] Set up monitoring/logging (e.g., Sentry, Logtail, Postgres dashboards)  
- [ ] Configure environment-based secrets handling 🛡️  
- [ ] Enable database access logging and query monitoring 🔍  
- [ ] Configure domain and sending domain for transactional email ✉️  
- [ ] Add DMARC/DKIM/SPF records for email deliverability ✉️  

## ✅ Phase 8: Private Beta Testing  
📅 Week 10  
- [ ] Invite 2–3 friendly bakeries to test MVP  
- [ ] Add feature flag system (to test in production safely)  
- [ ] Collect structured feedback via form or embedded tool  
- [ ] Fix bugs, polish flows based on tester feedback  
- [ ] Add analytics/events tracking (PostHog, Mixpanel) 🔍  
- [ ] Soft delete strategy for user/item deletion 🔍  

## ✅ Phase 9: Pre-Launch & Marketing  
📅 Week 11  
- [ ] Write landing page (can be static)  
- [ ] Add Intercom, Crisp, or similar for onboarding/help  
- [ ] Write onboarding flow + walkthrough  
- [ ] Write changelog system and in-app notification framework  
- [ ] Announce waitlist or early access  
- [ ] Perform final privacy/compliance pass (review data collection flows) 🔍  

## ✅ Phase 10: Launch 🎉  
📅 Week 12  
- [ ] Flip launch flag  
- [ ] Monitor usage and errors  
- [ ] Send first announcement email/newsletter  
- [ ] Create feedback loop (post-launch form or analytics)  
- [ ] Celebrate!
