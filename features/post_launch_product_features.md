That’s a powerful, thoughtful roadmap — you’re moving toward a **truly smart bakery management system**. Here's an updated breakdown with the new business logic features, structured to make planning and optimization easier:

---

# 🧠 Advanced Business Logic Features (Planned)

## 🍰 1. **Batch-to-Recipe Linking**
- Each batch of inventory can reference a specific recipe
- Recipe includes ingredients and steps
- Recipes stored as structured data (JSON or relational)
- Recipes accessible on mobile during baking

### Implication:
- Need a `batches` table linking to `recipes` and possibly `products`
- Enables deeper traceability and in-app guidance for bakers

---

## 📏 2. **Recipe Scaling & Dynamic Inventory Updates**
- Scale recipe up/down based on quota or manual override
- Ingredient usage is calculated dynamically
- Scaled output quantity is what gets added to inventory

### Implication:
- Implement recipe math logic (multipliers)
- Add `yield` fields to recipes and ingredients
- Need to auto-deduct used ingredients from stock if tracked

---

## 📈 3. **Production Tracking for Managers**
- Generate summaries (daily/weekly) of what was produced
- Filter by product, date, or user
- Supports CSV export and visual charts

### Implication:
- Add production logs (when a batch is marked as complete)
- Need `completed_at`, `produced_by`, `produced_qty` fields

---

## 🧪 4. **Configurable Expiration Warnings**
- Set optional expiration dates for batches
- Send warnings before expiry if batch still in inventory
- Businesses can configure:
  - How many days before expiry to warn
  - How much quantity remaining triggers a warning

### Implication:
- Add `expires_at` to batch
- Add settings for `warn_days_before_expiry` and `warn_qty_threshold`
- Implement nightly cron job or real-time checks

---

## 🧾 5. **Sales Data Integration (e.g., Square)**
- Import sales reports to compare with inventory
- Show inventory depletion vs sales volume
- Helps bakeries track shrink, theft, or misbakes

### Implication:
- API integration or CSV import from Square
- Sales model needs mapping to inventory categories
- Build reconciliation logic between inventory + sales

---

Would you like me to now:
- Add these to your **post-launch roadmap file**?
- Break them into **design + dev tasks** per feature?
- Sketch a **data model update** showing how recipes, batches, and inventory connect?

You're setting yourself up for a seriously robust system. Let’s get this scoped and clean.