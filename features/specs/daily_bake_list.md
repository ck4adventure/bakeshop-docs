# Daily Bake List / Bake Run / Bakeoff

## Description

## Roles
- Admin
- Manager
- Baker

## User Stories
### As a manager, I generate the next week's daily bake orders from the schedule
Can automate this to once weekly, or let the manager do manually. It reads the current schedule of items, organizing them by day and creating daily bakeoff orders.

### As a baker, I want to view the daily bakeoff order
A top level menu item, the mobile view of the `TodaysBakesPage` is a scrollable list of cards of all the inventory items that are currently active, along with their total bake count for that particular day. "Chocolate Chip Cookies: 24", "Orange Scones: 15". Same color bar warnings can be used here, red if not enough for that quota, and black if zero items. Optional details could include freezer location. The `TotalBakeCount` is the sum of the scheduled bake quota and the `SpecialOrderCount` for that day.

### As a baker, I want to mark an item as pulled / complete
I pull the scheduled amount for each item and line them up for either preparation or set them as ready to bake in the racks. This effectively takes it out of inventory and deems it no longer usable. It's status can now only become sold or lost. 

Tapping a specific item card in the list will trigger a confirmation modal to mark the item as complete. Once the user confirms it, the transaction log is updated with the item and how many. 

### As a baker, I want to be able to hit the Undo Button and mark a DailyBake Item as not complete
Basically an undo button to unmark an item as complete. Should have a ConfirmationModal.

### As a baker, I want to be able to override the final count
Maybe I dropped a focaccia or burnt a sheet of cookies, I might need to add more to the baked/pulled count. Or possible there was less stock in the freezer than expected. When viewing the `ConfirmationModal` to mark an Item as Pulled, there is an increment counter to update the count. This might be something to flag in the user transaction logs to track who changes what, same for a manager upping a DailyBakeCount or any other override.

### As a baker, I want to Preview an upcoming day's bakeoff order
Requires some kind of Weekly/Monthly Calendar view page to choose which day's order to view. 

No updates to counts allowed by a baker to a bake order.

### As a manager I want to add a special order to a Day's Bakeoff Order
`Special Order` adds to the `ProjectedBakesLog` of bakes, and eventually the `TransactionLog` when the days order is marked complete. 

Might want to keep the `ProjectedBakesLog` entries in place to be able to track expected vs actual?

When viewing the Daily Order Page, there is a list of items and their counts. There could be a `+` button at the  bottom, which could use the same ChooserList of ActiveItems to this time add a SpecialOrder. A popup modal with the Item Name and count, this time defaulting to 1. Date, time and user is logged as well.  

### As a manager, I want to override the scheduled daily bake quota with a different number
Usually it is to bake less than the scheduled quota, but also sometimes more. This could be a holiday, general uptick in sales or better than expected sales in some way. This number cannot be changed by the manager once the baker marks it complete.


## Routes

## UI

## Database
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
