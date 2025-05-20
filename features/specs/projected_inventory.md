# Projected Inventory


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


