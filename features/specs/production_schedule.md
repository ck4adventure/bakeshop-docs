# Weekly Baking/Production Schedule

## Description
Rather than a bake to order business concept, many bakeries bake a set quota of items early each morning and sell them until they run out or close for the day. These baking numbers are often built on historical sales data in an attempt to be as efficient as possible with sales.

So first a weekly schedule is created for each item, each day of the week with a number. This information is used to write out a planned schedule, creating bake plans for the next calendar week at the close of business Sunday. 

## User Stories
### Manager Sets/Updates the Weekly Schedule
Most likely the admin/manager will already have some sort of weekly schedule system. So on `ItemCreation` could also add in an optional `ProductionScheduleForm` for the item. Additionally, the `ItemDetailPage` should have a `ProductionSchedule` section in it which displays the current values and has a button to edit them.



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
  item_id INTEGER REFERENCES items(id) ON DELETE CASCADE,
  weekday SMALLINT NOT NULL CHECK (weekday BETWEEN 0 AND 6),  -- 0 = Sun
  quantity INTEGER NOT NULL CHECK (quantity >= 0),
  PRIMARY KEY (item_id, weekday)
);
```




