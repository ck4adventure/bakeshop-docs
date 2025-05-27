# Weekly Production List

## Description
Rather than a bake to order business concept, many bakeries have a `DailyQuota` of items to be ready early each morning and sell them until they run out or close for the day. These baking numbers are often built on historical sales data in an attempt to be as efficient as possible with sales.

So first a weekly schedule is created for each item, deciding how many of that item might be sold for each day of the week, aka `DailyQuota`. This information is used to calculate how many minimum are needed for the entire week. The total needed for a single week is the `WeeklyProductionList`. The schedule of all the items for the week is finalized and called the `ProductionSchedule`.

In addition, stock is depleted via `SpecialOrders`.

Baker's are responsible for different items on the weekly par schedule to ensure there is always enough stock in the freezers/fridge (Inventory) to meet the demands of each day's DailyQuota and SpecialOrders. Many items have a minimum par, such as ensuring min 30 of each type of cookie is in stock at all times despite an avg DailyQuota of 12. 

## Roles
- Admin
- Manager
- Baker

## User Stories
### Manager Sets the Initial Weekly Schedule
Most likely the admin/manager will already have some sort of weekly schedule system. So on `ItemCreation` could also add in an optional `ProductionScheduleForm` for the item. Additionally, the `ItemDetailPage` should have a `ProductionSchedule` section in it which displays the current values and has a button to edit them.

### Manager Creates the Next Week's Schedule
1. Creates the schedule based on all active items' `ProductionSchedule`s. 



## Routes
## Web Components
- ProductionScheduleUpdateForm
- ProductionScheduleComponent
- both will have the days of the week and a count for each day

## Database Schemas
### Weekly Schedule Table
By keeping the item_id and weekday combination as the primary key, it implicitly enforces uniqueness of only one item count per weekday. Addtly, it won't matter what order the rows are written, the query will sort out each item's count for a given weekday. 

Could see eventually keeping a changelog for the production schedules table, but at the same time, those changes will be recorded in the bake_orders table.

```sql
CREATE TABLE production_schedules (
	customer_id UUID NOT NULL REFERENCES customers(id),
  item_id INTEGER REFERENCES items(id) ON DELETE CASCADE,
  weekday SMALLINT NOT NULL CHECK (weekday BETWEEN 0 AND 6),  -- 0 = Sun
  quantity INTEGER NOT NULL CHECK (quantity >= 0),
  PRIMARY KEY (item_id, weekday)
);
```

Each customer can create their own set of unique category names. Just had the aha! moment that all tables will need to store customer_id and index on it. I think I have this written down somewhere, good reminder.
```sql
CREATE TABLE production_categories (
	id INTEGER ...
	name VARCHAR(255) NOT NULL,
	customer_id UUID NOT NULL REFERENCES customers(id),
  description TEXT,
  created_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(customer_id, name)
)
```




