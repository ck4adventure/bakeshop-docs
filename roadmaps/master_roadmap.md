# 🧾 B2B Bakery Inventory App – Master Execution Checklist

This checklist breaks your product plan into discrete, scoped tasks per phase. Each item is designed to be actionable and implementation-ready.

---

## ✅ Phase 1: MVP – Core Inventory Operations

- [ ] Define MVP scope of user roles (admin, manager, staff)
- [ ] Set up tenant-aware authentication (one bakery per org)
- [ ] Create product model with categories (e.g. dough, fillings)
- [ ] Create batch model with quantity, unit, and created date
- [ ] Build batch creation UI with product selector
- [ ] Add manual stock adjustment UI (e.g. for waste or transfers)
- [ ] Display batch inventory list grouped by product
- [ ] Sort batches by age (FIFO logic)
- [ ] Create initial NestJS schema (products, batches, users)
- [ ] Build basic UI: mobile-friendly React + Vite app
- [ ] Deploy backend with Neon PostgreSQL
- [ ] Deploy frontend to Vercel (or similar)

---

## 🧠 Phase 2: Smart Inventory + Recipe Integration

- [ ] Design schema for `recipes` table (steps, ingredients, yield)
- [ ] Link `batches` to `recipes` (nullable foreign key)
- [ ] Build CRUD UI for creating and editing recipes
- [ ] Add structured `steps` and `notes` to recipe model
- [ ] Add “Make from Recipe” flow to create batch from recipe
- [ ] Add scaling input to allow recipe quantity adjustment
- [ ] Calculate used ingredient quantities on scaling
- [ ] Auto-deduct ingredients from inventory after batch is made
- [ ] Display scaled yield and notes on confirmation screen
- [ ] Add read-only mobile recipe view for production team

---

## 📈 Phase 3: Production Tracking & Forecasting

- [ ] Add production log table (batch, produced_by, completed_at)
- [ ] Mark batches as “produced” via a confirm UI
- [ ] Track produced quantity and who completed it
- [ ] Build daily production summary UI with filters (date, user, product)
- [ ] Enable CSV export of production logs
- [ ] Add chart view for production trends

---

## ⚠️ Phase 4: Expiration Tracking + Smart Alerts

- [ ] Add `expires_at` field to batches
- [ ] Add bakery settings for:
  - [ ] Days before expiry to trigger warning
  - [ ] Quantity threshold to trigger warning
- [ ] Build nightly cron job to detect expiring/low inventory
- [ ] Add alert UI for low/inventory warnings
- [ ] (Optional) Send alert via email or push (when available)

---

## 🧾 Phase 5: Sales Integration & Shrink Tracking

- [ ] Design import model for sales data (CSV or API)
- [ ] Build UI for uploading/exporting sales files
- [ ] Map sales items to inventory products
- [ ] Reconcile inventory depletion vs sales volume
- [ ] Display shrink/loss report by product and date
- [ ] Add visual charts of inventory vs sales trends

---

## 📱 Phase 6: Mobile Readiness & Push Notifications

- [ ] Start migration to React Native via Expo
- [ ] Implement offline caching via SQLite for inventory & recipes
- [ ] Enable push notifications for low stock and expiring batches
- [ ] Add basic mobile views: inventory, recipes, alerts

---

## 📊 Phase 7: Bakery Insights & Analytics

- [ ] Build dashboard with:
  - [ ] Inventory trends (over time)
  - [ ] Quotas met/missed
  - [ ] Production vs target
- [ ] Add product popularity stats (most baked goods)
- [ ] Generate alerts for unusually low or high production days
- [ ] Enable export to CSV/Excel

---

## 🔧 Phase 8: Admin Tools & Support

- [ ] Build admin dashboard to view tenants and users
- [ ] Add ability to impersonate users for support
- [ ] Log tenant activity and changes
- [ ] Add feature flag system for gradual rollouts
- [ ] Enable in-app support chat (e.g. Intercom or custom)

---

## 💵 Phase 9: Monetization & Growth

- [ ] Integrate Stripe or LemonSqueezy billing
- [ ] Add per-seat and/or per-location pricing model
- [ ] Track subscription usage and overages
- [ ] Add referral tracking logic (invite = discount)
- [ ] Build self-service onboarding for new teams

---

## 🏪 Phase 10: Multi-Location Support

- [ ] Add location model and associate with users/products
- [ ] Allow single tenant to manage multiple locations
- [ ] Implement role-based access by location
- [ ] Build aggregated reporting across locations

---

## 🔐 Phase 11: Security, Audit & Compliance

- [ ] Add audit logs for user actions (e.g. who created/adjusted what)
- [ ] Build tools for data export and deletion (GDPR compliance)
- [ ] Design custom role-permission matrix per tenant
- [ ] Draft and track SOC2 readiness checklist

---

## ✉️ Phase 12: Communication & Notification System

- [ ] Add email template system (password resets, invites, alerts)
- [ ] Send daily/weekly digest emails to managers
- [ ] Queue transactional emails with retries and logging
- [ ] Configure in-app notifications (alerts + activity)

---

## 📢 Phase 13: Feedback, Requests, Community

- [ ] Build feedback collection widget or portal
- [ ] Display public roadmap (optional toggle)
- [ ] Track feature upvotes and requests
- [ ] Prompt users for feedback after key actions

---

_Track progress by checking off tasks as you build. Phases may be adjusted based on user feedback and bakery needs._
