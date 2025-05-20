# Weekly Baking Schedule

## Description
Rather than a bake to order business concept, many bakeries bake a set quota of items early each morning and sell them until they run out or close for the day. These baking numbers are often built on historical sales data in an attempt to be as efficient as possible with sales.

So first a weekly schedule is created for each item, each day of the week with a number. This information is used to write out a planned schedule, creating bake plans for the next calendar week at the close of business Sunday. 

## Database Schemas
### Weekly Schedule Table
By keeping the item_id and weekday combination as the primary key, it implicitly enforces uniqueness of only one item count per weekday. Addtly, it won't matter what order the rows are written, the query will sort out each item's count for a given weekday. 

Could see eventually keeping a changelog for the production schedules table, but at the same time, those changes will be recorded in the bake_orders table.

```sql
CREATE TABLE production_schedules (
  item_id INTEGER REFERENCES items(id) ON DELETE CASCADE,
  weekday SMALLINT NOT NULL CHECK (weekday BETWEEN 0 AND 6),  -- 0 = Sun
  quantity INTEGER NOT NULL CHECK (quantity >= 0),
  PRIMARY KEY (item_id, weekday)
);
```

### Bake Runs Table (Bake Orders?)
This table is great because the data for a single item for the day is all contained here. This allows auditing of the adjustments made, as well as the special order count having been transferred over properly. The `is_completed` bool can be used to check status during the day of, but also trigger the write to the transaction_log for each item to aid in inventory counts.
```sql
CREATE TABLE bake_runs (
  id SERIAL PRIMARY KEY,
  item_id INTEGER NOT NULL REFERENCES items(id) ON DELETE CASCADE,
  bake_date DATE NOT NULL,
  
  base_quantity INTEGER NOT NULL DEFAULT 0,     -- from the schedule
  manager_override_quantity INTEGER,            -- optional override
  special_order_quantity INTEGER NOT NULL DEFAULT 0,
  
  final_quantity INTEGER GENERATED ALWAYS AS (
    COALESCE(manager_override_quantity, base_quantity) + special_order_quantity
  ) STORED,

  completed_quantity INTEGER DEFAULT 0 CHECK (completed_quantity >= 0),
  is_completed BOOLEAN DEFAULT FALSE,

  UNIQUE (item_id, bake_date)
);
```

### Query the Projected Daily Inventory
```sql
WITH RECURSIVE usage_projection AS (
  -- Start with current inventory
  SELECT
    pi.item_id,
    p.name AS item_name,
    CURRENT_DATE AS date,
    pi.quantity AS remaining_quantity
  FROM item_inventory pi
  JOIN items p ON p.id = pi.item_id

  UNION ALL

  -- Each next day, subtract that day's scheduled quantity
  SELECT
    up.item_id,
    up.item_name,
    up.date + INTERVAL '1 day' AS date,
    up.remaining_quantity - COALESCE(ps.quantity, 0) AS remaining_quantity
  FROM usage_projection up
  LEFT JOIN production_schedules ps
    ON ps.item_id = up.item_id
    AND EXTRACT(DOW FROM up.date + INTERVAL '1 day')::INT = ps.weekday
  WHERE up.remaining_quantity - COALESCE(ps.quantity, 0) >= 0
  -- Optional limit to 30 days to prevent runaway recursion
  AND up.date < CURRENT_DATE + INTERVAL '30 days'
)

SELECT
  date,
  item_name,
  remaining_quantity
FROM usage_projection
ORDER BY item_name, date;
```



## User Stories
### Manager Sets the Weekly Schedule
Most likely the admin/manager will already have some sort of weekly schedule system. So on `ItemCreation` could also add in an optional `weekly schedule form section` for the item. Additionally, the `ItemDetailPage` should have a `weekly quota` section in it which displays the current values and has a button to edit them.

## Creating a Quota Schedule
On adding an item the manager can specify a bake schedule. Form with fields for each day of the week and the expected count for each as a number counter. Save or cancel buttons

### Optional Active/Inactive Item Status
Active/Inactive as a flag for each item allows the system to filter items for the daily bake order list, and other things. Rules can be enforced on just active items, such as requiring a weekly quota schedule.

## As a manager, I want to override the scheduled daily bake quota with a different number
Usually it is to bake less than the scheduled quota, but also sometimes more. This could be a holiday, general uptick in sales or better than expected sales in some way. This number cannot be changed by the manager once the baker marks it complete.
