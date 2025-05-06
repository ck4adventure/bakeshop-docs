# Core Concepts for PMs — B2B Bakery Inventory App

This document outlines the essential bakery operations knowledge a Product Manager should understand when building and maintaining features for a smart bakery management system.

---

## 1. Par Level ("PAR")

* **Definition:** The standard quantity of a product that should be available or produced each day.
* **Why it matters:** Falling below par can affect fulfillment. Meeting or exceeding par supports efficiency and customer satisfaction.
* **Implications for product:**

  * Let users configure PAR by product/day/location
  * Display actual vs PAR on dashboards
  * Trigger inventory alerts when levels fall below PAR

---

## 2. Production Schedule

* **Definition:** A plan for what gets made and when (daily/weekly).
* **Why it matters:** Ensures labor and ingredient use align with demand.
* **Implications for product:**

  * Schedule by date/product/user
  * Export/print production lists
  * Forecast required ingredients from recipes

---

## 3. Batching & Yield

* **Definition:** A batch is a single run of production; yield is how much it produces.
* **Why it matters:** Accurate yields enable reliable inventory tracking.
* **Implications for product:**

  * Support yield values in recipe data
  * Track completed batch quantity
  * Connect batches to inventory entries

---

## 4. Shrinkage / Waste

* **Definition:** Inventory loss due to spoilage, mistakes, theft, or overproduction.
* **Why it matters:** Affects profitability and planning.
* **Implications for product:**

  * Track and categorize waste events
  * Report on shrinkage trends
  * Compare forecasted vs actual usage

---

## 5. Inventory Types

* **Definition:** Raw ingredients, intermediate (e.g., dough), finished goods.
* **Why it matters:** Different handling, shelf life, and processing rules apply.
* **Implications for product:**

  * Tag and distinguish inventory types
  * Apply expiration and tracking rules accordingly
  * Support flow: ingredients → dough → final products

---

## 6. Cost of Goods Sold (COGS)

* **Definition:** Total cost to produce an item, usually based on ingredient and labor cost.
* **Why it matters:** Drives pricing and margin decisions.
* **Implications for product:**

  * Store cost per unit for ingredients
  * Calculate total COGS per recipe
  * Flag low-margin products

---

## 7. Special Orders

* **Definition:** Custom or out-of-schedule production (e.g., event catering).
* **Why it matters:** These need tracking outside the regular workflow.
* **Implications for product:**

  * Enable ad hoc batch creation
  * Label batches linked to special orders
  * Include in reporting with separate filters

---

## 8. Quotas

* **Definition:** Target production numbers set by managers (e.g., 10 dough batches/week).
* **Why it matters:** Helps ensure supply meets forecasted demand.
* **Implications for product:**

  * Allow setting quotas by product/team
  * Track progress vs quota
  * Alert if under quota for the week

---

## 9. Allergens & Labeling

* **Definition:** Ingredient tagging for allergens (e.g., nuts, dairy).
* **Why it matters:** Safety and legal compliance.
* **Implications for product:**

  * Tag allergens in ingredient data
  * Inherit allergens into product metadata
  * Generate downloadable allergen reports

---

## 10. Multi-Location Operations

* **Definition:** Larger businesses may have multiple physical locations.
* **Why it matters:** Each location may have different needs and stock.
* **Implications for product:**

  * Support location-specific inventory and users
  * Enable role-based access per site
  * Offer both per-location and consolidated reporting

---

> This document is a living reference for PMs working on the B2B Bakery App. Update as the product and customer understanding evolve.
