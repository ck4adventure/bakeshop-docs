# Top Level Pages

## Inventory
/inventory
- show list of current items
- gets items current count
- evtl will compare count against a minimum par

## Production Schedules
/inventory/schedule
- shows chart of all the items currently with a schedule
- show current WeekOf
- prolly some kind of button to view daily bakeoff lists
- was gonna do a basic count update but might want to keep weekly entries

## Bakeoff List
/bakeoffs
/bakeoff/2025-05-12
- needs a mechanism to create bakeoff lists for the upcoming week, but only once
- adding in special order counts where exist
- bakeoff marked complete, all items added to the item even store, which triggers count update for each item as well
- prolly want a view page for recent history and upcoming

## Special Orders
/inventory/orders
- view page for all the entered special orders
- special orders filter into the bakeoff list as well

## Batches
/inventory/batches
- view page for all the recently created batches
- a created batch is written to the ItemEventStore which triggers count updates