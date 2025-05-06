# 📅 B2B Bakery App – Master Feature Roadmap

This document tracks all planned features for bakery inventory and operations platform. Features are grouped by product maturity phase.

---

## 🚀 Phase 1: MVP (Core Inventory Operations & Forecasting)
*Goal: Launch usable, accurate inventory tracking system for bakeries*

- [ ] Product + batch tracking (base units, like cookie dough)
- [ ] Manual adjustments to stock (e.g. spoilage, transfers)
- [ ] Inventory projections based on planned baking schedules
- [ ] Track actual vs forecasted batch production
- [ ] View inventory by batch and freshness (FIFO)
- [ ] UI: Responsive React + Vite frontend
- [ ] Backend: NestJS + PostgreSQL on Neon
- [ ] Basic authentication and bakery tenant setup

---

## 📦 Phase 2: Smart Inventory + Recipe Integration
*Goal: Link inventory to recipes and enable production scaling*

- [ ] Batch-to-Recipe linking (traceability + batch guidance)
- [ ] Structured recipes (ingredients, steps, yield)
- [ ] Recipe scaling (adjust batch size dynamically)
- [ ] Auto-deduct ingredients when batch is made
- [ ] Ingredient-to-batch math (multipliers, yield, loss handling)
- [ ] Mobile visibility for recipe instructions (read-only)

---

## 📊 Phase 3: Production Tracking & Forecasting Tools
*Goal: Equip managers with insights and forecasting tools*

- [ ] Daily/weekly production summaries
- [ ] Filter views by product, staff, and date
- [ ] Charts and CSV export of production logs
- [ ] Track `produced_by`, `produced_qty`, and `completed_at`

---

## 🔔 Phase 4: Smart Alerts + Expiration Logic
*Goal: Help bakeries minimize waste and optimize stock*

- [ ] Expiration tracking (`expires_at` on batches)
- [ ] Configurable alert settings:
  - [ ] Days before expiry
  - [ ] Quantity threshold remaining
- [ ] Email or in-app alerts for expiring or low inventory
- [ ] Nightly cron job or real-time alert queue

---

## 📥 Phase 5: Sales Integration & Loss Tracking
*Goal: Reconcile production with real-world sales*

- [ ] Import sales reports (API or CSV from Square)
- [ ] Map sales to inventory categories
- [ ] Dashboard for shrink, theft, spoilage
- [ ] Sales vs inventory comparison and trends

---

## 📱 Phase 6: Mobile Readiness & Push Notifications
*Goal: Begin transition to mobile-native experience*

- [ ] Start migrating key flows to Expo (React Native)
- [ ] Local SQLite caching for offline mode
- [ ] Push notifications (low stock, reminders)

---

## 📈 Phase 7: Analytics & Reporting
*Goal: Provide operational insights for bakery owners*

- [ ] Activity dashboard (inventory trends, quota compliance)
- [ ] Alerts for abnormal days (low output, overproduction)
- [ ] Product popularity reports
- [ ] Export full reports to CSV/Excel

---

## 🛠️ Phase 8: Admin Tools & Support
*Goal: Internal tools for managing tenants and support*

- [ ] Admin dashboard for tenant viewing
- [ ] User impersonation for support
- [ ] Feature flags
- [ ] Multi-tenant activity logs

---

## 💰 Phase 9: Monetization & Growth
*Goal: Enable paid plans and grow user base*

- [ ] Stripe or LemonSqueezy billing integration
- [ ] Per-seat or per-location pricing support
- [ ] Referral tracking system
- [ ] Self-service team invites and onboarding

---

## 🏪 Phase 10: Multi-Location Support
*Goal: Support growing bakery chains and franchises*

- [ ] Support multiple locations per bakery account
- [ ] Role-based access per location
- [ ] Aggregated reporting across sites

---

## 🔐 Phase 11: Security, Audit, Compliance
*Goal: Prepare for enterprise and compliance demands*

- [ ] Audit logs (who did what, when)
- [ ] GDPR-compliant data export and deletion
- [ ] Custom RBAC (permissions matrix editor)
- [ ] SOC2 readiness checklist and audit tools

---

## ✉️ Phase 12: Communication & Email
*Goal: Automate ops communications and team coordination*

- [ ] Email templates (password reset, invites, reminders)
- [ ] Digest emails (daily/weekly inventory reports)
- [ ] Low-inventory and expiry alert emails
- [ ] Transactional email queue with retry and delivery tracking

---

## 📢 Phase 13: Feedback, Feature Requests, Community
*Goal: Enable feedback loops and encourage product adoption*

- [ ] Feedback collection portal (Canny-style or custom)
- [ ] In-app support chat (Intercom, Crisp, or custom)
- [ ] Public-facing roadmap (optional)