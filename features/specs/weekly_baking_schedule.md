# Weekly Baking Schedule

## Description
Rather than a bake to order business concept, many bakeries bake a set quota of items early each morning and sell them until they run out or close for the day. These baking numbers are often built on historical sales data in an attempt to be as efficient as possible with sales.

So first a weekly schedule is created for each item, each day of the week with a number. This information is used to write out a 

### Weekly Schedule Table
- id
- item_id
- weekday, 0-6, ensure know if sun or mon week start
- count
- UNIQUE (item_id, weekday), ensures only one entry per item per day of week

### Projected Daily Inventory
- id
- item_id
- date, not null
- qty, forecasted qty
- UNIQUE (item_id, date), ensures only one count per product per day



## User Stories
### Manager Sets the Weekly Schedule
Most likely the admin/manager will already have some sort of weekly schedule system. So on `ItemCreation` could also add in an optional weekly schedule for the item. 

