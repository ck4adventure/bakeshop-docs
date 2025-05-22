# Projected Inventory

## Actions
A `BakeCalendar` can be built on query to project out the daily bakes, paying special attention to finding the `ParMinimumDate` and `ZeroItemsDate`. Could eventually use the calendar for other things, such as reminders.

Below all that would be a `BakedownChart` showing the expected `InventoryCount` for each day, again visually highlighting when the stock count reaches the `ParMinimum`, `DailyBakeQuota`, `ZeroItems`, etc.

## Routes
### Backend
`GET /inventory/:id/projection` returns the projection data from the query

## Web Components
`BakedownChart`, which uses the dates and counts for a given item's projected daily inventory to display a chart with dates for the x-axis, quantity for the y-axis. The user will be able to hover over 

## Database
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


