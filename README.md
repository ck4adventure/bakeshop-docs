# B2B Bakery Inventory App — System Overview

## Purpose

This is a bakery-focused inventory and production management system built for small-to-medium bakery operations. It helps bakers and managers:

- Track cookie dough and baked goods batches across their lifecycle
- Forecast and plan production based on quotas or real-time needs
- Avoid waste and stock-outs by managing batch expiration and inventory levels
- Integrate recipe logic directly into the flow of daily operations

## Vision

A lightweight but powerful **SaaS platform** that evolves from basic inventory tracking into a full smart bakery assistant — built for busy production teams, not IT departments.

---

## Architecture

| Component    | Stack / Tool                           | Description                                                |
| ------------ | -------------------------------------- | ---------------------------------------------------------- |
| **Frontend** | React, Vite, Tailwind                  | Mobile-responsive UI for bakery staff and managers         |
| **Backend**  | NestJS (Node.js)                       | REST API with scalable modular architecture                |
| **Database** | PostgreSQL (Neon)                      | Core data store for products, inventory, recipes, etc.     |
| **Auth**     | Clerk or Auth.js                       | Multi-tenant, role-based user auth (admin, manager, staff) |
| **Payments** | Stripe or LemonSqueezy                 | Subscription billing & metering (enterprise-ready)         |
| **Emails**   | Resend or Postmark                     | Password resets, digests, low inventory alerts             |
| **Hosting**  | Vercel (Frontend), Render/Fly.io (API) | Deploy and scale per component needs                       |

## Domain Models (Preview)
User — Belongs to a tenant, has a role (admin, manager, staff)

Product — A cookie dough, baked item, or related good

Recipe — Steps and ingredients for a product

Batch — An inventory unit tied to a recipe + yield

Inventory — Tracks live, usable inventory

Production Log — Captures what was made and when

Settings — Holds preferences like expiration warning thresholds

## Data Flow Example
1. Baker creates a new cookie dough batch from a saved recipe

1. The recipe scales based on quota, and ingredient deductions are auto-calculated

1. The batch is added to inventory, tagged with a timestamp and optional expiration

1. Daily summaries are generated, and low-stock warnings trigger as needed

1. Sales data from Square is reconciled against inventory to detect shrink